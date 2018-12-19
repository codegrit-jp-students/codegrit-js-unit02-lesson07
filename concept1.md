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