# GAS(GoogleAppsScript)とLINE Notifyを使ってタスクを自動通知
GASとLINE Notifyを使ってタスクの状況を自動でLINE通知するようにしました。

#　準備
以下の三つを使えるように準備します。
・GAS(GoogleAppsScript)
・スプレッドシート
・LINE Notify

LINE Notifyは[ここから](https://notify-bot.line.me/ja/)ログインし、アクセストークンを発効します。

# コード
以下は今回のコードです。

```コード.gs
//確認待ちの通知
function checkTaskAddStatus(){
  var lastRow = SHEET_TASK.getLastRow();
    for(i=1; i<lastRow+1 ; i++){
      var TaskStatus = SHEET_TASK.getRange(i, 4).getValue();
      if(TaskStatus === "確認待ち"){
        var taskDetail = SHEET_TASK.getRange(i, 3).getValue();
        var message = "[タスク確認待ち通知]\n・タスク内容:" + taskDetail + "\n・進捗状況:" + TaskStatus;
        SendToLine(message);   
    }
```

```setting.gs
const NOTIFY_TOKEN = "アクセストークン";
//タスクシート
const SPREAD_SHEET_TASK = SpreadsheetApp.openById('シートid');
//const URl = "シートのURL";
const SHEET_TASK =  SPREAD_SHEET_TASK.getSheetByName("タスク状況");
```

```notify.gs
//LINEに通知
function SendToLine(message){
    var token = [NOTIFY_TOKEN];
    var options = {
      "method": "post",
      "payload" : {"message": message },
      "headers": {"Authorization": "Bearer " + token}    
    };
    UrlFetchApp.fetch("https://notify-api.line.me/api/notify", options);
  
}
```