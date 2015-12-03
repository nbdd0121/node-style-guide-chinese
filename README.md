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
* [用小写驼峰命名变量、属性和函数名](#用小写驼峰命名变量、属性和函数名)
* [用大写驼峰命名类名](#用大写驼峰命名类名)
* [用全大写命名常量](#用全大写命名常量)

### 变量
* [Object / Array creation](#object--array-creation)

### Conditionals
* [Use the === operator](#use-the--operator)
* [Use multi-line ternary operator](#use-multi-line-ternary-operator)
* [Use descriptive conditions](#use-descriptive-conditions)

### Functions
* [Write small functions](#write-small-functions)
* [Return early from functions](#return-early-from-functions)
* [Name your closures](#name-your-closures)
* [No nested closures](#no-nested-closures)
* [Method chaining](#method-chaining)

### Comments
* [Use slashes for comments](#use-slashes-for-comments)

### Miscellaneous
* [Object.freeze, Object.preventExtensions, Object.seal, with, eval](#objectfreeze-objectpreventextensions-objectseal-with-eval)
* [Requires At Top](#requires-at-top)
* [Getters and setters](#getters-and-setters)
* [Do not extend built-in prototypes](#do-not-extend-built-in-prototypes)

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

### Object / Array creation

Use trailing commas and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = ['hello', 'world'];
var b = {
  good: 'code',
  'is generally': 'pretty',
};
```

*Wrong:*

```js
var a = [
  'hello', 'world'
];
var b = {"good": 'code'
        , is generally: 'pretty'
        };
```

## Conditionals

### Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0;
if (a !== '') {
  console.log('winning');
}

```

*Wrong:*

```js
var a = 0;
if (a == '') {
  console.log('losing');
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

### Use multi-line ternary operator

The ternary operator should not be used on a single line. Split it up into multiple lines instead.

*Right:*

```js
var foo = (a === b)
  ? 1
  : 2;
```

*Wrong:*

```js
var foo = (a === b) ? 1 : 2;
```

### Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptively named variable or function:

*Right:*

```js
var isValidPassword = password.length >= 4 && /^(?=.*\d).{4,}$/.test(password);

if (isValidPassword) {
  console.log('winning');
}
```

*Wrong:*

```js
if (password.length >= 4 && /^(?=.*\d).{4,}$/.test(password)) {
  console.log('losing');
}
```

## Functions

### Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

### Return early from functions

To avoid deep nesting of if-statements, always return a function's value as early
as possible.

*Right:*

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

*Wrong:*

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

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100);
  return isInRange;
}
```

### Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning');
});
```

*Wrong:*

```js
req.on('end', function() {
  console.log('losing');
});
```

### No nested closures

Use closures, but don't nest them. Otherwise your code will become a mess.

*Right:*

```js
setTimeout(function() {
  client.connect(afterConnect);
}, 1000);

function afterConnect() {
  console.log('winning');
}
```

*Wrong:*

```js
setTimeout(function() {
  client.connect(function() {
    console.log('losing');
  });
}, 1000);
```


### Method chaining

One method per line should be used if you want to chain methods.

You should also indent these methods so it's easier to tell they are part of the same chain.

*Right:*

```js
User
  .findOne({ name: 'foo' })
  .populate('bar')
  .exec(function(err, user) {
    return true;
  });
````

*Wrong:*

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

## Comments

### Use slashes for comments

Use slashes for both single line and multi line comments. Try to write
comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things.

*Right:*

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

*Wrong:*

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

## Miscellaneous

### Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

### Requires At Top

Always put requires at top of file to clearly illustrate a file's dependencies. Besides giving an overview for others at a quick glance of dependencies and possible memory impact, it allows one to determine if they need a package.json file should they choose to use the file elsewhere.

### Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)

### Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Your future self will
be forever grateful.

*Right:*

```js
var a = [];
if (!a.length) {
  console.log('winning');
}
```

*Wrong:*

```js
Array.prototype.empty = function() {
  return !this.length;
}

var a = [];
if (a.empty()) {
  console.log('losing');
}
```