## Webスクレイピング・ワークフロー
**Webスクレイピング**とは、Webページなどから情報を取得すること。

    ### ワークフロー
    1. GASを用いて、Webページから情報を取得する。
    2. スプレッドシートに取得した情報を反映させる。

    ### 必要な知識
    1. 外部ライブラリを読み込む方法(簡単に作業が出来る。)
    2. Webスクレイピングを行う方法

##　外部ライブラリを読み込む
1. GAS内のリソースからライブラリを選択
2. 外部ライブラリ(M1lugvAXKKtUxn_vdAG9JZleS6DrsjUUV)をペーストし保存

## 入手したい情報を取得してくる
入手したい情報(今回ならば受講者数とレビュー数)を取得する。

```gas:gas
function scraping() {
  var url = 'https://scraping-for-beginner.herokuapp.com/udemy';
  var response = UrlFetchApp.fetch(url);
  var content = response.getContentText('UTF-8');
  
  var parser = Parser.data(content);
  
  var subscribers = parser.from('<p class="subscribers">').to('</p>').build();
  subscribers = Number(subscribers.split(':')[1]);
  
  var reviews = parser.from('<p class="reviews">').to('</p>').build();
  reviews = Number(reviews.split(':')[1]); 
  
  var today = new Date();
  return[today, subscribers, reviews];
}
```

## シートに書き込む

シートとGASを連携させ、`sheet.getEange`で情報を書き込む。

```gas:gas
function writeData(){
  var results = scraping();
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheetByName('データ');
  
  var lastRow = sheet.getLastRow();
  sheet.getRange(lastRow+1, 1, 1, 3).setValues([results]);
}
```