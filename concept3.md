## Set

SetもES6で新たに導入されたオブジェクト型です。Setは配列に非常によく似ており複数のリファレンス型やプリミティブ型の値を保持することが出来ます。Arrayとの大きな違いとして**Setは重複した値を持つことが出来ません**。Setを利用するのに便利なのはコレクションがある値を持つかどうかチェックしたい場合です。

- **Setの基本的な使い方**

```javascript
let set1 = new Set(); // 空のSetを作成する。
let set2 = new Set([1,2,3]); // 値を持つSetを作成する。
let person = {
  name: "Steve Jobs",
  email: "steve@apple.com"
}

// size関数を使い、Setの値の数をチェックする。
console.log(set1.size); // 0
console.log(set2.size); // 3

// add関数を使い、Setに値を追加する。
set1.add("1");
set1.add(1);
set1.add(person);

// has関数を使い、Setに値があるかどうかをチェックする。
console.log(set1.has(1)); // true

// 重複する値は保存されない。
console.log(set1.size); // 3
set1.add("1");
console.log(set1.size); // 3

// forEach関数で繰り返し処理を行う。
set1.forEach((item) => {
  console.log(item);
})

// Setから値を消去する。
set1.delete(1);
console.log(set1.size); // 2

// 全ての値を消去する。
set1.clear();
console.log(set1.size); // 0
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/Laq62d53/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

- **Setを配列に変換する**

Setと配列は非常によく似ているため、Setを配列に返還することも簡単に出来ます。また、先ほど学んだspreadオペレーターと組み合わせることで重複をなくした配列を簡単に作ることが出来ます。

```javascript
let arr1 = [1,3,1,2,4,3]; // 重複を持つ配列
let set1 = new Set(arr1); // 配列からSetを作成する。
let arr2 = [...set1]; // スプレッドオペレーターを利用して、Setを配列に変換する。

console.log(arr2); // [1,3,2,4];
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/vu6qw712/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## Map

Mapはkey-valueペアを格納することの出来るコレクションです。ES5まではObjectがMapの代わりとして使われていました。しかし、Objectの場合は、keyとしてString型かSymbol型の値しか取ることが出来ないという問題がありました。またObjectの要素に対して繰り返し処理を行う場合、まずkeyを得てからそのkeyで要素のvalue(値)を得るという手間がありました。

以下はObjectをkey-valueペアのコレクションとして利用した場合の例です。

```javascript
let obj1 = {
  1: "One", // 数字をkeyにしても強制的に"1"というStringに変換される。
  2: "Two",
  3: "Three"
}

let keys = Object.keys(obj1); // 繰り返し処理のためにkeyを配列としてまず得る。
console.log(keys[1]); // "1"

keys.forEach((key) => {
  console.log(obj1[key]); // "one" "Two" "Three"
});
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/dp7ygw08/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

上記のような、Objectを利用した場合の手間がMapではなく、またObjectに比べて高速で繰り返し処理を行うことが出来ます。

- **Mapの基本的な使い方**

```javascript

let map1 = new Map(); // 空のMapを作成する。
let map2 = new Map([
  [1, "One"],
  [2, "Two"],
  [3, "Three"]
]); // 要素を持つMapを作成する。

// set関数でMapにkey-valueペアを格納する。
map1.set("apple", "Apple");

// get関数でMapから値を得る。
console.log(map1.get("apple")); // "Apple"

// size関数でMap内の要素の数を得る。
console.log(map2.size); // 3

// has関数でMapに要素があるかどうか調べる。
console.log(map2.has("1")); // false
console.log(map2.has(1)); // true

// for...of関数で繰り返し処理を行う。
for (let [key, value] of map2) {
  console.log(`key: ${key} - value: ${value}のペアです。`);
}

// forEach関数を利用して繰り返し処理を行う。valueとkeyの順番に注意。
map2.forEach((value, key) => {
  console.log(`key: ${key} - value: ${value}のペアです。`);
});
```

<iframe width="100%" height="500" src="//jsfiddle.net/codegrit_hiro/pdmhetjx/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## Symbol

### シンボルの特徴と定義方法

シンボルはES6から追加されたプリミティブ型です。JavaScriptに習熟するまではシンボルを利用するメリットや使い所はなかなか分かりづらいかと思いますが存在については知っておき、徐々にマスターすることを目指しましょう。

以下のようにして作成することが出来ます。

```js
Symbol("シンボルの名前")
```

このような作成方法は他のプリミティブ型でも同様に出来ます。

```js
Number(5); 
5 // Number(5)の省略形

String("文字列です。")
"文字列です。" // String("文字列です。")の省略形

Boolean(true);
true // Boolean(true)の省略形
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/5upqhykd/1/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

他の型だと、上記の例のように省略して書く方法がありますがSymbolにはありません。

シンボル型は他のプリミティブ型と異なり、全てのシンボルはユニーク(互いに一致しない)です。

```js
// 他の型
true === true // true
"test" === "test" // true
5 === 5 // true

// シンボル型

Symbol("test") === Symbol("test") // false
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/8brxLqus/2/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

### シンボルの使いどころ

シンボルはES6から登場しましたが、ES5までは文字列でシンボルの代用をしてきていたこともあり、現状シンボルを使ったプログラムを見る機会は少ないかと思います。シンボルのわかりやすい使い所の一つは、限られた選択肢だけを持つ、Switch文などを作りたい場合です。

例えば以下の例を見てみましょう。

```js
let votes = 0;
const UPVOTE = Symbol('UP');
const DOWNVOTE = Symbol('DOWN');

function upvote() {
  console.log('ポジティブな投票をしました。')
  votes++;
}

function downvote() {
  console.log('ネガティブな投票をしました。')
  votes--;
}

function dealVote(vote) {
  switch (vote) {
    case UPVOTE:
      return upvote();
      break;
    case DOWNVOTE:
      return downvote();
      break;
    default:
      console.log("投票形式が異なります。")
  }
}

dealVote(UPVOTE); // ポジティブな投票をしました。
dealVote(UPVOTE); // ポジティブな投票をしました。
dealVote('UP'); // 投票形式が異なります。
dealVote('DOWN'); // 投票形式が異なります。
dealVote(DOWNVOTE); // ネガティブな投票をしました。
console.log(votes); // 1
```

<iframe width="100%" height="300" src="//jsfiddle.net/codegrit_hiro/q6hnfc1x/4/embedded/js,result/dark/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>

## 更に学ぼう

### 記事で学ぶ

- [分割代入 - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Map - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [Symbol - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [Rest parameters - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions_and_function_scope/rest_parameters)
