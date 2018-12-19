# レッスン7. Advanced ES6

## 目的

- 分割代入などES6の新しい機能を知る。

## 分割代入(Destructuring)

分割代入はオブジェクトと配列内のプロパティや要素を変数にアクセスする際の手間を減らすために導入された仕組みです。

### Objectの分割代入

- **Object内のプロパティを変数に代入する**

ES5まではObject内のプロパティを変数に代入するには以下のようにしていました。

```javascript
let person = {
  name: "Steve Jobs",
  email: "steve@apple.com"
}

let name = person.name;
let email = person.email; 
```

これを分割代入を利用すると以下のように書くことが出来ます。

```javascript
let { name, email } = person;

console.log(name); // "Steve Jobs"
console.log(email); // "steve@apple.com"
```

このように、カーリーブレイス`{}`に、Objectのキーを含め、右側にはobjectのみを置きます。

- **Objectの値を代入する**

またObjectを作成する際にも分割代入の仕組みを利用するとコーディング量を減らすことが出来ます。以下はES5までのオブジェクト作成の例です。

```javascript
let name = "Steve Jobs";
let email = "steve@apple.com";

let person = {
  name: name,
  email: email
};
```

分割代入を利用すると、これは以下のように書き換えられます。

```javascript
let person = { 
  name, 
  email 
}
```

このようにキーの値に代入する変数名がキー名と同一の場合`キー名: 変数名`の`: 変数名`の部分を省略することが出来ます。

- **デフォルトの値を設定する**

また、変数に値を代入する際に値がない場合はデフォルトの値を入れるということも出来ます。例えば、以下では、roleが設定されていない場合は"CEO"を自動的で代入するようにしています。

```javascript
let person = {
  name: "Steve Jobs",
  email: "steve@apple.com",
  role: null
}

let { name, email, role = "CEO" } = person;

console.log(role); // "CEO"
```

- **異なる変数名を利用する**

また、分割代入を行う際に変数名をオブジェクトのkeyとは異なるものを利用したい場合もあるでしょう。こうした際には以下のようにします。

```javascript
let person = {
  name: "Steve Jobs",
  email: "steve@apple.com",
  role: null
}

let { name: fullName, email: mail, role: job = "CEO" } = person;

console.log(fullName); // "Steve Jobs"
console.log(mail); // "steve@apple.com"
console.log(job); // "CEO
```

- **ネストされたオブジェクトに対する分割代入**

また、オブジェクトにネストされたオブジェクトがある場合は以下のようにして分割代入を行います。以下ではcompanyというネストされたオブジェクトのキーにアクセスしています。

```javascript
let person = {
  name: "Steve Jobs",
  email: "steve@apple.com",
  company: {
    name: "Apple, Inc",
    founded: "1976年4月1日"
  }
}

let { company: { name: companyName, founded = "不明" } } = person;

console.log(companyName); // "Apple, Inc"
console.log(founded); // "1976年4月1日"
```

### Arrayの分割代入

Arrayの分割代入のシンタックスはObjectの分割代入と非常に似ている


- **Arrayの要素を代入する**

以下は、配列の最初の2つの要素を変数に代入する場合の例です。

```javascript
let companies = ["Apple", "Facebook", "Microsoft"];

let [ apple, facebook ] = companies;

console.log(apple); // "Apple"
console.log(facebook); // "Facebook"
```

また、配列の3番目の要素のみを変数に代入したい場合は以下のようにします。

```javascript
let [ , , microsoft ] = companies;

console.log(microsoft); // "Microsoft"
```

- **変数に値を代入する**

分割代入を使うと、既存の変数にArrayからまとめて値を代入することも簡単です。

```javascript
let companies = ["Apple", "Facebook", "Microsoft"];
let apple = "Apple, Inc";
let facebook = "Facebook, Inc";

[ apple, facebook ] = companies;

console.log(apple); // "Apple"
console.log(facebook); // "Facebook"
```

- **変数の値の交換**

上記の変数への代入を応用することで、2つの変数の値を交換することも出来ます。

以下は分割代入を利用しない場合の値の交換の例です。

```javascript
let a = 1, b = 2, temp;

temp = a;
a = b;
b = temp;

console.log(a); // 2
console.log(b); // 1
```

上記のように、分割代入をしない場合はtempという変数を用意し、そこに一旦aの値を代入するという手間が発生します。これを分割代入を使って次のように書き換えることが出来ます。

```javascript
let a = 1, b = 2;

[ a, b ] = [ b, a ]

console.log(a); // 2
console.log(b); // 1
```

- **デフォルトの値の設定**

Objectの場合と同様にデフォルトの値を設定出来ます。

```javascript
let companies = ["Apple", "Facebook", "Microsoft"];

let [ apple, facebook, , tesla = "Tesla, Inc" ] = companies;

console.log(tesla); // "Tesla, Inc"
```

- **ネストされたArrayの分割代入**

Objectの場合と同様、ArrayにネストされたArrayの値を分割代入することも出来ます。

```javascript
let companies = ["Apple", ["Facebook", "Instagram"], "Microsoft" ];

let [ , [ facebook, instagram ] ] = companies

console.log(facebook); // "Facebook";
console.log(instagram); // "Instagram";
```

## spreadオペレーター

spreadオペレーターは、繰り返し処理の可能な要素(配列、オブジェクト、文字列)を展開するための構文です。ファンクションの引数として代入したり、新しい配列を作成する際に利用します。spreadオペレーターの基本的なシンタックスは以下です

```javascript
...iterable
```

以下では、spreadオペレーターの利用方法を紹介します。

- **配列に利用する**

例えば、以下は文字列をspreadオペレーターで展開して配列に代入する例です。

```javascript
let str = "abc";

let arr = [...str, "d", "e", "f"];

console.log(arr); // ["a", "b", "c", "d", "e", "f"]
```

- **ファンクションの引数に利用する**

以下はファンクションの引数としてarrayの要素をとる例です。

```javascript

let numbers = [1, 2, 3];

const addThreeNums = (a, b, c) => {
  return a + b + c;
};

console.log(addThreeNums(...numbers)); // 6
```

- **オブジェクトを複製する**

オブジェクトを複製したいという場合、Object.assignを使う方法以外に、spreadオペレーターを利用する方法があります。

```javascript
let obj = {
  color1: "red",
  color2: "green",
  color3: "blue"
};

let copy1 = Object.assign({}, obj);
let copy2 = { ...obj };

console.log(copy1); // {color1: "red", color2: "green", color3: "blue"}
console.log(copy2); // {color1: "red", color2: "green", color3: "blue"}
console.log(copy1 === obj); // false
console.log(copy2 === obj); // false
console.log(copy1 === copy2); // false
```

- **配列を複製する**

オブジェクトと同様に配列の複製も出来ます。

```javascript
let arr = [1, 2, 3];
let copy1 = arr.slice();
let copy2 = [...arr];

console.log(copy1); // [1, 2, 3]
console.log(copy2); // [1, 2, 3]
console.log(arr === copy1); // false
console.log(arr === copy2); // false
console.log(copy1 === copy2); // false
```

## restパラメーター

restパラメーターを利用すると、複数の要素を配列としてファンクションの引数に与えることが出来ます。restパラメーターのシンタックスは以下の通りです。

```javascript
function(引数1, 引数2, ...複数の引数) {}
```

restパラメーターより前の、引数の数には制限はありません。またrestパラメーターは引数の最後にしか置けないという制限があります。そのため、以下の書き方はエラーとなります。

```javascript
function(引数1, ...複数の引数, 引数2) {}
```

以下は実際にrestパラメーターを利用して、会社の製品名を複数表示する例です。

```javascript
function sayProducts(company, ...products) {
  console.log(`${company}のサービスは以下のようなものがあります: `)
  for (let product of products ) {
    console.log(product);
  }
}

sayProducts("Google", "Googleドライブ", "Gmail", "Googleドキュメント", "Googleサーチ");
/* 
Googleのサービスは以下のようなものがあります:
Googleドライブ
Googleドキュメント
Googleサーチ
*/
```

このように、引数の数が決っていない場合に、繰り返し処理を行う上で、restオペレーターを利用すると便利です。

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

- **Setを配列に変換する**

Setと配列は非常によく似ているため、Setを配列に返還することも簡単に出来ます。また、先ほど学んだspreadオペレーターと組み合わせることで重複をなくした配列を簡単に作ることが出来ます。

```javascript
let arr1 = [1,3,1,2,4,3]; // 重複を持つ配列
let set1 = new Set(arr1); // 配列からSetを作成する。
let arr2 = [...set1]; // スプレッドオペレーターを利用して、Setを配列に変換する。

console.log(arr2); // [1,3,2,4];
```

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
  console.log(obj1[key]);
});
```

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

## Symbol

### シンボル

ES5にはなかったシンボルがES6では使用できるようになりました。シンボルはオブジェクトに似ているため、作成されたシンボルは全てユニーク、つまりどれ一つとして同じになるシンボルはないと言う特徴があります。

シンボルはプリミティブ（基本型）で、リテラル（テキスト文字）表現を持たないことも特徴です。

シンボルは以下のように書くことで使用できます。

```js
const GREETINGS = Symbol("こんにちは");
console.log(GREETINGS); // Symbol(こんにちは)
```

<img src="images/class2-symbol.png" />

 `Symbol(こんにちは)` が返ってきました。

シンボルがユニークなことである証拠を確かめてみましょう。
１つの例として、 `厳密等価演算子` の `===` を使用して確かめます。

厳密等価演算子は、以下のケースかどうかを確かめることができます。
（詳しくはClass 3へ。）

| 厳密等価演算子として見なされる基準 |  |
| ------------- | -----:|
| 同じオブジェクトを参照 | プリミティブ型で、データ型も値も同じ |

これだけでは少し理解が難しいので、簡単な厳密等価演算子の例を先に見てみましょう。

```js
const one = 1;
const literalOne = "1";
console.log(one === literalOne); // false
```

同じ `1` を変数に入れたのに、なぜ `false` が返ってきたのでしょうか？
これは、１行目の `one` の1は数値で、２行目の `literalOne` は文字列としての1という `データ型の違い` （文字列と数値という違い）があり、厳密等価演算子では `false` つまり one と literalOne は同じ１ではないと見なされます。

話を元に戻すと、シンボルがユニーク、つまり１つ１つ異なるものであることを証明するために厳密等価演算子を使用してみましょうとなっていたので、上記の例を利用します。

先ほどの例が同じ１でも、データ型が異なっていたために `false` になったのであれば、データ型の違いはなくても、１つ１つがユニークでお異なるシンボルは同じ名前のシンボルでも `false` となるはずです。

```js
const me = Symbol("私");
const watashi = Symbol("私");
console.log(me === watashi);// false
```

これは、特にオブジェクトとオブジェクト指向プログラミングにおいて、識別子を区別する際にとても役立ちます。

オブジェクトに新しいプロパティを加える時に、他に既存のプロパティと同じ識別子になってしまい、競合するというリスクをなくすことができます。

## チャレンジ

- [チャレンジ7](./challenge/README.md)

## 更に学ぼう

### 記事で学ぶ

- [分割代入 - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Map - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Map)
- [Symbol - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
- [Rest parameters - Mozilla](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Functions_and_function_scope/rest_parameters)
