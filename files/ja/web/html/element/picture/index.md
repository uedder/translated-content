---
title: '<picture>: 画像要素'
slug: Web/HTML/Element/picture
tags:
  - Element
  - Graphics
  - HTML
  - HTML embedded content
  - Images
  - Reference
  - Web
  - WebP
  - picture
translation_of: Web/HTML/Element/picture
---
{{HTMLRef}}

**HTML の `<picture>` 要素**は、0 個以上の {{HTMLElement("source")}} 要素と一つの {{HTMLElement("img")}} 要素を含み、様々な画面や端末の条件に応じた画像を提供します。

ブラウザーは複数の `<source>` 子要素を検討し、その中から最も適切なものを選択します。適切なものがない場合や、ブラウザーが `<picture>` 要素に対応してない場合、 `<img>` 要素の {{htmlattrxref("src", "img")}} 属性で指定された URL が選択されます。選択された画像は `<img>` 要素が占有する領域に表示されます。

{{EmbedInteractiveExample("pages/tabbed/picture.html", "tabbed-standard")}}

どの URL を読み込むかを選択するには、{{Glossary("user agent","ユーザーエージェント")}}はそれぞれの `<source>` 要素の {{htmlattrxref("srcset", "source")}}, {{htmlattrxref("media", "source")}}, {{htmlattrxref("type", "source")}} 属性を調べて、現在のページのレイアウトや表示機器の能力に最も合う画像を検討します。

`<img>` 要素は 2 つの役割を担います。

1.  画像の寸法やその他の属性を記述します。
2.  `<source>` 要素で利用可能な画像を提供できなかった場合の代替策を提供します。

`<picture>` をよく使う場面は以下の通りです。

- **アートディレクション** 様々な `media` の条件に合わせて画像を切り抜いたり変更したりする (例えば、小さな画面では、詳細すぎない、より簡単な版の画像を読み込むなど)。
- 特定の形式に対応していないブラウザーに対して、**代替画像形式を提供する**。
- 見る人の画面に最も適合する画像を読み込むことで、**通信帯域を節約しページの読み込みをより速くする**。

DPI の高い (高解像度の) ディスプレイのために高解像度版の画像を提供する場合は、代わりに {{htmlattrxref("srcset", "img")}} 属性を `<img>` に使用してください。これによってブラウザーはデータ節約モードでは低解像度版を選択することができ、 `media` 条件を明示的に書かなくてもよくなります。

<table class="properties">
  <tbody>
    <tr>
      <th scope="row">
        <a href="/ja/docs/Web/HTML/Content_categories">コンテンツカテゴリ</a>
      </th>
      <td>
        <a href="/ja/docs/Web/HTML/Content_categories#フローコンテンツ"
          >フローコンテンツ</a
        >, 記述コンテンツ, 埋め込みコンテンツ
      </td>
    </tr>
    <tr>
      <th scope="row">許可されている内容</th>
      <td>
        0個以上の {{HTMLElement("source")}} 要素、その後に1個の
        {{HTMLElement("img")}} 要素、任意でスクリプト対応要素と混在。
      </td>
    </tr>
    <tr>
      <th scope="row">タグの省略</th>
      <td>{{no_tag_omission}}</td>
    </tr>
    <tr>
      <th scope="row">許可されている親要素</th>
      <td>埋め込みコンテンツを含むことができるすべての要素。</td>
    </tr>
    <tr>
      <th scope="row">暗黙の ARIA ロール</th>
      <td>
        <a href="https://www.w3.org/TR/html-aria/#dfn-no-corresponding-role"
          >対応するロールなし</a
        >
      </td>
    </tr>
    <tr>
      <th scope="row">許可されている ARIA ロール</th>
      <td>許可されている <code>role</code> なし</td>
    </tr>
    <tr>
      <th scope="row">DOM インターフェイス</th>
      <td>{{domxref("HTMLPictureElement")}}</td>
    </tr>
  </tbody>
</table>

## 属性

この要素は[グローバル属性](/ja/docs/Web/HTML/Global_attributes)のみを持ちます。

## 使用上のメモ

{{cssxref("object-position")}} プロパティを使用して、要素の枠内で画像の位置を調整したり、 {{cssxref("object-fit")}} プロパティを使用して、枠内に合わせるための画像の寸法を変更する方法を制御したりすることができます。

> **Note:** これらのプロパティは子の `<img>` 要素に用い、 `<picture>` 要素には**用いない**でください。

## 例

これらの例は、 {{HTMLElement("source")}} 要素の様々な属性がどのように `<picture>` 内の画像の選択を変更するかを示しています。

### media 属性

`media` 属性はユーザーエージェントがそれぞれの {{HTMLElement("source")}} 要素を評価するメディア条件を (メディアクエリと同様に) 指定します。

メディア条件が `false` と評価された場合、 {{HTMLElement("source")}} 要素はスキップされ、 `<picture>` 内の次の要素が評価されます。

```html
<picture>
  <source srcset="mdn-logo-wide.png" media="(min-width: 600px)">
  <img src="mdn-logo-narrow.png" alt="MDN">
</picture>
```

### srcset 属性

[{{htmlattrdef("srcset")}}](/ja/docs/Web/HTML/Element/source#attr-srcset) 属性は、*寸法に基づいた*利用可能な画像のリストを提供するために使用します。

これは画像記述子のカンマ区切りのリストで構成されます。それぞれの画像記述子は画像の URL と、次の*いずれか*で構成されます。

- _幅記述子_ は `w` に続けて書きます (`300w` など)
  _または_
- _ピクセル密度記述子_ は `x` に続けて書き (`2x` など)、高 DPI 画面の高解像度画像を提供します。

```html
<picture>
  <source srcset="logo-768.png 768w, logo-768-1.5x.png 1.5x">
  <source srcset="logo-480.png, logo-480-2x.png 2x">
  <img src="logo-320.png" alt="logo">
</picture>
```

### type 属性

`type` 属性は、 {{HTMLElement("source")}} 要素の `srcset` 属性で与えられるリソース URL の [MIME タイプ](/ja/docs/Web/HTTP/Basics_of_HTTP/MIME_types)を指定します。ユーザーエージェントが指定されたタイプに対応していない場合、その {{HTMLElement("source")}} 要素はスキップされます。

```html
<picture>
  <source srcset="logo.webp" type="image/webp">
  <img src="logo.png" alt="logo">
</picture>
```

## 仕様書

| 仕様書                                                                                                                   | 状態                             | 備考     |
| ------------------------------------------------------------------------------------------------------------------------ | -------------------------------- | -------- |
| {{SpecName('HTML WHATWG', 'embedded-content.html#the-picture-element', '&lt;picture&gt;')}} | {{Spec2('HTML WHATWG')}} | 初回定義 |

## ブラウザーの互換性

{{Compat("html.elements.picture")}}

## 関連情報

- {{HTMLElement("img")}} 要素
- {{HTMLElement("source")}} 要素
- フレーム内の画像の位置や寸法の設定: {{cssxref("object-position")}} 及び {{cssxref("object-fit")}}
- [画像ファイルの Image file type and format guide](/ja/docs/Web/Media/Formats/Image_types)
