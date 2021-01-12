# 出勤管理の出来るLINE　BOTを作る
Google　Apps　Scriptを用いて出勤管理を行うためのLINE　Botを作っていく。
## LINE Botの作り方
### LINE Developersのページでプロバイダーとチャネルを作る 
1.  LINE Developersにログインし、新しくプロバイダーを作成する。(プロバイダー名は公開されるので、個人名などは避け、適切な名前にする。また、ユーザーIDはプロバイダーに紐づけられる。)
2. チャネルの設定はMessaging APIを選択。その後は基本設定を行う。

### GASでWebhook URLを発行し、チャネルに張り付ける
1.  https://docs.google.com/spreadsheets/d/1dDHbpPX-7tdNEQW-VaA4IvydrJBPksP806nNXsHumWY/edit#gid=0 を開き、このスプレッドシートをコピーする。その後、ツールをクリックし、スクリプトエディタを選択すると、GASを開くことが出来る。
2. Messaging　API設定のところでチャネルアクセストークンを発行しコピー。その後、先ほど開いたGASのアクセストークンのところにペーストする。
3. スプレッドシートのIDとURLをGASに入力する。URLはスプレッドシートのURLをそのまま入力。IDの方はスプレッドシートのURLのd/の次から/editの前までのコードを入力。
4. LINE　Official Account Managerを開き、応答設定を開く。そこの詳細設定で応答メッセージをオフ、Webhookをオンにする。
5.  GASの公開をクリックし、ウェブアプリケーションとして導入を選択。デプロイ出来たら、URLが発行されるので、これをWebhookのURLに張り付ける。

## リッチメニューで文字を打たずにボタン操作
1. LINE　Official Account Managerを開き、ホームからリッチメニューを開いて、リッチメニューを作成。
2. 表示設定、コンテンツ設定を行う。