# jsonで取得したコードをHTML上に表示できるようにする
jsonで取得したコードをHTML上に表示させるようにします。

## JavaScriptのコード

・HTML上に表示させるため、`document.getElementById`でidを取得。
・非同期処理を行うため、`async`と`await`を使う。
・`fetch`を用いてjsonのデータを返す。

```index.js
const output = document.getElementById("output");

async function testfunc(){
    var url = "取得したjsonのURL";
    const res = await fetch(url);
    const users = await res.json();
```

・`forEach`を使い、jsonのそれぞれのオブジェクトを取得。
・`document.createElement(p)`を使い、pタグを生成。
・`innerText`を用いて、pタグの中に今回は例として、jsonのidというオブジ　ェクトを取得。
・`appendChild()`を用いて、取得した情報をHTML上に表示させるようにす　　る。


```
    users.forEach((user) => {
        const title = document.createElement("p");
        title.innerText = user.id;
        output.appendChild(title);
    }
```

## HTMLのコード
`output`のidを準備して、ここにindex.jsで取得した情報を表示させるようにする。

```index.html
<body>
    <script src="index.js"></script>
    <div id="output"></div>
</body>
```
これでHTML上にjsonの情報が表示されます。

# コード書いたときに感じたこと
・`output`のようなidを指定しないと、HTML上に表示出来ないので注意。
・`forEach`以外にも、`for`を使うのもよさそうです。
・`document.write()`を使うとただの文字列になってしまうので、　`createElement`を使った方がいいと思います。