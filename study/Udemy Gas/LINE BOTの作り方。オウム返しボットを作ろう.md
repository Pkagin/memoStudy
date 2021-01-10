## LINEオウム返しBOTとは・フローチャート

###　LINEオウム返しBOT
LINEBOTに文章を送ると送った文章がそのまま返信されるBOTのこと。
例）Botに「ハロー」と打つと、「ハロー」と返信が返ってくる。

### フローチャート
1.  **LINE Developers**でチャンネル登録
2.  GASとLINEを連携（オウム返しボット）

## LINE Developersへの登録
1.  https://developers.line.biz/en/
    上のサイトに自分のLINEアカウントでログインする。
2.  新しくプロバイダーを作成し、チャンネルの種類をMessaging　APIにする。
3.  チャンネルの基本設定を行う。必要事項などを記入する。
4.  Messaging APIをおすと、QRコードが表示されているので、そこから友達追加を行う。
5.  今回はオウム返しボットを作るので、応答設定で応答メッセージをオフにする。Webhookはオンにする。
6.  チャンネルアクセストークンを発行する。

## google apps scriptとLINEを連携（オウム返しボット）

### オウム返しボットのプログラム
オウム返しボットは以下参照。アクセストークンには、LINE　Developersで作成したチャンネルのトークンを張り付ける。

```js
var CHANNEL_ACCESS_TOKEN = 'アクセストークン';

function doPost(e) {
  var replytoken= JSON.parse(e.postData.contents).events[0].replyToken;
  if (typeof replytoken === 'undefined') {
    return;
  }
  var user_message = JSON.parse(e.postData.contents).events[0].message.text;

  var url = 'https://api.line.me/v2/bot/message/reply';
  UrlFetchApp.fetch(url, {
    'headers': {
      'Content-Type': 'application/json; charset=UTF-8',
      'Authorization': 'Bearer ' + CHANNEL_ACCESS_TOKEN,
    },
    'method': 'post',
    'payload': JSON.stringify({
      'replyToken': replytoken,
      'messages': [{
        'type': 'text',
        'text': user_message,
      }],
    }),
  });
  return ContentService.createTextOutput(JSON.stringify({'content': 'post ok'})).setMimeType(ContentService.MimeType.JSON);
```

### Webhook設定
1.  GASの公開のウェブアプリケーションとして導入をクリックし、不特定多数に人が見れるように設定し許可する。
2.  発行されたURLをLINE DevelopersのWebhook設定のURLの部分に張り付け、Webhookの利用を許可する。
3.  これでボットにメッセージを送るとその文章がそのまま返ってくる。


