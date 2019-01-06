# Spring注解实现定时功能，动态改变cron

> 原文：https://www.cnblogs.com/rinack/p/6768136.html

```java
package com.kyee.feiyi.spider.schedule;

import java.util.Date;
import java.util.Locale;
import java.util.ResourceBundle;
import java.util.concurrent.Executor;
import java.util.concurrent.Executors;

import com.kyee.feiyi.spider.service.ISpiderProcessorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Lazy;
import org.springframework.scheduling.Trigger;
import org.springframework.scheduling.TriggerContext;
import org.springframework.scheduling.annotation.EnableScheduling;
import org.springframework.scheduling.annotation.SchedulingConfigurer;
import org.springframework.scheduling.config.ScheduledTaskRegistrar;
import org.springframework.scheduling.support.CronTrigger;
import org.springframework.stereotype.Component;

@Lazy(false)
@Component
@EnableScheduling
public class SpiderSchedule implements SchedulingConfigurer {

    @Autowired
    @Qualifier("spiderProcessorService")
    private ISpiderProcessorService spiderProcessorService;

    //获取定时器cron表达式
    private static String cron = ResourceBundle.getBundle("spider-cfg", Locale.getDefault()).getString("cronExpression");


    public Executor taskExecutor() {
        return Executors.newScheduledThreadPool(20);
    }

    @Override
    public void configureTasks(ScheduledTaskRegistrar taskRegistrar) {
        //用于设置定时任务线程数，默认不设置的话为单线程
        taskRegistrar.setScheduler(taskExecutor());
        taskRegistrar.addTriggerTask(new Runnable() {
            @Override
            public void run() {
                // 任务逻辑
                System.out.println("dynamicCronTask is running...");
            }
        }, new Trigger() {
            @Override
            public Date nextExecutionTime(TriggerContext triggerContext) {
                // 任务触发，设置任务的执行周期
                CronTrigger trigger = new CronTrigger(cron);
                Date nextExec = trigger.nextExecutionTime(triggerContext);
                return nextExec;
            }
        });
    }
}
```