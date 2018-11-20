# ionic3学习笔记
1. 查看版本： ionic -version
- 创建应用：ionic start 项目名 模板（ionic start ionic3Demo tabs）blank-空项目，tabs-底部栏，sidemenu-侧滑栏
- 安装依赖：cd ionic3Demo/;	npm install
- 运行项目：ionic serve
- 添加平台：ionic cordova platform add android / ionic cordova platform add ios
- 编译（在platforms/android/build/outputs/apk会生成apk）

 ionic cordova build android
 ionic cordova build android --prod --release（不需要签名）
- 设备连接电脑
  1. 打开设备“USB调试模式”
  - mac下查看设备ID：“关于本机“-“系统报告”-“硬件”-“USB”-“厂商ID”
  - 打开终端输入命令：open -e ~/.android/adb_usb.ini
  - 在adb_usb.ini文件中加入厂商ID
  - 保存adb_usb.ini文件，重启adb
- 真机调试：ionic cordova run android
- 浏览器调试：<a>chrome://inspect/#devices</a>
- 真机调试实时更新代码：ionic cordova run android -l -c 
- 打包APK：anroid studio: 打开已存在的项目=>build->build apk
- 生成keystore文件
- 使用jarsigner签名
- 压缩文件：/Users/rambler/Library/Android/sdk/build-tools/26.0.2/zipalign -v 4 apk路径 压缩后的名字.apk （在项目根目录生成apk）