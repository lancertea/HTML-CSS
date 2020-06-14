### XML、HTML、SGML之间的关系
![XML、HTML、SGML](https://github.com/lancertea/HTML-CSS/blob/master/img/HTML.png)
- ML “Markup language(置标语言)”，用标准的标记来解释纯文本文档的内容，从而提供关于文档结构或文档该如何渲染的信息。
- GML 是第一代置标语言，使文档能明确将标示和内容分开，所有文件使用同样的标示方法。
- SGML 在 GML 的基础上进行整理，形成了一套非常严谨的文件描述方法。它的组成包括语法定义，DTD，文件实例三部分。
- HTML 是人们抽取了 SGML 的一个微小子集而提取出来的。其早期规范比较松散，但比较易学。
- XML 也是 SGML 的一个子集，但使用比较严格的模式。
- XHTML 的出现是因为HTML扩充性不好，内容的表现跟不上时代的变化（如无法表示某些化学符号等），以及因为性能的问题，官方逐渐趋于严格的模式，所以使用 XML 的严格规则的 XHTML 成了 W3C 计划中 HTML 的替代者。

HTML 经过一系列修订，到现在说的 HTML 一般指 HTML 4.01；而现在的 HTML 5 则是 HTML 的第五个修订版，其主要的目标是将互联网语义化，以便更好地被人类和机器阅读，并同时提供更好地支持各种媒体的嵌入。而HTML5本身并非技术，而是标准。它所使用的技术早已很成熟，国内通常所说的html5实际上是html与css3及JavaScript和api等的一个组合，
大概可以用以下公式说明：HTML5 ≈ HTML + CSS 3 + JavaScript + API.

### Doctype 作用？标准模式与兼容模式各有什么区别?
DOCTYPE是用来声明文档类型和DTD规范的。 <!DOCTYPE html>声明位于HTML文档中的第一行，不是一个HTML标签，处于 html 标签之前。告知浏览器的解析器用什么文档标准解析这个文档。DOCTYPE不存在或格式不正确会导致文档以兼容模式呈现。
标准模式的排版 和 JS 运作模式都是以该浏览器支持的最高标准运行。在兼容模式中，页面以宽松的向后兼容的方式显示,模拟老式浏览器的行为以防止站点无法工作。
在HTML4.01中<!doctype>声明指向一个DTD，由于HTML4.01基于SGML，所以DTD指定了标记规则以保证浏览器正确渲染内容 HTML5不基于SGML，所以不用指定DTD

### 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？
定义：CSS 规范规定，每个元素都有 display 属性，确定该元素的类型，每个元素都有默认的 display 值，如 div 的 display 默认值为“block”，则为“块级”元素；span 默认 display 属性值为“inline”，是“行内”元素。
- 块级元素有：div ul ol li dl dt dd h1-h6 p

block 独占一行，可以设置宽高，子元素的默认宽度为父元素宽度（仅是宽度可以）
- 行内元素有：a b span img input select strong

incline 可以与其他行内元素位于同一行，设置长度和宽度无效，由内容决定长度，但是可以设置左右内边距和外边距（仅左右内外边距设置有效，上下无效）
- 行级块元素：img input button

inline-block 让block元素不再独占一行，多个block元素可以同排一行，且元素具有block的属性，可设置宽高，是block和inline元素的综合体。
- 空元素：没有内容的 HTML 元素

常见: br hr img input link meta

不常见: area base col command embed keygen param source track wbr
- 自闭合标签：没有结束标签的标签

表单元素 input、图片 img、换行 br、水平线 hr、meta 设置页面元信息、link 引用外部链接、base> 设置网页所有链接的相对目录(如根目录)

