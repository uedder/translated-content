---
title: Storage.clear()
slug: Web/API/Storage/clear
tags:
  - API
  - Method
  - Reference
  - Storage
  - Web Storage
translation_of: Web/API/Storage/clear
---
{{APIRef("Web Storage API")}}

**`clear()`** は {{domxref("Storage")}} インターフェイスのメソッドで、指定された `Storage` オブジェクトに格納されているすべてのキーを消去します。

## 構文

```
storage.clear();
```

### 返値

{{jsxref("undefined")}} です。

## 例

以下の関数はローカルストレージに 3 個のデータアイテムを作成して、 `clear()` を使用してすべて削除します。

```js
function populateStorage() {
  localStorage.setItem('bgcolor', 'red');
  localStorage.setItem('font', 'Helvetica');
  localStorage.setItem('image', 'miGato.png');

  localStorage.clear();
}
```

> **Note:** **注**: 実際の例としては、 [Web Storage Demo](https://mdn.github.io/dom-examples/web-storage/) をご覧ください。

## 仕様書

| 仕様書                                                                                                       | 状態                             | 備考 |
| ------------------------------------------------------------------------------------------------------------ | -------------------------------- | ---- |
| {{SpecName('HTML WHATWG', 'webstorage.html#dom-storage-clear', 'Storage.clear')}} | {{Spec2('HTML WHATWG')}} |      |

## ブラウザーの互換性

{{Compat("api.Storage.clear")}}

## 関連情報

[Web Storage API の使用](/ja/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)
