---
title: 检测 CSS 动画的支持性
slug: orphaned/Web/CSS/CSS_Animations/Detecting_CSS_animation_support
original_slug: Web/CSS/CSS_Animations/Detecting_CSS_animation_support
---
{{CSSRef}}

CSS 动画 使仅用 CSS 属性来使内容呈现动画效果成为一种可能，然而，某些时候 CSS 动画属性并不能生效，此时，我们希望能够通过 javascript 代码来实现相似的动画效果。针对此种情况，本文基于 Chris Heilmann 的[博客](https://hacks.mozilla.org/2011/09/detecting-and-generating-css-animations-in-javascript/)对该技术进行了示范。

## CSS 动画支持检测

下面的代码将检测 CSS 动画的支持性是否是有效的。

```js
var animation = false,
    animationstring = 'animation',
    keyframeprefix = '',
    domPrefixes = 'Webkit Moz O ms Khtml'.split(' '),
    pfx  = '',
    elm = document.createElement('div');

if( elm.style.animationName !== undefined ) { animation = true; }

if( animation === false ) {
  for( var i = 0; i < domPrefixes.length; i++ ) {
    if( elm.style[ domPrefixes[i] + 'AnimationName' ] !== undefined ) {
      pfx = domPrefixes[ i ];
      animationstring = pfx + 'Animation';
      keyframeprefix = '-' + pfx.toLowerCase() + '-';
      animation = true;
      break;
    }
  }
}
```

首先先定义几个变量，并通过初始化 `animation` 为 false 来假设不支持 CSS 动画属性，先设置 animationstring 变量为 `animation` 并在稍后进行修改。创建一个浏览器前缀的数组用来循环遍历并设置 pfx 前缀为空字符串。

然后，检测创建的 elm 元素的 style 属性集合中 {{cssxref("animation-name")}} 属性是否被设置，如果被设置，则意味着着浏览器支持 CSS animation 属性，而不需要加任何前缀，然而到目前，还没有任何浏览器实现（译者：chrome 中试验了一下是可以的）；

如果浏览器不支持无前缀的 animation，那么 animation 变量值仍为 false，遍历所有可能的浏览器前缀，由于所有的主流浏览器现在都在该属性前加了前缀，因此在 `AnimationName` 前加上前缀即可。

当代码执行完，如果浏览器不支持 CSS animation 属性，则返回 animation 为 false，否则为 true。如果 animation 为 true，则所有 animation 相关属性名称以及 keyframes 属性前缀都是检测到的正确的，因此，如果使用 firefox，属性名称就是 MozAnimation，keyframes 前缀就是 -moz-，如果使用 chrome，属性为`WebkitAnimation` ，keyframes 前缀为 `-webkit-`。注意，浏览器是不方便在驼峰法和连字符法之间进行切换的。

## 针对不同浏览器使用正确语法实现动画效果

现在可以知道，无论浏览器是否支持 CSS animation，均可以实现动画效果。

```js
if( animation === false ) {

  // animate in JavaScript fallback

} else {
  elm.style[ animationstring ] = 'rotate 1s linear infinite';

  var keyframes = '@' + keyframeprefix + 'keyframes rotate { '+
                    'from {' + keyframeprefix + 'transform:rotate( 0deg ) }'+
                    'to {' + keyframeprefix + 'transform:rotate( 360deg ) }'+
                  '}';

  if( document.styleSheets && document.styleSheets.length ) {

      document.styleSheets[0].insertRule( keyframes, 0 );

  } else {

    var s = document.createElement( 'style' );
    s.innerHTML = keyframes;
    document.getElementsByTagName( 'head' )[ 0 ].appendChild( s );

  }

}
```

以上代码主要根据 animation 的值来进行不同的操作，如果为 false，则需要执行 javascript 脚本来实现动画效果，否则，就用 javascript 来创建所需要的 CSS animation 效果。

设置 animation 属性是很简单的，可以在 style 属性集合中简单的更新它的值。然而，增加 keyframes 是有难度的，由于它们不能够通过传统的 css 语法来定义。（虽然这样使得它们更加灵活，但是通过脚本来定义更加不易）

使用 javascript 来定义 keyframes，需要将其具体语法写为字符串。为了创建 keyframes 变量，在构建 keyframes 时要在其所有属性前加前缀，该变量包含完整的所有动画序列所需要的 keyframes 描述。

下一个任务是将创建的 keyframes 添加到实际的 CSS 中。首先要检查是否在 document 中存在 CSStylesheet，如果存在，则能够简单的将 keyframes 值插入到 CSSstylesheet 中。

如果不存在 CSSstylesheet，创建一个新的 {{HTMLElement("style")}} 元素，并将 keyframes 设置为其内容。然后将新的 {{HTMLElement("style")}} 元素插入到 document 的 head 中，从而将新的 style sheet 添加到了 html 文档中。

[在 JSFiddle 中查看](https://jsfiddle.net/codepo8/ATS2S/8/embedded/result)

## 参见

- [CSS animations](/en/CSS/CSS_animations)
