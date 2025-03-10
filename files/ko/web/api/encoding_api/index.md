---
title: 인코딩 API
slug: Web/API/Encoding_API
tags:
  - API
  - 개요
  - 레퍼런스
  - 인코딩
translation_of: Web/API/Encoding_API
---
{{DefaultAPISidebar("Encoding API")}}{{SeeCompatTable}}

**인코딩 API**는 {{Glossary("문자 인코딩", "character encodings")}}, {{Glossary("UTF-8")}}이 아닌 레거시 인코딩을 포함한 다양한 문자열을 제어할 수 있는 매커니즘을 제공한다.

인코딩 API는 4가지 인터페이스를 제공한다. {{domxref("TextDecoder")}}, {{domxref("TextEncoder")}}, {{domxref("TextDecoderStream")}}, {{domxref("TextEncoderStream")}} 등 이다.

## Interfaces

<div class="index"><ul><li>{{DOMxRef("TextDecoder")}}</li><li>{{DOMxRef("TextEncoder")}}</li><li>{{DOMxRef("TextDecoderStream")}}</li><li>{{DOMxRef("TextEncoderStream")}}</li></ul></div>

## Tutorials & tools

- A [shim](http://code.google.com/p/stringencoding/) allowing to use this interface in browsers that don't support it.
- [`StringView`](/en-US/Add-ons/Code_snippets/StringView "/en-US/docs/Web/JavaScript/Typed_arrays/StringView") – a C-like representation of strings based on typed arrays.

## Specifications

{{Specifications}}

## Browser compatibility

### `TextDecoder`

{{Compat("api.TextDecoder")}}

### `TextEncoder`

{{Compat}}
