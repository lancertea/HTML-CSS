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

### 选择器
#### 选择器分类
https://www.w3cschool.cn/css/css-selector.html
- （HTML元素）标签选择   eg: div{}
- id选择器    eg：#div
- class选择器   eg：.div
- 后代选择器 a b{}  用空格隔开   选中a的后代中的b(后代指后面很多代)元素
- 子代选择器 a>b{}  用箭头隔开   选中a的子代中的b(子代指下一代)元素
- 并集选择器 a,b{}  用逗号隔开    选中满足a或者b的元素
- 交集选择器 ab{}   没有分隔符    选中同时满足a和b的元素
- 相邻选择器 a+b{}  选中指定元素的直接后继元素(紧挨)    a~b{}:选择跟在目标元素后面的所有匹配的元素
ps: a，b可以是类选择器，标签选择器，id选择器
- 通配符选择 （*）
- 否定选择器 :not(.link){}
- 属性选择器   eg:a[title] 只会选择有title属性的元素
- 伪类选择器(:hover)
- 伪元素选择器 ::before{}

#### 伪类和伪元素区别
伪元素:在内容元素的前后插入额外的元素（行内元素）或样式（CSS语法），但是这些元素实际上并不在文档中生成。它们只在外部显示可见，但不会在文档的源代码中找到它们，因此，称为“伪”元素。例如：
```javascript
p::before {content:"第一章：";}
p::after {content:"Hot!";}
p::first-line {background:red;} 
p::first-letter {font-size:30px;}
```

伪类: 将特殊的效果添加到特定选择器上。它是已有元素上添加类别的，不会产生新的元素。例如：
```javascript
a:hover {color: #FF00FF} 
p:first-child {color: red}
```

#### ::before 和 :after 中双冒号和单冒号有什么区别？
在 CSS 中伪类一直用 : 表示，如 :hover, :active 等  
伪元素在 CSS1 中已存在，当时语法是用 : 表示，如 :before 和 :after  
后来在 CSS3 中修订，伪元素用 :: 表示，如 ::before 和 ::after，以此区分伪元素和伪类  
由于低版本 IE 对双冒号不兼容，开发者为了兼容性各浏览器，继续使使用 :after 这种老语法表示伪元素  
综上所述：::before 是 CSS3 中写伪元素的新语法； :after 是 CSS1 中存在的、兼容 IE 的老语法

#### css 属性 content 有什么作用？
content 属性专门应用在 before/after 伪元素上，用于插入额外内容或样式（必须设置）