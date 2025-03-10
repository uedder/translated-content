---
title: 配置
slug: Web/SVG/Tutorial/Positions
tags:
  - Beginner
  - Coordinate systems
  - Coordinates
  - Drawing
  - Graphics
  - NeedsBeginnerUpdate
  - SVG
  - SVG:Tutorial
translation_of: Web/SVG/Tutorial/Positions
---
{{ PreviousNext("Web/SVG/Tutorial/Getting_Started", "Web/SVG/Tutorial/Basic_Shapes") }}

この記事では、 Scalable Vector Graphics (SVG) がどのようにオブジェクトの位置や大きさを表現しているのか、座標系や、スケーラブルなコンテキストにおける「ピクセル」の測定値の意味などを紹介します。

## グリッド

![](canvas_default_grid.png)SVG はすべての要素に対して座標系または**グリッド**システムを使用しており、これは [canvas](/ja/docs/Web/API/Canvas_API) (またはその他多くのコンピュータ描画ルーチン) で使用されているものと同様です。すなわち、文書の左上隅を点 (0,0)、すなわち原点と見なします。位置は、左上からのピクセル単位で測定され、正の x 方向は右に、正の y 方向は下になります。これは、子どもの頃に教わったグラフの描き方 (Y 軸が反転している) とは少し違うことに注意してください。しかし、これは HTML の要素の配置方法と同じです (既定では、左書きの文書では同様に考えられますが、右書きの文書は X を右から左に配置します)。

#### 例:

次の要素、

```
<rect x="0" y="0" width="100" height="100" />
```

は、左上の角を起点に、そこから右と下に 100px の範囲で四角形を定義します。

### 「ピクセル」とは

最も基本的な場合においては、 SVG 文書の 1 ピクセルは出力デバイス (例えば画面) の 1 画素に対応します。しかし、この動作を変えることができないのであれば、 SVG の名称に "Scalable" が付いていなかったでしょう。 CSS のフォントサイズに絶対値と相対値があるように、 SVG でも絶対単位 ("pt" や "cm" など寸法の識別子) と、そのような識別子を持たない数値だけの、いわゆるユーザー単位があります。

特に指定しない限り、 1 ユーザー単位は 1 画面単位と同じです。明示的にこの動作を変えるための手段が SVG にあります。以下の `svg` ルート要素から始める場合:

```
<svg width="100" height="100">
```

上記の要素は、 100x100px のシンプルな SVG キャンバスを定義します。1 ユーザー単位は 1 画面単位と同じです。

```
<svg width="200" height="200" viewBox="0 0 100 100">
```

この場合、 SVG キャンバス全体の大きさは 200px×200px です。しかし `viewBox` 属性は、表示するキャンバスの部分を定義しています。これら 200x200 ピクセルの領域は、ユーザー単位 (0,0) から始まり右方向および下方向に 100x100 ユーザー単位を占める領域を表示します。これは実質的に 100x100 単位の領域をズームインし、画像を 2 倍のサイズに引き伸ばします。

現行の (単一の要素またはイメージ全体への) ユーザー単位と画面単位間のマッピングは、**ユーザー座標系** (user coordinate system) と呼ばれます。座標系から離れることで、回転・変形・反転を行うこともできます。既定のユーザー座標系は、1 ユーザーピクセルを 1 デバイスピクセルに割り当てます。(ただし、デバイスは何を 1 ピクセルとして扱うかを決めることができるかもしれません。) SVG ファイルで "in" や "cm"など 特定の寸法である長さは、結果の画像で 1:1 で見えるようにする方法で計算されます。

これを説明する SVG 1.1 の仕様を引用します。

> (前略) ユーザーエージェントは自身の環境から、"1px" を "0.2822222mm" に対応づける (すなわち 90dpi) と仮定します。すると、SVG コンテンツの処理において (中略) "1cm" は "35.43307px" (よって、35.43307 ユーザー単位) と一致します。

{{ PreviousNext("Web/SVG/Tutorial/Getting_Started", "Web/SVG/Tutorial/Basic_Shapes") }}
