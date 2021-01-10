## カウントアップ機能を作る
+ボタンを押すと1ずつ数字が増えていくカウントアップ機能をReactでつくる。

### stateを定義する
`constructor`内でプロパティ名が`count`、値が`0`の`state`を定義する。

```js
constructor(props) {
    super(props);
    this.state = {count:0};
  }
```

### ボタンとつくり、stateを表示
ボタンは`button`のタグを使ってつくる。そして前述で定義した`state`を`return`内で表示させる。その際、`this.state.count`はJavascriptなので、`{}`で囲む。

```js
render() {
    return (
      <div>
        <h1>{this.state.count}</h1>
        
        <button>+</button> 
      </div>
    );
  }
```

### handleClickを定義
`handleClick`のメソッドを定義して、`state`の`count`の値に`1`を足す処理を追加する。

```js
handleClick(){
    this.setState({count: this.state.count + 1});
  }
```
### buttonタグにonClickイベントを追加
`button`タグに`onClick`のイベントを追加して、`onClick`のイベント時に前述で定義した`handleClick`のメソッドが呼び出されるようにする。

```js
<button onClick={()=>{
    this.handleClick()
    }
}>+</button>
```