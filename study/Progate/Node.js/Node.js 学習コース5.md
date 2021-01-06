# ログイン機能を作ろう

## 1.ログイン機能を作ろう
### app.jsでlogin.ejsを表示させる。

```js
app.get('/login', (req, res)=>{
  res.render('login.ejs');
})login.ejs
```

### login.ejs内でメールアドレスとパスワードを入力する欄を作成。

```js
<p>メールアドレス</p>
    <input type="text">

<p>パスワード</p>
    <input type='password'>
```
## ユーザー認証の処理を作ろう（１）
ログイン画面のフォームの値を受け取るルーティングを用意

```list.ejs
<li><a href="/login">ログイン</a></li>
```

```app.js
app.post("/login", (req, res) => {
  res.redirect("/list");
```

