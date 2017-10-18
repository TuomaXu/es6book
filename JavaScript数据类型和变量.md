# 第3章 JavaScript数据类型和变量

## 3.1 数据类型

计算机顾名思义就是可以做数学计算的机器，因此，计算机程序理所当然地可以处理各种数值。但是，计算机能处理的远不止数值，还可以处理文本、图形、音频、视频、网页等各种各样的数据，不同的数据，需要定义不同的数据类型。

在JavaScript中定义了以下几种数据类型：

* Number：JavaScript不区分整数和浮点数，统一用Number表示
* String：以单引号'或双引号"括起来的任意文本
* Boolean：布尔值和布尔代数的表示完全一致，一个布尔值只有true、false两种值。
* Object：对象是一组由键-值组成的无序集合
* 空值：什么也没有，用`null`表示

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

### 空值

`null`表示一个“空”的值，它和`0`以及空字符串`''`不同，`0`是一个数值，`''`表示长度为0的字符串，而`null`表示“空”。

在其他语言中，也有类似JavaScript的`null`的表示，例如Java也用`null`，Swift用`nil`，Python用`None`表示。但是，在JavaScript中，还有一个和`null`类似的`undefined`，它表示“未定义”。

JavaScript的设计者希望用`null`表示一个空的值，而`undefined`表示值未定义。事实证明，区分两者的意义不大。大多数情况下，我们都应该用`null`。`undefined`仅仅在判断函数参数是否传递的情况下有用。

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