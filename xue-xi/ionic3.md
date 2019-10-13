- 查看版本： `ionic -version`

- 创建应用：`ionic start 项目名 模板`（ionic start ionic3Demo tabs）blank-空项目，tabs-底部栏，sidemenu-侧滑栏

- 安装依赖：`cd ionic3Demo/`、` npm install`

- 安装cordova：`npm install -g cordova`

- 运行项目：`ionic serve`

- 添加平台：`ionic cordova platform add android`、`ionic cordova platform add ios`

- 编译（在platforms/android/build/outputs/apk会生成apk）

- 移除平台：`ionic cordova platform rm android`、`ionic cordova platform rm ios`

- 打包apk
  - `ionic cordova build android`
  - `ionic cordova build android --prod --release`（不需要签名）

- 设备连接电脑
  1. 打开设备“USB调试模式”
  - mac下查看设备ID：“关于本机“-“系统报告”-“硬件”-“USB”-“厂商ID”
  - 打开终端输入命令：open -e ~/.android/adb_usb.ini
  - 在adb_usb.ini文件中加入厂商ID
  - 保存adb_usb.ini文件，重启adb

- 真机调试：ionic cordova run android

- 浏览器调试：<a>chrome://inspect/#devices</a>

  - 控制台：点击 inspect（==若打开后的页面是空白，打开VPN后再重试==）

- 真机调试实时更新代码：ionic cordova run android -l -c 

- 打包APK：anroid studio: 打开已存在的项目=>build->build apk

- 生成keystore文件

- 使用jarsigner签名

- 压缩文件：/Users/rambler/Library/Android/sdk/build-tools/26.0.2/zipalign -v 4 apk路径 压缩后的名字.apk （在项目根目录生成apk）

- 手势滑动事件

  - swipeleft：左滑
  - swiperight：右滑
  - swipeup：上滑
  - swipedown：下滑

---

> ##### Q：android 运行出现```Application Error - The connection to the server was unsuccessful```或```Application Error - The connection to the server was unsuccessful. (file:///android_asset/www/index.html)```

R：可能是项目资源太多，启动的时间太久，导致超时

A：解决方案：在config.xml中设置超时时间（参考资料：https://www.cnblogs.com/huangenai/p/7373231.html）

```
<preference name="loadUrlTimeoutValue" value="100000" />
```

> ##### Q：ionic3定义```declare let cordova: any;```使用```cordova```时，浏览器提示```cordova is undefined```

R：cordova插件需要在真机或者模拟器上测试，不能在浏览器里测试

A：在真机或者模拟器上运行

> ##### Q：报错：`Execution failed for task ':app:transformClassesWithDexBuilderForDebug'`

A：删除platforms文件夹下的所有内容，重新添加平台

> ##### Q：`注: 某些输入文件使用或覆盖了已过时的 API。 注: 有关详细信息, 请使用 -Xlint:deprecation 重新编译`

A：在```platforms/android/build.gradle```中添加如下代码，可以看到详细的错误信息。（参看资料：https://blog.csdn.net/libeyond_/article/details/50904271）

```
allprojects {
    gradle.projectsEvaluated {
        tasks.withType(JavaCompile) {
            options.compilerArgs << "-Xlint:unchecked" << "-Xlint:deprecation"
        }
    }
}
```

> ##### Q：键盘弹出后tab页上移

R：在Android 和 iOS中, Ionic会试图阻止键盘的模糊输入以及聚焦元素，当在视图中滚动出现的时候。为了这项工作，任何可以获取焦点的元素必须在一个滚动视图或一个类似于带有滚动视图的Content指令内

A：添加平台依赖后，修改```platforms/android/AndroidManifest.xml```中的```windowSoftInputMode```的值为`adjustPan|stateHidden`（参考资料：https://blog.csdn.net/qq_32107121/article/details/78627196）

> ##### Q：ionic3打包报错：```Error: spawn EACCES```

R：权限问题

A：终端执行命令（参考资料：https://blog.csdn.net/wang1144/article/details/78772069）

```
chmod 777 "/Applications/Android Studio.app/Contents/gradle/gradle-4.1/bin/gradle"
```

> ##### Q：ionic3打包报错：

```
ERROR: In <declare-styleable> FontFamilyFont, unable to find attribute android:fontVariationSettings
ERROR: In <declare-styleable> FontFamilyFont, unable to find attribute android:ttcIndex
```

A：在platforms/android/build.gradle中加入（参考资料：https://www.cnblogs.com/madyina/p/8533505.html）

```
configurations.all {
    resolutionStrategy {
        force 'com.android.support:support-v4:27.1.0'
    }
}
```

> ##### Q：编译报错：```找不到tsconfig.json```

R：执行命令的当前路径不对

A：回到项目根目录执行编译命令

> ##### Q：运行报错：```Error: Cannot find module '../cordova/platform_metadata'```

R：插件库版本并没有升级到该版本

A：（参考资料：https://blog.csdn.net/qq_26744901/article/details/79180317）

```
npm uninstall -g cordova
npm install -g cordova@7.1.0
```

> ##### Q：ion-datetime的done事件监听

A：使用```ngModelChange```事件来监听（参考资料：http://www.codes51.com/itwd/4500106.html）

> ##### Q：ionic3 上下滑动不能触发

R：ionic3 采用hammerjs的手势事件，但是hammerjs的swipe默认是不允许垂直方向的滑动，因此，需要手动配置，并重载配置。

A：（参考资料：https://blog.csdn.net/Amesteur/article/details/80272147）

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

> ##### Q：ionic3 微信h5开发，页面中滑动时整个网页也会跟着动

A：给body标签添加禁止滑动或者拖拽事件（参考资料：https://blog.csdn.net/yingzhi3104/article/details/78730342）

```javascript
document.body.addEventListener('touchmove' , function(e){
e.preventDefault();
})
```

> ##### Q：ionic3使用本地图标

A：https://www.jianshu.com/p/0fdf88275350

```javascript
<script>
    setTimeout(function() {
        var links = document.getElementsByTagName('link');
        var linksLength = links.length;
        for (var i = 0; i < linksLength; i++) {
            if ('icon' === links[i].rel) {
                links[i].type = 'image/x-icon';
                links[i].href = 'assets/icon/favicon.ico';
            }
        }
        links = null;
    }, 0);
</script>
```

> ##### Q：全局隐藏scroll滚动条样式

A：https://blog.csdn.net/Neokekeke/article/details/78799430

```css
// 在app.scss中加入以下代码
::-webkit-scrollbar { display: none !important;}
```

