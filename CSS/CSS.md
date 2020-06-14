### 添加样式的方式
- 导入式：在 .css文件中使用@import url("...")来引入另一个css样式表
- 外部式：写在一个单独的文件中，在html页面中的head中使用 link 标签引入
```javascript
<link rel="stylesheet" type="text/css" href="a.css" />
```
- 内部式(嵌入式)：在HTML页面中的style标签中使用样式 
```javascript
<style type="text/css">...</style>
```
- 内联式：html标签的内部使用style属性设置的样式，直接与当前html标签相关联
```javascript
<div style=" width:100px；high:100px "></div>//(样式之间用；隔开)
```

#### 页面导入样式时，使用 link 和@import 有什么区别？
HTML外部资源链接元素 (<link>) 规定了当前文档与外部资源的关系。该元素最常用于链接样式表，此外也可以被用来创建站点图标
- link属于XHTML标签，除了加载CSS 外，还能用于定义RSS, 定义rel连接属性等作用；而@import是CSS提供的，只能用于加载CSS;link 可以通过 rel="alternate stylesheet" 指定候选样式
- 页面被加载的时，link 会同时被加载（最大限度支持并行下载），而@import 引用的 CSS 会等到页面被加载完再加载（过多嵌套导致串行下载，出现 FOUC）。
- import 是 CSS2.1 提出的，只在 IE5 以上才能被识别，而 link 是 XHTML 标签，无兼容问题;
- link 支持使用 js 控制 DOM 去改变样式，而@import 不支持;

#### 什么是 FOUC(Flash of Unstyled Content)？ 如何来避免 FOUC？
FOUC即无样式内容闪烁（Flash Of Unstyled Content），是在IE下通过@import导入css文件引起的。IE会首先加载整个HTML文档的DOM，然后再导入外部的css文件。因此，在页面DOM加载完成到css导入完成之间，有一段时间页面上的内容是没有样式的，这段时间的长短跟网速和电脑速度都有关系。  
解决方法：在<head>之间加入一个<link>标签来导入css文件。