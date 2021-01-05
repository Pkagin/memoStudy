## ワークフロー・必要な知識
### ワークフロー
    ・Gmailから特定の情報に当てはまるような情報を取得する
    ・取得した情報をスプレッドシートに反映させる

### 必要な知識
    ・メール情報を取得する方法
    ・スプレッドシートに情報を書き込む方法

## メールを取得する
    ・問合せのメールを取得するという条件のもとでメールを取得していく。
    ・https://support.google.com/mail/answer/7190?hl=ja
    　上のページでGmailで使用できる検索演算子を見つけることが出来る。
    ・Gmailのメールを検索というところから、件名で[問合せ]と条件を指定することもできる。
    ・一回の抽出で取得できる情報は500個まで。
    ・GASに以下のようにコードを書くことでメールを取得することが出来る。
    
    ```gas:gas
        function getMessage() {
    var condition = 'subject:([問合せ])';
    var start = 0;
    var max = 500;
    var threads = GmailApp.search(condition, start, max);
    var messages = GmailApp.getMessagesForThreads(threads);
  
    }
    ```

## メールの必要な情報を取得する
    ・`getPlainBody`でメールの内容を取得することが出来る。
    ・取得したい情報(日にちや名前、メールアドレスなど)を以下のように取得することが出来る。
    ・`split`は文字列を分割、区切ることが出来、今回は取得したい情報の最初と最後を区切って情報を取得している。

```gas:gas
    var body = messages[0][0].getPlainBody();
    var date = messages[0][0].getDate();
    var name = body.split('お名前:')[1].split(' 様')[0];
    var email = body.split('メールアドレス')[1].split('\n')[0];
    var title = body.split('お問い合わせタイトル')[1].split('\n')[0];
    var content = body.split('お問い合わせ内容')[1].split('- - - - - - - -')[0];
```

## 1つのメールをシートに書き込む
    ・`SpreadsheetApp.getActiveSpreadsheet();`と`ss.　getSheetByName('シート名');`でスプレッドシートを取得する
    ・`sheet.getRange(何行目から, 何列目から, 何行、何列目まで). setValues([data])`と書くことでスプレッドシートに指定した範囲で情報を書き込むことが出来る。`setValues([data]`で配列を二次元配列にできる。

    ```gas:gas  
    var ss = SpreadsheetApp.getActiveSpreadsheet();
    var sheet = ss.getSheetByName('メール一覧');
    
    var data = [date, name, email, title, content];

    var firstRow = 2;
    sheet.getRange(firstRow, 1, 1,data.length).setValues([data]);
    ```

## 全てのメールをシートに書き込む
    ・`forEach()`を使うことで全てのメールの情報をスプレッドシートに書き込む事が出来る。

    ```gas:gas
    messages.forEach(function(message)){
        var body = message[0].getPlainbody();
  
        var date = message[0].getdate();
        var name = body.split('お名前:')[1].split(' 様')[0];
        var email = body.split('メールアドレス')[1].split('\n')[0];
        var title = body.split('お問い合わせタイトル')[1].split('\n')[0];
        var content = body.split('お問い合わせ内容')[1].split('- - - - - - - -')[0];
  
        var data = [date, name, email, title, content];

        sheet.getRange(firstRow, 1, 1,data.length).setValues([data]);

        firstRow++;
    });
    ```