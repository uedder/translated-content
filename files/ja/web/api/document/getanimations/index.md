---
title: Document.getAnimations()
slug: Web/API/Document/getAnimations
tags:
  - API
  - Animation
  - CSS
  - CSS Animations
  - CSS Transitions
  - Document
  - Experimental
  - Method
  - Reference
  - Transitions
  - Web Animations
  - getAnimations
  - waapi
  - web animations api
translation_of: Web/API/DocumentOrShadowRoot/getAnimations
original_slug: Web/API/DocumentOrShadowRoot/getAnimations
---
{{ SeeCompatTable() }}{{APIRef("Web Animations")}}

`getAnimations()` メソッドは {{domxref("Document")}} インターフェイスのメソッドで、この文書の配下にあるターゲット要素にあるすべての {{domxref("Animation")}} オブジェクトの配列を返します。この配列には [CSS アニメーション](/ja/docs/Web/CSS/CSS_Animations), [CSS トランジション](/ja/docs/Web/CSS/CSS_Transitions), [ウェブアニメーション](/ja/docs/Web/API/Web_Animations_API) が含まれます。

## 構文

```
var allAnimations = Document.getAnimations();
```

### 引数

なし。

### 返値

{{domxref("Animation")}} オブジェクトの {{jsxref("Array")}} で、それぞれの要素は呼び出された {{domxref("Document")}} の配下にある要素に現在関連付けられているアニメーション 1 つを表します。

## 例

次のコードスニペットは、ページ上のすべてのアニメーションの {{domxref("Animation.playbackRate")}} を半分にすることで速度をゆっくりにします。

```js
document.getAnimations().forEach(
  function (animation) {
    animation.playbackRate *= .5;
  }
);
```

## 仕様書

| 仕様書                                                                                                                                   | 状態                                 | 備考 |
| ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | ---- |
| {{SpecName('Web Animations', '#dom-documentorshadowroot-getanimations', 'document.getAnimations()' )}} | {{Spec2('Web Animations')}} |      |

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [ウェブアニメーション API](/ja/docs/Web/API/Web_Animations_API)
- [CSS アニメーション](/ja/docs/Web/CSS/CSS_Animations)
- [CSS トランジション](/ja/docs/Web/CSS/CSS_Transitions)
- {{domxref("Element.getAnimations()")}} - 単一の要素 ({{domxref("Element")}}) とその子孫にあるアニメーションのみを読み取る
- {{domxref("Animation")}}
