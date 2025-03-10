---
title: PushManager.getSubscription()
slug: Web/API/PushManager/getSubscription
tags:
  - API
  - Experimental
  - Method
  - PushManager
  - Reference
  - Service Workers
translation_of: Web/API/PushManager/getSubscription
---
{{SeeCompatTable}}{{ApiRef("Push API")}}

{{domxref("PushManager")}} インターフェースの **`PushManager.getSubscription()`** メソッドは、既存のプッシュサブスクリプションを取得します。

これは既存のプッシュサブスクリプションの詳細を含む {{domxref("PushSubscription")}} を解決する {{jsxref("Promise")}} を返します。既存のプッシュサブスクリプションが存在しない場合 `null` 値で解決されます。

## 構文

```js
​PushManager.getSubscription().then(function(pushSubscription) { ... } );
```

### パラメーター

なし。

### 戻り値

{{domxref("PushSubscription")}} オブジェクトで解決される {{jsxref("Promise")}}。

## 例

このコードスニペットは、[push messaging and notification sample ](https://github.com/GoogleChrome/samples/blob/gh-pages/push-messaging-and-notifications)から取ってきました（使用できるライブデモはありません）。

```js
// サブスクリプションをチェックするために、service worker の登録が必要である。
  navigator.serviceWorker.ready.then(function(serviceWorkerRegistration) {
    // 既にプッシュメッセージサブスクリプションがあるか？
    serviceWorkerRegistration.pushManager.getSubscription()
      .then(function(subscription) {
        // プッシュメッセージからサブスクライブ ／ アンサブスクライブ
        // する任意の UI を有効にする
        var pushButton = document.querySelector('.js-push-button');
        pushButton.disabled = false;

        if (!subscription) {
          // プッシュを購読していない場合、ユーザーがプッシュできるように
          // UI を設定する。
          return;
        }

        // 最新の subscriptionId でサーバ同期を維持する。
        sendSubscriptionToServer(subscription);

        showCurlCommand(subscription);

        // プッシュメッセージの購読を表示するために
        // UI を設定する。
        pushButton.textContent = 'Disable Push Messages';
        isPushEnabled = true;
      })
      .catch(function(err) {
        window.Demo.debug.log('Error during getSubscription()', err);
      });
  });
}
```

## 仕様

| 仕様                                                                                                                                             | 状態                         | コメント   |
| ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------- | ---------- |
| {{SpecName('Push API', '#widl-PushManager-getSubscription-Promise-PushSubscription', 'getSubscription()')}} | {{Spec2('Push API')}} | 初期定義。 |

## ブラウザ実装状況

{{Compat("api.PushManager.getSubscription")}}

## 関連項目

- [Using the Push API](/ja/docs/Web/API/Push_API/Using_the_Push_API)
