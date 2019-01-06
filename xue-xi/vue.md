- 安装vue：`npm install vue -g`

- 安装命令行工具：`npm install vue-cli -g`

- 安装webpack：`npm install webpack -g`

- 创建项目：`vue init webpack 项目名`

- 启动：`npm run dev`

- 定义全局sass变量（参考链接：https://segmentfault.com/a/1190000015287756）

  -  `npm i sass-resources-loader`

  - 修改`vue-cli`的目录下`build/utils.js`，`scss`选项修改为：(color.scss为我自己创建的文件)

    ```javascript
    return {
        css: generateLoaders(),
        postcss: generateLoaders(),
        less: generateLoaders('less'),
        sass: generateLoaders('sass', { indentedSyntax: true }),
        // scss: generateLoaders('sass'),
        scss: generateLoaders('sass').concat({
          loader:'sass-resources-loader',
          options:{
            resources:path.resolve(__dirname,'../src/assets/style/color.scss')
          }
        }),
        stylus: generateLoaders('stylus'),
        styl: generateLoaders('stylus')
      }
    ```

  -  `color.scss`中可以使用`@import`导入其他scss文件，也可以使用`$`定义静态scss变量，如`$color-theme: #23262E;`

  - 使用：直接通过使用变量名（如`$color-theme`）使用。==style开始标签中要加`lang="scss"`==

  - 配置完毕后若未生效，重启试试

- 定义全局变量和函数（参考链接：https://segmentfault.com/a/1190000015842187）

  -  定义一个公共组件`Comm.vue`，内容如下：

   ```javascript
   <script type="text/javascript">
       // 定义一些公共的属性和方法
       const httpUrl = 'http://39.105.17.99:8080/'
       function commonFun() {
           console.log("公共方法")
       }
       // 暴露出这些属性和方法
       export default {
           httpUrl,
           commonFun
       }
   </script>
   ```

  - `main.js`中引入

   ```javascript
   // 导入共用组件
   import global from './Comm'
   Vue.prototype.COMMON = global
   ```

  - 使用

   ```javascript
   export default {
     data() {
       return {
         // 赋值使用, 可以使用this变量来访问
         globalHttpUrl: this.COMMON.httpUrl
       }
     }
   ```

---

> ##### Q：导入scss文件报错：==relative module was not found==

A：安装`node-sass`和`sass-loader`

> ##### Q：浏览器图标不能显示

A：将图标文件放在`static`文件夹下，然后`index.html`中加入代码`<link rel="shortcut icon" href="static/logo.png">`，`logo.png`为图标文件