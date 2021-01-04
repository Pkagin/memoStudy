## gitから新しくレポジトリをクローンしてプッシュまでの操作

1.  git clone レポジトリのURL
2.  cd レポジトリ名
3.  code レポジトリ名
4.  git add .
    git commit -m "commit"
    git push


## 先にローカルにフォルダーをつくった場合

1.  レポジトリ作成
2.  ⇓をターミナルにペースト
    echo "# gasRepository" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin https://github.com/Pkagin/gasRepository.git
    git push -u origin main