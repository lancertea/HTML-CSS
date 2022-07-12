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

#### 选择器权重计算方式
!important 无限大
内联样式 1000
id选择器 100
类选择器 | 属性选择器 | 伪类选择器 10
html标签 | 伪元素选择器 1
通配符* ｜ 关系选择器 ｜ 否定伪类 0
权重值相同的情况下，后面的样式会覆盖前面的

#### 伪类和伪元素区别
**CSS引入伪类和伪元素概念是为了格式化文档树以外的信息。也就是说伪类和伪元素是用来修饰不在文档树中的部分，比如，一句话中的第一个字母，或者是列表中的第一个元素。**
伪元素:在内容元素的前后插入额外的元素（行内元素）或样式（CSS语法），但是这些元素实际上并不在文档中生成。它们只在外部显示可见，但不会在文档的源代码中找到它们，因此，称为“伪”元素。例如：
```javascript
p::before {content:"第一章：";}
p::after {content:"Hot!";}
p::first-line {background:red;} 
p::first-letter {font-size:30px;}
```

伪类: 将特殊的效果添加到特定选择器上。它是已有元素上添加类别，不会产生新的元素。
- 伪类用来当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。比如说，当用户悬停在指定元素的时，我们可以通过`:hover`来描述这个元素的状态。虽然它和普通的CSS类相似，可以为已有的元素添加样式，但是它只有处于dom树无法描述的状态下才能为元素添加样式，所以将其称为伪类。
例如：
```javascript
a:hover {color: #FF00FF} 
p:first-child {color: red}
```

区别
- 伪类的操作对象是文档树中已有的元素，而伪元素则创建了一个文档树外的元素。因此，伪类和伪元素的区别在于：有没有创建一个文档树之外的元素。

伪类
- `:link`:选择未访问的链接
- `:hover`：选择鼠标指针浮动在其上的元素
- `:focus`：选择获取焦点的输入字段
- `:active`：选择活动的链接
- `first-child`：匹配元素的第一个子元素

伪元素
- `::before`:在被选元素前插入内容
- `::after`: 在被元素后插入内容
- `::first-letter/:first-letter`: 匹配元素中文本的首字母
- `::first-line/:first-line`：匹配元素中的第一行的文本
- `::placeholder`: 匹配占位符的文本，只有元素设置了`placeholder`属性时，该伪元素才能生效

#### ::before 和 :after 中双冒号和单冒号有什么区别？
- CSS3 规范中的要求使用双冒号`（::）`表示伪元素，以此来区分伪元素和伪类，比如`::before`和`::after`等伪元素使用双冒号`(::)`，`:hover`和`:active`等伪类使用单冒号`(:)`。除了一些低于IE8版本的浏览器外，大部分浏览器都支持伪元素的双冒号`(::)`表示方法。虽然CSS标准要求伪元素使用双冒号的写法，但也支持单冒号的写法。为了向后兼容，我们建议你在目前还是使用单冒号的写法。

在 CSS 中伪类一直用 : 表示，如 :hover, :active 等  
伪元素在 CSS1 中已存在，当时语法是用 : 表示，如 :before 和 :after  
后来在 CSS3 中修订，伪元素用 :: 表示，如 ::before 和 ::after，以此区分伪元素和伪类  
由于低版本 IE 对双冒号不兼容，开发者为了兼容性各浏览器，继续使使用 :after 这种老语法表示伪元素  
综上所述：::before 是 CSS3 中写伪元素的新语法； :after 是 CSS1 中存在的、兼容 IE 的老语法

#### css 属性 content 有什么作用？
content 属性专门应用在 before/after 伪元素上，用于插入额外内容或样式（必须设置）

#### 选择器优先级
选择器越特殊，它的优先级越高。也就是选择器指向的越准确，它的优先级就越高，按照权重由高到低：  
!important最高  
内联样式 1000  
id选择器 100  
类选择器 | 属性选择器 | 伪类选择器 10  
html标签 | 伪元素选择器 1  
权重值相同的情况下，后面的样式会覆盖前面的

### 文本
首行缩进：text-indent
文本对齐方式：text-align
装饰线：text-decoration（none|underline|overline|line-through）

字体：font-family
字体大小： font-size
字体粗细：font-weight
字体样式：font-style（normal|italic）
字体颜色：color
字符间隔：letter-spacing
打断单词：word-break:break-all;

#### 文本省略
单行文本溢出显示省略号 
1.不换行：white-space: nowrap;
2.超出部分省略：overflow: hidden;
3.多出的文本变成省略号：text-overflow: ellipsis;

多行 除了IE都支持
display: -webkit-box;
-webkit-line-clamp: 3;
-webkit-box-orient: vertical;

