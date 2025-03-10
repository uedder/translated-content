---
title: Range.intersectsNode()
slug: Web/API/Range/intersectsNode
page-type: web-api-instance-method
tags:
  - API
  - DOM
  - Experimental
  - Method
  - Range
  - Reference
browser-compat: api.Range.intersectsNode
translation_of: Web/API/Range/intersectsNode
---
{{ApiRef("DOM")}} {{SeeCompatTable}}

**`Range.intersectsNode()`** メソッドは、指定された {{domxref("Node")}} が {{domxref("Range")}} と交差しているかどうかを示す論理値を返します。

## 構文

```js
intersectsNode( referenceNode )
```

### 引数

- `referenceNode`
  - : この {{domxref("Range")}} と比較する {{domxref("Node")}} です。

### 返値

論理値です。

## 例

```js
const range = document.createRange();

range.selectNode(document.getElementsByTagName("div").item(0));
const intersectingNode = range.intersectsNode(document.getElementsByTagName("p").item(0));
```

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [DOM インターフェイスの索引](/ja/docs/Web/API/Document_Object_Model)
