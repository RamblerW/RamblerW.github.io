# ionic3 的坑

1. android 运行出现```Application Error - The connection to the server was unsuccessful```或```Application Error - The connection to the server was unsuccessful. (file:///android_asset/www/index.html)```
    * 问题原因：可能是项目资源太多，启动的时间太久，导致超时
    * 解决方案：在config.xml中设置超时时间
```
<preference name="loadUrlTimeoutValue" value="100000" />
```
    * 参考资料：https://www.cnblogs.com/huangenai/p/7373231.html

- ionic3定义```declare let cordova: any;```使用```cordova```时，浏览器提示```cordova is undefined```
    * 问题原因：cordova插件需要在真机或者模拟器上测试，不能在浏览器里测试
    * 解决方案：在真机或者模拟器上运行
    
- 报错：```Execution failed for task ':app:transformClassesWithDexBuilderForDebug'```
    * 解决方案：删除platforms文件夹下的所有内容，重新添加平台
    
- 报错：```注: 某些输入文件使用或覆盖了已过时的 API。 注: 有关详细信息, 请使用 -Xlint:deprecation 重新编译```
    * 解决方案：在```platforms/android/build.gradle```中添加如下代码，可以看到详细的错误信息。
```
allprojects {
    gradle.projectsEvaluated {
        tasks.withType(JavaCompile) {
            options.compilerArgs << "-Xlint:unchecked" << "-Xlint:deprecation"
        }
    }
}
```
    * 参看资料：https://blog.csdn.net/libeyond_/article/details/50904271

- 键盘弹出后tab页上移
    * 问题原因：在Android 和 iOS中, Ionic会试图阻止键盘的模糊输入以及聚焦元素，当在视图中滚动出现的时候。为了这项工作，任何可以获取焦点的元素必须在一个滚动视图或一个类似于带有滚动视图的Content指令内
    * 解决方案：添加平台依赖后，修改```platforms/android/AndroidManifest.xml```中的```windowSoftInputMode```的值为```adjustPan|stateHidden```
    * 参考资料：https://blog.csdn.net/qq_32107121/article/details/78627196

- ionic3打包报错：```Error: spawn EACCES```
    * 问题原因：权限问题
    * 解决方案（Mac）：终端执行命令
```
chmod 777 "/Applications/Android Studio.app/Contents/gradle/gradle-4.1/bin/gradle"
```
    * 参考资料：https://blog.csdn.net/wang1144/article/details/78772069

- ionic3打包报错：
```
ERROR: In <declare-styleable> FontFamilyFont, unable to find attribute android:fontVariationSettings
ERROR: In <declare-styleable> FontFamilyFont, unable to find attribute android:ttcIndex
```
    * 解决方案：在platforms/android/build.gradle中加入
```
configurations.all {
    resolutionStrategy {
        force 'com.android.support:support-v4:27.1.0'
    }
}
```
    * 参考资料：https://www.cnblogs.com/madyina/p/8533505.html

- 编译报错：```找不到tsconfig.json```
    * 问题原因：执行命令的当前路径不对
    * 解决方案：回到项目根目录执行编译命令

- 运行报错：```Error: Cannot find module '../cordova/platform_metadata'```
    * 问题原因：插件库版本并没有升级到该版本
    * 解决方案：
```
npm uninstall -g cordova
npm install -g cordova@7.1.0
```
    * 参考资料：https://blog.csdn.net/qq_26744901/article/details/79180317

- ion-datetime的done事件监听
    * 解决方案：使用```ngModelChange```事件来监听
    * 参考资料：http://www.codes51.com/itwd/4500106.html

- ionic3 手势滑动事件
    - swipeleft：左滑
    - swiperight：右滑
    - swipeup：上滑
    - swipedown：下滑
- ionic3 上下滑动不能触发
    * 问题原因：ionic3 采用hammerjs的手势事件，但是hammerjs的swipe默认是不允许垂直方向的滑动，因此，需要手动配置，并重载配置。
    * 解决方案：
    
    ```
    1.编写配置文件
        1.1.下载hammerjs和类型描述文件：npm install hammerjs --save
        1.2.新建myHammer.config.ts文件，并写入以下内容：
        import { HammerGestureConfig } from '@angular/platform-browser';
        import * as Hammer from 'hammerjs';
        ///原因是hanmmerjs默认是手势事件都是水平方向的
        export class MyHammerConfig extends HammerGestureConfig {
          overrides = <any>{
            'swipe': { direction: Hammer.DIRECTION_ALL } // 重载设置
          }
        }
    2.模块的跟模块重载配置
        建议在app.module.ts模块导入：
        providers: [{ provide: HAMMER_GESTURE_CONFIG,  useClass: MyHammerConfig }]
    ```
    * 参考资料：https://blog.csdn.net/Amesteur/article/details/80272147
- ionic3 微信h5开发，页面中滑动时整个网页也会跟着动
    * 解决方案：给body标签添加禁止滑动或者拖拽事件
    ```javascript
    document.body.addEventListener('touchmove' , function(e){
    e.preventDefault();
})
    ```
    * 参考资料：https://blog.csdn.net/yingzhi3104/article/details/78730342