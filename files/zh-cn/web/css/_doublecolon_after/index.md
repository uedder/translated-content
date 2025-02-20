---
title: '::after (:after)'
slug: Web/CSS/::after
---
{{ CSSRef() }}

CSS[伪元素](/zh-CN/CSS/Pseudo-elements)`::after`用来创建一个伪元素，作为已选中元素的最后一个子元素。通常会配合{{ cssxref("content") }}属性来为该元素添加装饰内容。这个虚拟元素默认是行内元素。

```
/* Add an arrow after links */
a::after {
  content: "→";
}
```

{{ fx_minversion_note("3.5", "Firefox 3.5 之前版本仅实现了 CSS 2.0 版本的语法<code> :after</code>. 且不允许在<code> position, float, list-style-* </code>等属性中使用。Firefox 3.5 开始没有了这项限制。") }}

## 语法

```
element:after  { style properties }  /* CSS2 语法 */

element::after { style properties }  /* CSS3 语法 */
```

`::after 表示法是在`CSS 3 中引入的，::符号是用来区分[伪类](/zh-CN/CSS/Pseudo-classes)和伪元素的。支持 CSS3 的浏览器同时也都支持 CSS2 中引入的表示法`:after。`

> **备注：** IE8 仅支持`:after`。

## 示例

### 简单用法

让我们创建两个类：一个无趣的和一个有趣的。我们可以在每个段尾添加伪元素来标记他们。

```html
<p class="boring-text">这是些无聊的文字</p>
<p>这是不无聊也不有趣的文字</p>
<p class="exciting-text">在 MDN 上做贡献简单又轻松。
按右上角的编辑按钮添加新示例或改进旧示例！</p>
```

```css
.exciting-text::after {
  content: "<- 让人兴兴兴奋！";
  color: green;
}

.boring-text::after {
  content: "<- 无聊！";
  color: red;
}
```

#### 输出

{{ EmbedLiveSample('Simple_usage', 500, 170) }}

### 装饰用法

我们几乎可以用想要的任何方法给 {{ cssxref("content") }} 属性里的文字和图片的加上样式。

```html
<span class="ribbon">Notice where the orange box is.</span>
```

```css
.ribbon {
 background-color: #5BC8F7;
}

.ribbon::after {
 content: "Look at this orange box.";
 background-color: #FFBA10;
 border-color: black;
 border-style: dotted;
}
```

#### 输出

{{ EmbedLiveSample('Decorative_example', 450, 20) }}

### 提示用法

接下来的示例展示了用`::after`[伪元素](/en/CSS/Pseudo-elements)，[`attr()`](/zh-CN/docs/CSS/attr)CSS 表达式和一个[自定义数据属性](/en/HTML/Global_attributes#attr-data-*) `data-descr` 创建一个纯 CSS，词汇表提示工具。在[单独页面](https://developer.mozilla.org/files/4591/css-only_tooltips.html)看这个例子。

```html
<p>这是上面代码的实现<br />
  我们有一些 <span data-descr="collection of words and punctuation">文字</span> 有一些
  <span data-descr="small popups which also hide again">提示</span>。<br />
  把鼠标放上去<span data-descr="not to be taken literally">看看</span>。
</p>
```

```css
span[data-descr] {
 position: relative;
 text-decoration: underline;
 color: #00F;
 cursor: help;
}

span[data-descr]:hover::after {
 content: attr(data-descr);
 position: absolute;
 left: 0;
 top: 24px;
 min-width: 200px;
 border: 1px #aaaaaa solid;
 border-radius: 10px;
 background-color: #ffffcc;
 padding: 12px;
 color: #000000;
 font-size: 14px;
 z-index: 1;
}
```

#### 输出

{{ EmbedLiveSample('Tooltips', 450, 160) }}

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat("css.selectors.after")}}

## 相关链接

{{ Cssxref("::before") }}, {{ cssxref("content") }}

### 高级用法

[getComputedStyle](/zh-CN/docs/Web/API/Window/getComputedStyle)

[getPropertyValue](/zh-CN/docs/Web/API/CSSStyleDeclaration/getPropertyValue)

[setProperty](/zh-CN/docs/Web/API/CSSStyleDeclaration/setProperty)
