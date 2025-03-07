---
title: モバイルとデスクトップで別々のサイト
slug: conflicting/Web/Progressive_web_apps
tags:
  - Mobile
  - Web Development
translation_of: Web/Guide/Mobile/Separate_sites
original_slug: Web/Guide/Mobile/Separate_sites
---

モバイルウェブ開発への「別々のサイト」アプローチは、モバイルウェブユーザーとデスクトップウェブユーザーのために異なるサイトを作成することを含みます。このアプローチにはプラス面とマイナス面があります。

## 長所

この最初の選択肢はこれまでで最も人気があります — [ユーザーエージェント検出](https://ja.wikipedia.org/wiki/ユーザーエージェント#ユーザーエージェント・スニッフィング)を使用して、携帯電話のユーザーを別のモバイルサイト（典型的には m.example.com）に転送する方法です。一言で言えば、このテクニックではサーバー側のロジックを使用して[モバイルウェブ開発の 3 つの目標](http://blog.mozilla.com/webdev/2011/05/04/approaches-to-mobile-web-development-part-1-what-is-mobile-friendliness/)（英語）すべてを一度に解決します — ユーザーのブラウザーが携帯電話のように見える場合は、携帯電話用にフォーマットされ、速度が最適化されたモバイルコンテンツを配信します。

概念的には単純ですが、特にテンプレートをサポートする CMS またはウェブアプリケーションを使用している場合は、これが既存のサイトに追加する最も簡単な選択肢です。モバイルユーザーにはモバイル固有のコンテンツ、スタイル、およびスクリプトのみが送信されるため、この方法では、ここに示されている他の選択肢のどれよりも最高のパフォーマンスが得られます。最終的に、デスクトップとモバイルでまったく異なるユーザーエクスペリエンスを実現できます — 結局のところ、それらは 2 つの異なるサイトです！

## 短所

残念ながら、このアプローチは欠点がないわけではありません。手始めに、モバイルユーザーに公開したいサイトの各ページに対して 2 つの異なるページを管理しています。CMS を使用している場合は、この重複を最小限に抑えるようにサイトのテンプレートを配置することが可能です。ただし、モバイルとデスクトップでテンプレートに違いがあるときはいつでも、コードには複雑な原因がひそんでいます。同様に、2 セットのフロントエンドロジックをコーディングする必要があるため、これにより新しいサイト機能の実装時間が長くなります。

ただし、それよりもさらに重要なのは、ユーザーエージェントの検出には[本質的に欠陥があり](http://css-tricks.com/browser-detection-is-bad/)（英語）、将来を見据えたものではないという事実です。新しいブラウザーが登場するたびに、それに対応するようにアルゴリズムを調整する必要があります。そして誤検知は特に怖いです — モバイルサイトを誤ってデスクトップユーザーに配信すると当惑させるかもしれません。

## この選択肢を選ぶのが正しいとき

![sumo_screenshot.png](sumo_screenshot.png)まず、対象視聴者に古いかローエンドの[フィーチャーフォン](http://www.cnet.com/8301-17918_1-10461614-85.html)（英語）のユーザーが含まれている場合は、この戦略を[ある程度](http://www.passani.it/gap/#adaptation)（英語）採用する必要があるかもしれません。これは、一部のフィーチャーフォンのデフォルトブラウザーは、デスクトップを対象としたウェブサイトと同じマークアップをサポートしておらず、代わりに [XHTML-MP](http://ja.wikipedia.org/wiki/XHTML_Mobile_Profile) や古い [WML](http://ja.wikipedia.org/wiki/Wireless_Markup_Language) などの形式を理解するためです。

この要因はさておき、この戦略が他の方法よりも本当に優れているケースが 1 つあります。モバイルデバイスでユーザーに提供したい機能がデスクトップのそれとは極端に異なる場合は、別々のサイトを使用するのが[最も実用的な選択](http://tripleodeon.com/2010/10/not-a-mobile-web-merely-a-320px-wide-one)（英語）になる可能性があります。これは、完全に完全に別々の HTML、JavaScript、CSS を携帯電話と PC に送信するという選択肢があるからです。

このアプローチを使用することを余儀なくされるもう 1 つのケースは、何らかの理由で既存のデスクトップサイトを変更できず、100% 別のモバイルサイトを必要とする場合です。理想的ではありませんが、少なくともこの選択肢があります。

## 例

[Facebook](http://m.facebook.com/)、[YouTube](http://m.youtube.com/)、[Digg](http://m.digg.com/ "Mobile Digg")、[Flickr](http://m.flickr.com/ "Mobile Flickr") など、あなたが実際に目にする主要なウェブアプリケーションのほとんどがこの方法を選択しています。実際、Mozilla はモバイル版の [addons.mozilla.org](https://addons.mozilla.org/)（AMO）と [support.mozilla.org](http://support.mozilla.com/)（SUMO）にこの戦略を選択しました。このアプローチの例の背後にあるソースコードを実際に見たい場合は、[AMO](https://github.com/jbalogh/zamboni/) または [SUMO](https://github.com/jsocol/kitsune)（リンク切れ）の github リポジトリをチェックしてください。

## モバイルウェブ開発へのアプローチ

モバイルプラットフォーム向けに開発するための背景やその他のアプローチについては、以下の記事を参照してください。

- [モバイルの親しみやすさとは？](/ja/docs/Web/Guide/Mobile/Mobile-friendliness)
- [レスポンシブデザイン](/ja/docs/Web_Development/Mobile/Responsive_design)
- [ハイブリッドアプローチ](/ja/docs/Web/Guide/Mobile/A_hybrid_approach)

### 原本情報

この記事は、もともと 2011 年 5 月 13 日に Mozilla Webdev ブログで「[モバイルウェブ開発へのアプローチ 第 2 部 - 別々のサイト](http://blog.mozilla.com/webdev/2011/05/13/approaches-to-mobile-web-development-part-2-separate-sites/)」として Jason Grlicky によって公開されました。（英語）
