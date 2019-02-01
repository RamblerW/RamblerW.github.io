> ### 常用命令

* 创建项目：ng new project-name --style=scss （使用scss开发）
* 创建模块（一级菜单）：ng g module 模块名
* 创建组件（二级菜单）：ng g c 组件名
* 新增服务：ng g service 服务名
* 创建管道：ng g pipe 管道名

> ### 常用操作

1. 统计字符串长度（汉字也按照一个字符计算）：`[...str].length`

2. 循环标签中id拼接：
   `id="sLevelName_{{item.ID}}"`

3. 禁止触发行点击事件
   ts中弹框事件return之前加上：
   `event.stopPropagation();`

4. 根据条件添加样式
   * HTML:
     ```html
     <td [ngClass]="{'mark':item[0].launchName !== item[1].launchName,'unmark':item[0].launchName === item[1].launchName}">{{item[0].launchName}}</td>
     ```
   * CSS:
     ```css
     .mark{
       color: red;
     }
     .unmark{
       color: black;
     }
     ```

5. 覆盖框架样式
   自定义样式前加 
   ```css
   :host /deep/
   ```

6. 更新框架为最新

   `npm install portalface --save`

7. ng serve启动项目报如下错误：
   ![](../Resources/images/kyee/portalface_1.jpeg)
     执行 npm rebuild node-sass --force 后，再次运行 ng serve 启动项目，仍报上图中的错误。
   * 问题原因：rebuild node-sass 的时候，需要从github上下载文件，会涉及墙的问题
   * 解决方案：请翻墙或者连手机的热点再次执行 npm rebuild node-sass --force

8. Supplied parameters do not match any signature of call target.

   * 解决方案：执行 git merge origin/feiyi\_dev 与 npm install portalface --save

9. angular创建项目报错：cb\(\) never called!

   * 解决方案：执行npm cache verify命令后，重新创建

10. 打包报错：JavaScript heap out of menory
     * 问题原因：node内存不够

     * 解决方案：`package.json`中，设置`build:prod`的值为
       ```
       node --max_old_space_size=8000 ./node_modules/@angular/cli/bin/ng build --prod
       ```

       使用`npm run build:prod`命令进行编译

11. 更新node后`ng serve`启动报错

      - 解决方案：
        1. 删除 node_modules，重新执行 `npm install`
        2. `npm install node-sass`
        3. `npm rebuild node-sass`

12. 跨域请求

      - 增加参数

        ```javascript
        xhrFields:{
        		  withCredentials: true
        }
        ```

13. 

### 资料

* angular-cli的用法以及一些常见命令：[https://github.com/angular/angular-cli](https://github.com/angular/angular-cli)
* angular的一个大致介绍（有助于形成知识体系）：[https://github.com/lizhonghui/blog/issues/14](https://github.com/lizhonghui/blog/issues/14)
* VScode请自行去官网安装，推荐自己使用的几款好用的插件，配合vscode使用有助于提高开发效率，很爽：
  * \[Angular 4 and TypeScript/HTML VS Code Snippets - Visual Studio Marketplace\]：[https://marketplace.visualstudio.com/items?itemName=danwahlin.angular2-snippets](https://marketplace.visualstudio.com/items?itemName=danwahlin.angular2-snippets)
  * 快捷生成代码片段：
    [https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2](https://marketplace.visualstudio.com/items?itemName=johnpapa.Angular2)
  * 自动导包：
    [https://marketplace.visualstudio.com/items?itemName=steoates.autoimport](https://marketplace.visualstudio.com/items?itemName=steoates.autoimport)
  * css智能提示：
    [https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion](https://marketplace.visualstudio.com/items?itemName=Zignd.html-css-class-completion)
  * TS语法错误提示：
    [https://marketplace.visualstudio.com/items?itemName=eg2.tslint](https://marketplace.visualstudio.com/items?itemName=eg2.tslint)



