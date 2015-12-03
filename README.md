# Node.js 代码风格指南

这是一份用来编写一致并且优雅的 node.js 代码的指南。这份规范源于社群中所流行的做法，并且按照个人意见稍作修改。

有一份 .jshintrc 会尽可能地实行这些规则。你可以使用并调整它，或者使用[这个脚本](https://gist.github.com/kentcdodds/11293570)来创建你自己的。

这份指南由 [Felix Geisendörfer](http://felixge.de/) 创建并由 [Gary Guo](http://github.com/nbdd0121) 翻译，授权在 [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/) 许可证下。你被鼓励来创建这个仓库的分支并按照自己喜好进行调整。

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 内容目录

### 格式化
* [用2格空格缩进](#用2格空格缩进)
* [换行](#换行)
* [没有行尾空格符](#没有行尾空格符)
* [使用分号](#使用分号)
* [每行最多80个字符](#每行最多80个字符)
* [使用单引号](#使用单引号)
* [在同一行写开大括号](#在同一行写开大括号)
* [每一个var语句只定义一个变量](#每一个var语句只定义一个变量)

### 命名规范
* [用小写驼峰命名变量、属性和函数名](#用小写驼峰命名变量属性和函数名)
* [用大写驼峰命名类名](#用大写驼峰命名类名)
* [用全大写命名常量](#用全大写命名常量)

### 变量
* [对象/数组的创建](#对象数组的创建)

### 条件
* [使用 === 运算符](#使用--运算符)
* [使用多行的三元运算符](#使用多行的三元运算符)
* [用描述性的条件](#用描述性的条件)

### 函数
* [写短小的函数](#写短小的函数)
* [尽早从函数返回](#尽早从函数返回)
* [给你的闭包命名](#给你的闭包命名)
* [避免嵌套闭包](#避免嵌套闭包)
* [链式方法调用](#链式方法调用)

### 注释
* [Use slashes for comments](#use-slashes-for-comments)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [在最顶端使用require](#在最顶端使用require)
* [Getter 和 Setter](#Getter-和-Setter)
* [不要扩展内建原型](#不要扩展内建原型)

## 格式化


### 用2格空格缩进

用2格空格缩进你的代码并且发誓绝不混合使用Tab和空格 - 不然一种特殊的地狱将会等待你的到来。

### 换行

使用UNIX风格换行 (`\n`), 并且把一个换行符作为文件的最后一个字符。Windows风格换行 (`\r\n`) 在任何仓库中被禁止使用。

### 没有行尾空格符

就像你会在吃饭后刷牙一样，你需要在提交你的JS文件之前清理任何行尾的空格符。否则腐烂的气味会最终赶走其他的贡献者和/或你的同事。

### 使用分号

根据[科学研究][hnsemicolons]，分号的使用是我们社群的核心价值。考虑一下[反对派][the opposition]的观点，但是我们需要注重传统，而不是滥用错误恢复机制，仅仅为了廉价的书写时的愉快。

[the opposition]: http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding
[hnsemicolons]: http://news.ycombinator.com/item?id=1547647

### 每行最多80个字符

每行最多限制在80个字符。是的，近几年屏幕越来越大，但是你的脑子并没有。使用额外的屏幕空间来分屏吧，你的编辑器肯定支持它，对吧？

### 使用单引号

除非你在写JSON，不然使用单引号。

*正确：*

```js
var foo = 'bar';
```

*错误：*

```js
var foo = "bar";
```

### 在同一行写开大括号

你的开大括号需要和你的语句写在同一行。

*正确：*

```js
if (true) {
  console.log('winning');
}
```

*错误：*

```js
if (true)
{
  console.log('losing');
}
```

另外，注意在条件前后空格的使用。

### 每一个var语句只定义一个变量

每一个var语句只定义一个变量，这样将这些行重排序就会轻松很多。另外，在函数内部深层定义变量忽略 [Crockford][crockfordconvention]的规范，把变量声明在有它们的存在意义的地方。

*正确：*

```js
var keys   = ['foo', 'bar'];
var values = [23, 42];

var object = {};
while (keys.length) {
  var key = keys.pop();
  object[key] = values.pop();
}
```

*错误：*

```js
var keys = ['foo', 'bar'],
    values = [23, 42],
    object = {},
    key;

while (keys.length) {
  key = keys.pop();
  object[key] = values.pop();
}
```

[crockfordconvention]: http://javascript.crockford.com/code.html

### 命名规范

### 用小写驼峰命名变量、属性和函数名

变量、属性和函数名应该使用小写驼峰 `lowerCamelCase`。它们的名字应该本身就是对自己的描述。单字母的变量和不常用的缩写在通常情况下应该被避免。

*正确：*

```js
var adminUser = db.query('SELECT * FROM users ...');
```

*错误：*

```js
var admin_user = db.query('SELECT * FROM users ...');
```

### 用大写驼峰命名类名

类名的首字母应该被大写，使用大写驼峰 `UpperCamelCase`。

*正确：*

```js
function BankAccount() {
}
```

*错误：*

```js
function bank_Account() {
}
```

## 用全大写命名常量

常量应该被像常规变量或者静态类属性一样被声明，用全大写 `UPPERCASE`。

*正确：*

```js
var SECOND = 1 * 1000;

function File() {
}
File.FULL_PERMISSIONS = 0777;
```

*错误：*

```js
const SECOND = 1 * 1000;

function File() {
}
File.fullPermissions = 0777;
```

译注：由于`const`已经在ECMAScript 2015中正式成为标准，原文中关于 [const][] 的一段文字已经被移除。但是在其认为普及的今天，仍然不推荐需要移植性的代码使用`const`。

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## 变量

### 对象/数组的创建

在末尾使用逗号，并且将*短小的* 声明放在一行中。只有在解释器会抱怨的时候才用引号包裹键：

*正确：*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*错误：*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## 条件

### 使用 === 运算符

编程不是如何记住[逗逼的比较运算符规则][comparisonoperators]。使用三重等号，因为它会如你期望的一般工作。

*正确：*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*错误：*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### 使用多行的三元运算符

三元运算符不应该放在同一行，而应该把它拆开放在多行。

*正确：*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*错误：*

```js
var foo = (a === b) ? 1 : 2;
```

译注：在只有一个三元运算符的简单情况下这样做可能会被认为冗余，但是对于包含多个三元运算符的复杂表达式来说，拆成多行能够大幅增加代码清晰度。

### 用描述性的条件

任何不显而易见的条件都应该被赋值到一个具有描述性名字的变量或者函数：

*正确：*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*错误：*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## 函数

### 写短小的函数

保持你的函数短小。一个好的函数能够被容纳在一张幻灯片里，并且坐在大房间最后面一排的人也能舒舒服服地读。所以别抱怨他们的视力太差，而是把每个函数的长度限制在大约15行。

### 尽早从函数返回

为了避免深层次嵌套 if 语句，始终尽早返回一个函数的值。

*正确：*

```js
function isPercentage(val) {
  if (val < 0) {
    return false;
  }

  if (val > 100) {
    return false;
  }

  return true;
}
```

*错误：*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}
```

或者，对于这个例子来说，用更加简化的方法也是可行的：

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### 给你的闭包命名

随心地给你的闭包命名。这表示你关心他们，并且这回产生更好的栈轨迹，堆和CPU档案。

*正确：*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*错误：*

```js
req.on('end', function() {
  console.log('losing');
});
```

### 避免嵌套闭包

使用闭包，但别嵌套他们。不然你的代码会看起来一团糟。

*正确：*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*错误：*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```


### 链式方法调用

如果你想链式调用方法，把每个方法写在独立的一行。

你也应该缩进这些行，这样更容易分辨出它们属于同一条链。

*正确：*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

*错误：*

```js
User
.findOne({ name: 'foo' })
.populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });

User.findOne({ name: 'foo' }).populate('bar')
.exec(function(err, user) {
  return true;
});

User.findOne({ name: 'foo' }).populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

## 注释

### 用双斜杠进行注释

不管是单行还是多行，始终使用双斜杠。尝试解释高层机制或者说明不同部分代码的意图，而不是附属一些显而易见的事情。

*正确：*

```js
// 'ID_SOMETHING=VALUE' -> ['ID_SOMETHING=VALUE', 'SOMETHING', 'VALUE']
var matches = item.match(/ID_([^\n]+)=([^\n]+)/));

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now());
if (isSessionValid) {
  // ...
}
```

*错误：*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/);

// Usage: loadUser(5, function() { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now());
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## 杂项

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

一些蛋碎并且你可能永远不需要使用的功能。远离它们。

### 在最顶端使用require

使用把 requires 放在文件的最前面，以说明该文件的依赖。这也可以给他人提供依赖的一览以及潜在的内存影响，这可以让人判断如果他们是否需要 package.json，那么是否选择应该在别处使用这个文件。

### Getter 和 Setter

别用 Setter，它们会对使用你软件的人造成更多的问题，甚至超过你的软件本身能够用来解决的问题。

可以随意使用没有[副作用][sideeffect]的 Getter，比如给一个集合类提供一个 length 属性。

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### 不要扩展内建原型

不要扩展JavaScript内建对象的原型。你未来的自己会感谢你的。

*正确：*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*错误：*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```