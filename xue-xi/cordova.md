- 使用插件
  - 安装SQLite插件：ionic cordova plugin add cordova-sqlite-storage
  - 将native插件写入package.json文件：npm install --save @ionic-native/sqlite
  - 在src/app/app.module.ts中添加：import {SQLite} from "@ionic-native/sqlite";
  - 在provides中添加 SQLite

- ts中使用插件：platforms/android/assets/www/cordova_plugins.js 查看对应插件的clobbers
- 删除插件：cordova plugin remove cordova-plugin-battery-status
- 查看当前项目的插件：ionic cordova plugin
- 自行扩展插件，编译时使用命令：cordova compile（不要使用cordova build, cordova build = cordova perpare + cordova compile）
- npm install 安装的东西，在页面中用 import * as io from 引用
- 制作插件
    - npm install -g plugman
    - 创建插件
    
    plugman create --name cordovaTcpSocket --plugin_id cordovaTcpSocket --plugin_version 1.0.0
    - 进入插件目录
    
    cd cordovaTcpSocket
    - 增加Android平台
    
    plugman platform add --platform_name android

##### 制作完成后

    - 添加package.json文件
    
    npm init
    
    - 安装插件
    
    cordova plugin add 插件路径
