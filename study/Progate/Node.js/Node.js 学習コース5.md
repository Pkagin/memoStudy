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

