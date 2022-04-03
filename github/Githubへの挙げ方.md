## gitから新しくレポジトリをクローンしてプッシュまでの操作

1.  git clone レポジトリのUR
2.  cd レポジトリ名
3.  code レポジトリ名

### ここはずして書いたほうがいいんじゃない

4.  git add .
    git commit -m "commit"
    git push


## 先にローカルにフォルダーをつくった場合

1.  レポジトリ作成
    ### ここはgithubcliでできるので今後したほうがいい

### ある程度抽象化して書いたほうがわかると思う
2.  ⇓をターミナルにペースト
    echo "# レポジトリ名" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/Pkagin/レポジトリ名.git
    git push -u origin main


## 未解決タスク(例)
### タスクが発生した日時と終了した日時を書いたほうがあとで見やすいよ
1.  github cliの導入 12/30-12/31 11:00
2.  cliからレポジトリを作成できるようにする 12/30-


## ログ
