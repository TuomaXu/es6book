# 第3章 JavaScript数据

## 3.1 数据类型

计算机顾名思义就是可以做数学计算的机器，因此，计算机程序理所当然地可以处理各种数值。但是，计算机能处理的远不止数值，还可以处理文本、图形、音频、视频、网页等各种各样的数据，不同的数据，需要定义不同的数据类型。

在JavaScript中定义了以下几种数据类型：

* Number：JavaScript不区分整数和浮点数，统一用Number表示
* String：以单引号'或双引号"括起来的任意文本
* Boolean：布尔值和布尔代数的表示完全一致，一个布尔值只有true、false两种值。
* Object：对象是一组由键-值组成的无序集合
* 空值：什么也没有，用`null`表示
* Symbo：表示独一无二的值

### 3.1.1 Number

JavaScript不区分整数和浮点数，统一用Number表示，以下都是合法的Number类型：

```
123; // 整数123
0.456; // 浮点数0.456
1.2345e3; // 科学计数法表示1.2345x1000，等同于1234.5
-99; // 负数
NaN; // NaN表示Not a Number，当无法计算结果时用NaN表示
Infinity; // Infinity表示无限大，当数值超过了JavaScript的Number所能表示的最大值时，就表示为Infinity

```Number可以直接做四则运算，规则和数学一致：

```
1 + 2; // 3
(1 + 2) * 5 / 2; // 7.5
2 / 0; // Infinity
0 / 0; // NaN
10 % 3; // 1
10.5 % 3; // 1.5
```

>注意%是求余运算


### 3.1.2 String

字符串是以单引号'或双引号"括起来的任意文本，比如'abc'，"xyz"等等。请注意，''或""本身只是一种表示方式，不是字符串的一部分，因此，字符串'abc'只有a，b，c这3个字符。

```
'Hellow'

"World"
```

### 3.1.3 Boolean

布尔值和布尔代数的表示完全一致，一个布尔值只有true、false两种值，要么是true，要么是false，可以直接用true、false表示布尔值，也可以通过布尔运算计算出来：

```
true; // 这是一个true值
false; // 这是一个false值
2 > 1; // 这是一个true值
2 >= 3; // 这是一个false值
```

### 3.1.4 Object

JavaScript的对象是一组由键-值组成的无序集合，例如：

```
{
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

JavaScript对象的键都是字符串类型，值可以是任意数据类型。上述person对象一共定义了6个键值对，其中每个键又称为对象的属性。

### 3.1.5 空值

`null`表示一个“空”的值，它和`0`以及空字符串`''`不同，`0`是一个数值，`''`表示长度为0的字符串，而`null`表示“空”。

在其他语言中，也有类似JavaScript的`null`的表示，例如Java也用`null`，Swift用`nil`，Python用`None`表示。但是，在JavaScript中，还有一个和`null`类似的`undefined`，它表示“未定义”。

JavaScript的设计者希望用`null`表示一个空的值，而`undefined`表示值未定义。事实证明，区分两者的意义不大。大多数情况下，我们都应该用`null`。`undefined`仅仅在判断函数参数是否传递的情况下有用。

### 3.1.6 Symbol值

ES6 引入了一种新的原始数据类型`Symbol`，表示独一无二的值。它是 JavaScript 语言的基本数据类型。

Symbol 值通过`Symbol`函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

```javascript
let s = Symbol();

typeof s
// "symbol"
```

上面代码中，变量`s`就是一个独一无二的值。`typeof`运算符的结果，表明变量`s`是 Symbol 数据类型，而不是字符串之类的其他类型。

注意，`Symbol`函数前不能使用`new`命令，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象。也就是说，由于 Symbol 值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。

`Symbol`函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

```javascript
let s1 = Symbol('a');
let s2 = Symbol('b');

s1 // Symbol(a)
s2 // Symbol(b)

s1.toString() // "Symbol(a)"
s2.toString() // "Symbol(b)"
```

上面代码中，`s1`和`s2`是两个 Symbol 值。如果不加参数，它们在控制台的输出都是`Symbol()`，不利于区分。有了参数以后，就等于为它们加上了描述，输出的时候就能够分清，到底是哪一个值。

如果 Symbol 的参数是一个对象，就会调用该对象的`toString`方法，将其转为字符串，然后才生成一个 Symbol 值。

```javascript
const obj = {
  toString() {
    return 'abc';
  }
};
const s = Symbol(obj);
s // Symbol(abc)
```

注意，`Symbol`函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的`Symbol`函数的返回值是不相等的。

```javascript
// 没有参数的情况
let s1 = Symbol();
let s2 = Symbol();

s1 === s2 // false

// 有参数的情况
let s1 = Symbol('foo');
let s2 = Symbol('foo');

s1 === s2 // false
```

上面代码中，`s1`和`s2`都是`Symbol`函数的返回值，而且参数相同，但是它们是不相等的。

Symbol 值不能与其他类型的值进行运算，会报错。

```javascript
let sym = Symbol('My symbol');

"your symbol is " + sym
// TypeError: can't convert symbol to string
`your symbol is ${sym}`
// TypeError: can't convert symbol to string
```

但是，Symbol 值可以显式转为字符串。

```javascript
let sym = Symbol('My symbol');

String(sym) // 'Symbol(My symbol)'
sym.toString() // 'Symbol(My symbol)'
```

另外，Symbol 值也可以转为布尔值，但是不能转为数值。

```javascript
let sym = Symbol();
Boolean(sym) // true
!sym  // false

if (sym) {
  // ...
}

Number(sym) // TypeError
sym + 2 // TypeError
```

有时，我们希望重新使用同一个 Symbol 值，`Symbol.for`方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol值。如果有，就返回这个 Symbol 值，否则就新建并返回一个以该字符串为名称的 Symbol 值。

```javascript
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2 // true
```

上面代码中，`s1`和`s2`都是 Symbol 值，但是它们都是同样参数的`Symbol.for`方法生成的，所以实际上是同一个值。

`Symbol.for()`与`Symbol()`这两种写法，都会生成新的 Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会。`Symbol.for()`不会每次调用就返回一个新的 Symbol 类型的值，而是会先检查给定的`key`是否已经存在，如果不存在才会新建一个值。比如，如果你调用`Symbol.for("cat")`30次，每次都会返回同一个 Symbol 值，但是调用`Symbol("cat")`30次，会返回30个不同的 Symbol 值。

```javascript
Symbol.for("bar") === Symbol.for("bar")
// true

Symbol("bar") === Symbol("bar")
// false
```

上面代码中，由于`Symbol()`写法没有登记机制，所以每次调用都会返回一个不同的值。

`Symbol.keyFor`方法返回一个已登记的 Symbol 类型值的`key`。

```javascript
let s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

上面代码中，变量`s2`属于未登记的 Symbol 值，所以返回`undefined`。

需要注意的是，`Symbol.for`为 Symbol 值登记的名字，是全局环境的，可以在不同的 iframe 或 service worker 中取到同一个值。

```javascript
iframe = document.createElement('iframe');
iframe.src = String(window.location);
document.body.appendChild(iframe);

iframe.contentWindow.Symbol.for('foo') === Symbol.for('foo')
// true
```

上面代码中，iframe 窗口生成的 Symbol 值，可以在主页面得到。



## 3.2 变量

在程序运行过程中，其值可以改变的量称为变量。变量是用于存储信息的"容器"。

### 3.2.1 变量的命名

JavaScript中的变量名必须以字母开头，其后可以跟数字和下划线等，不能有空格，不可以使用`+`、`-`、`，`、`？`等运算符或者标点符号表示，不可以使用关键字如let、const、for等。


### 3.2.2 let关键字

let声明变量非常简单，如下代码：

```
let name = 'Tom';
console.log(name);

let a = 1;
let b = 2;
let sum = a+b;

let age;
age = 10;
age = 11;
```

> 在声明变量中，变量名为驼峰命名法。例如：let myName = 'Tom';

变量一定要先申明，再使用，例如：

```
console.log(name);//错误，找不到name
let name = 'Tom';
```

### 3.2.3 const关键字

const声明的变量，其值不能改变，代码如下：

```
const age = 10;
age = 11;//error，const 声明的变量，其值不能改变
```

但大家一定注意一点，const声明的变量值不能变，但如果该变量为对象，其对象属性值可变。

```
const person={
	name:'Tom',
	age:10,
};

person.name = 'Jhon';//没问题

person = {
	name:'TT',
	age:11
}//error，错误，不能改变person的值

```

### 3.2.4 变量作用域

JavaScript语言中所有的量都有自己的作用域。变量声明的方式不同，其作用域也不同。JavaScript语言中的变量，按作用域范围可分为两种，即局部变量和全局变量。

局部变量也称为内部变量。局部变量是在函数形参或大括号内作定义申明的。其作用域仅限于函数内或相应大括号内， 离开该函数或大括号后再使用这种变量是非法的。

>有关函数的内容在后续章节讲解

```
{
	const name = 'Tom';
	console.log(name);//正确
}//变量name的作用域到此结束
console.log(name);//错误！name作用域再上面大括号内，超过无法使用
```

在有多层作用域嵌套的情况下，如果有同名变量，内层变量会屏蔽外面变量作用域，例如：

```
{
	const name = 'Tom';
	{
		const name = 'Jim';
		console.log(name);//打印为Jim
	}
	console.log(name);//打印为Tom
}
```

在多层作用域嵌套下，如没有同名变量，作用域范围不变。例如：

```
{
	const name = 'Tom';
	{
		console.log(name);//打印为Tom
	}
	console.log(name);//打印为Tom
}
```

注意，在多层作用域嵌套下，内层如有声明同名变量，内层变量声明之前，变量不能使用。例如：

```
{
	const name = 'Tom';
	{
		console.log(name);//错误！找不到name变量！
		const name = 'Jim';
	}
	console.log(name);//打印为Tom
}
```

全局变量是在函数外部定义的变量。它不属于哪一个函数，它属于一个源程序文件模块。其作用域是从定义开始的位置到整个文件模块结束。

```
const age = 10;//全局变量
{
	const name = 'Tom'//局部变量
}
```

### 3.2.5 变量解构

变量解构是ES6中的新特性，可以对变量进行批量定义和赋值

在之前的语法中，如果有需要定义三个变量，并且赋值，需要至少写三行代码

```
const a = 1;
const b = 2;
const c = 3;
```

在变量解构中我们可以这样写一行代码，完成变量的定义和赋值

```
const [a,b,c] = [1,2,3];
```
变量解构的语法可以将变量的定义放在一个数据结构中同时，使用相同的数据结构对象为其变量赋值。

数据结构不仅可以为数字，还可以为对象

```
const {x,y} = {
	x:1,
	y:2
};
```

对对象进行变量结构是，一定注意**解构的变量名需要与对象中的键一致**

```
const {a,b} = {x:1,y:2};
//此种情况下，a和b为空值，
```

变量解构常用在函数参数传递过程，传递一个对象，通过变量解构出其具体的值。例如

```
func1({name,age}){
	console.log(name);
	console.log(age);
}

const per = {
	name:'Tom',
	age:10,
}

func1(per);
```

## 3.3 数据交互

### 数据控制台输出

`console.log()`可以将数据在控制台进行输出，其用法非常简单。

```
console.log(123);
console.log('Tom');

const name = 'Tom';
console.log(name);
```

### 数据控制台输入

在调试程序或编写算法等非界面应用时，经常需要从控制台输入数据实现数据交互。

nodejs环境本身不支持控制台数据输入，但社区中有人仿照C语言的`scanf`函数实现了nodejs中的阻塞输入。

```
import scanf from 'scanf';

console.log('请输入名字');
const name = scanf('%s');
console.log(name);
```

目前输入支持如下格式：

* %d - 整数
* %f - 浮点数
* %s - 字符串
* %S - 字符串（匹配处开始往后一整行）
* %x - 十六进制数字
* %o - 八进制数字

