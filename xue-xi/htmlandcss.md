> ### HTML
- 一个汉字的占位符：```&emsp;```

- 半个汉字的占位符：```&ensp;```
- 让浏览器直接输出HTML代码而不解析：将HTML代码嵌入到```<script type='text/html' style='display:block'></scipt>```中

> ### CSS

- 宽和高按比例设置：

```css
width: 40%;
height: 0;
/*padding如果是百分比的话,那这个百分比是相对于其父元素的宽度而言*/
padding-bottom: 40%;
```
- ```z-index```和```position: absolute;```要同时使用才能生效。

> ### SCSS
- 获取子元素

```css
:nth-child(1)
```