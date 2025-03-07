---
title: Firefox 78 for developers
slug: Mozilla/Firefox/Releases/78
tags:
  - '78'
  - Firefox
  - Mozilla
  - Releases
translation_of: Mozilla/Firefox/Releases/78
---
{{FirefoxSidebar}}

このページでは、開発者に影響する Firefox 78 の変更点をまとめています。Firefox 78 は、[2020 年 6 月 30 日](https://wiki.mozilla.org/RapidRelease/Calendar#Future_branch_dates/docs/) にリリースされました。

Mozilla hacks の記事「[New in Firefox 78: DevTools improvements, new regex engine, and abundant web platform updates](https://hacks.mozilla.org/2020/06/new-in-firefox-78/)」もご覧ください。

## ウェブ開発者向けの変更点一覧

### 開発者ツール

#### デバッガー

- [about:debugging](/ja/docs/Tools/about:debugging#Connecting_to_a_remote_device) パネルで、リモート端末がアクセスする URL を変更できるようになりました ({{bug("1617237")}})。
- [デバッガー](/ja/docs/Tools/Debugger/UI_Tour) のメニュー項目 "**JavaScript を無効化**" が現在のタブにのみ作用するようになりました。また、開発ツールを閉じるとリセットされるようになりました ({{bug("1640318")}})。
- [スコープペイン](/ja/docs/Tools/Debugger/UI_Tour#Scopes) で **マッピング** を有効にすると、[ログポイント](/ja/docs/Tools/Debugger/Set_a_logpoint) でソースマップを適用したコードの変数名と元の変数名をマッピングできます ({{bug("1536857")}})。

#### ネットワークモニター

- [ネットワークモニター](/ja/docs/Tools/Network_Monitor/request_list#Network_request_columns) で、要求リストの表の列の境界をどこでもドラッグして、リサイズできるようになりました ({{bug("1618409")}})。
- ネットワークモニターの [要求の詳細パネル](/ja/docs/Tools/Network_Monitor/request_details) の UX を改良しました ({{bug("1631302")}}, {{bug("1631295")}})。
- 要求がブロックされたとき、[要求リスト](/ja/docs/Tools/Network_Monitor/request_list) でアドオン、CSP、CORS、強化型トラッキング防止などの理由を表示するようになりました ({{bug("1555057")}}, {{bug("1445637")}}, {{bug("1556451")}})。

#### その他のツール

- [アクセシビリティ](/ja/docs/Tools/Accessibility_inspector) インスペクターがベータ版から脱しました。このツールを使用して、サイトのさまざまなアクセシビリティの問題を確認できます ({{bug("1602075")}})。
- キャッチされていない promise エラーについて、名前やスタックを含む詳細情報をコンソールに表示するようになりました ({{bug("1636590")}})。

### CSS

- {{CSSxRef(":is", ":is()")}} および {{CSSxRef(":where", ":where()")}} 疑似クラスをデフォルトで有効にしました ({{bug(1632646)}})。
- {{CSSxRef(":read-only")}} および {{CSSxRef(":read-write")}} 疑似クラスを、接頭辞なしでサポートしました ({{bug(312971)}})。

  - また `:read-write` のスタイルが、無効化した [`<input>`](/ja/docs/Web/HTML/Element/input) および [`<textarea>`](/ja/docs/Web/HTML/Element/textarea) 要素に適用されないようになりました。これは [HTML 仕様書](https://html.spec.whatwg.org/#selector-read-write) に違反していました ({{bug(888884)}})。

### JavaScript

- [`Intl.ListFormat`](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/ListFormat) API をサポートしました ({{bug(1589095)}})。
- [`Intl.NumberFormat()`](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat) コンストラクターを、[Intl.NumberFormat Unified API Proposal](https://github.com/tc39/proposal-unified-intl-numberformat) で定義された新しいオプションをサポートするように拡張しました ({{bug(1633836)}})。特に、以下のようなものがあります:

  - [指数表記のサポート](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat#Scientific_engineering_or_compact_notations)
  - [単位](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat#Unit_formatting)、[通貨](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat#Currency_formatting)、[符号表示](/ja/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat/NumberFormat#Displaying_signs) の整形

- {{JSxRef("RegExp")}} エンジンを [更新](https://hacks.mozilla.org/2020/06/a-new-regexp-engine-in-spidermonkey/) して、ECMAScript 2018 で導入したすべての新機能をサポートしました:

  - [後読み言明](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Assertions) ({{bug(1225665)}})
  - {{JSxRef("RegExp.prototype.dotAll")}} ({{bug(1361856)}})
  - [Unicode property escapes](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes) ({{bug(1361876)}})
  - [名前付きキャプチャグループ](/ja/docs/Web/JavaScript/Guide/Regular_Expressions/Groups_and_Ranges) ({{bug(1362154)}})

- 2020 年中頃の [WebIDL 仕様書の変更](https://github.com/heycam/webidl/pull/357) により、[`Symbol.toStringTag` プロパティをすべての DOM プロトタイプオブジェクトに追加しました](/ja/docs/Web/JavaScript/Reference/Global_Objects/Symbol/toStringTag#toStringTag_available_on_all_DOM_prototype_objects) ({{bug(1277799)}})。
- {{jsxref("WeakMap")}} オブジェクトのガベージコレクションを改良しました。`WeakMaps` を徐々にマークするようになりました ({{bug(1167452)}})。

### API

#### DOM

- {{DOMxRef("ParentNode.replaceChildren()")}} メソッドを実装しました ({{bug(1626015)}})。

#### Service workers

- [Extended Support Releases (ESR)](https://www.mozilla.org/firefox/organizations/): Firefox 78 は [Service workers](/ja/docs/Web/API/Service_Worker_API) (および [Push API](/ja/docs/Web/API/Push_API)) をサポートする最初の ESR リリースです。過去の ESR リリースはサポートしていませんでした ({{bug(1547023)}})。

### WebAssembly

- [Wasm Multi-value](https://hacks.mozilla.org/2019/11/multi-value-all-the-wasm/) をサポートしました。WebAssembly の関数が複数の値を返したり、命令シーケンスが複数のスタックの値を使用および生成したりすることが可能になりました ({{bug(1628321)}})。
- WebAssembly で、[`BigInt`](/ja/docs/Web/JavaScript/Reference/Global_Objects/BigInt) を使用して JavaScript から 64-bit 整数の関数パラメーター (i64) をインポートおよびエクスポートできるようになりました ({{bug(1608770)}})。

### TLS 1.0 および 1.1 の廃止

- [Transport Layer Security](/ja/docs/Web/Security/Transport_Layer_Security) (TLS) プロトコルのバージョン 1.0 および 1.1 のサポートを、すべてのブラウザーで廃止しました。以前の告知と、影響を受ける場合の対処について、[TLS 1.0 and 1.1 Removal Update](https://hacks.mozilla.org/2019/05/tls-1-0-and-1-1-removal-update/) をご覧ください ({{bug(1643229)}})。

## アドオン開発者向けの変更点

- {{WebExtAPIRef("browsingData.removeCache")}} および {{WebExtAPIRef("browsingData.removePluginData")}} が、ホスト名による削除をサポートしました ({{bug(1636784)}})。
- [`proxy.onRequest`](/ja/docs/Mozilla/Add-ons/WebExtensions/API/proxy/onRequest) を使用するとき、タブやウィンドウの ID に基づいて制限するフィルターが正しく適用されるようになりました。これは、プロキシの機能をひとつのウィンドウだけに提供したいアドオンで役に立つでしょう。
- "すべてのタブ" ドロップダウンから [コンテキストメニューでクリックするとき](/ja/docs/Mozilla/Add-ons/WebExtensions/API/menus/onClicked)、適切なタブオブジェクトが渡されるようになりました。以前は、誤ってアクティブなタブが渡されていました。
- [`downloads.download`](/ja/docs/Mozilla/Add-ons/WebExtensions/API/downloads/download) に saveAs オプションをつけて使用したとき、最近使用したディレクトリーを記憶するようになりました。この情報は開発者が使用できませんでしたが、ユーザーにはとても便利でした。

## 過去のバージョン

{{Firefox_for_developers(77)}}
