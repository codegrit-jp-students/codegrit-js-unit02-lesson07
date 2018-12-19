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