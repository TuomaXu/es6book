# 第7章 JavaScript对象

对象是客观世界存在的人、事和物体等实体。现实世界中存在很多的对象，如：猫、狗、汽车等。不难发现它们之间存在两个共同特征：都有状态和方法。比如猫有自己的状态（年龄、性别、毛色等）和行为（爬树、抓老鼠），汽车也有自己的状态（品牌、价格等）和行为（启动、加速、刹车）。面向对象编程（OPP）是一种计算机编程架构，其基本原则：计算机程序由单个能够起到子程序作用的单元或对象组合而成。具有三个最基本的特点：重用性、灵活性和扩展性。这种方法将软件程序的每个元素构成对象，同时对象的类型、属性和描述对象的方法。为了实现整体操作，每个对象都能够接收信息、处理数据和向其它对象发送信息。

## 7.1 对象概念

对象只是一种特殊的数据。对象拥有属性和方法。可以描述更复杂的问题。

例如:

在代码中描述一个三角形，如果使用普通变量进行描述，一个三角形由3个点组成，一个点有两个坐标组成，一共需要六个变量。

```
const a_x = 0;
const a_y = 0;

const b_x = 1;
const b_y = 0;

const c_x = 0;
const c_y = 1;
```

这时，如果需要使用三角形的ab边边长数据是，我们需要通过这写变量进行计算。

```
const dx = a_x - b_x;
const dy = a_y - b_y;
const a_b = Math.sqrt(dx*dx+dy*dy);
```

如果需要三角形的面积，我们就需要编写代码计算三个边长。然后在通过海伦公式求取三角形面积

```
const p = (a_b + b_c + c_a)/2;
const s = Math.sqrt(p*(p-a_b)*(p-b_c)*(p-c_a));
```

如果有多个三角形，需要使用多个三角形面积，以上代码还需要编写多遍。对于这个问题，我们可以使用函数对以上代码进行封装。

```
function distance(x1,y1, x2,y2){
	const dx = x1 - x2;
	const dy = y1 - y2;
	const d = Math.sqrt(dx*dx+dy*dy);
	return d;
}


function area(d1,d2,d3){
	const p = (d1 + d2 + d3)/2;
	const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
	return s;
}

```


但在代码复用时，这种使用函数封装代码的解决方案仍存在问题。要处理数据就需要首先获取数据处理函数。数据和数据处理方法是相互独立的。

**对象就是将数据和数据处理方法进行合并作为一个整体的数据类型**

对象中的数据称之为属性，相应的数据处理函数称之为方法。


我们现在用对象处理三角形的问题，将三角形的数据和数据处理函数通过对象组装到一起，形成一个对象。

```
const triangle = {
	a:{x:0,y:0},
	b:{x:1,y:0},
	c:{x:0,y:1},
	distance:function(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	},
	area:function(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
}
```
具体代码暂时不需要大家理解，只需要知道上述代码是创建了一个三角形对象，把三角形的数据和处理数据的方法都集合在了个对象内。

有了这个对象，我们就可以对三角形的数据进行直接操作了。

例如，求三角形的面积

```
const s = triangle.area();
console.log(s);
```

**这样包含数据和数据处理函数的变量，我们称之为对象，数据为对象的属性，处理函数为对象的方法。**

后续的编程，我们使用的变量除了数值以外基本上都是对象。

## 7.2 对象构造

JavaScript语言中，提供了两种构造对象的方法：

* 键值对构造法
* Class模板构造法

第一种构造方法相对简单，适用于处理比较单一的问题。第二种构造方法复杂，能够提供继承等面向对象特性。

### 7.2.1 键值对构造法

JavaScript语言中的对象可以简单看成一个键值对容器。通过键值对，一个对象可以储存多个数据和相应的数据处理函数。

首先来定义一个最简单的对象，该对象只储存简单数据，且该简单数据没有相应的处理函数。

还是以三角形为实际问题背景。这里我们首先用对象来描述三角形的顶点。

一个二维中的点具有横纵两个坐标信息。如果用变量表述需要使用两个变量：

```
const x = 0;
const y = 0;
```

但数据处理过程中，需要将相关联的数据合并在一起，所以要将这两个数据合并为一个对象进行保存。使用`{}`来构造一个键值对容器，然后在其中添加键值对构造一个对象。

```
const point = {
	x:0,
	y:0
}
```
这样只包含数据不包含相应数据处理函数的对象，称之为数据对象。通过JavaScript提供的`{}`构造语法，可以将多种信息已键值对的方式集合成一个对象，从而实现对复杂信息的描述。

构造语法注意事项：

* 键与值之间用`:`分割
* 键值对之间用`,`分割
* 最后一个键值对后面的逗号可加可不加，不影响编码语法。
* 键的类型为字符串，默认不需要加单引号或双引号，但如字符串中包含非字母数字字符时，需要加单引号或双引号。
* 值的类型可以为任意类型

```
const obj1 = {
	x-1:0,//此键值对语法错误
	'x-1':0,//包含非字母数字字符时，键需要加单引号或双引号
}

const obj2 = {
	obj:obj1,//值的类型可以为任何类型，当为数据对象类型是，表示嵌套结构
}

//obj2和obj3两个对象描述的数据相同，但注意不是两个对象相等。
const obj3 = {
	obj:{
		'x-1':0,
	}
}
```




在对象中添加一个值为函数的键值对，对象即有了处理数据的能力。

我们以一个对象描述一个线段。通过两个点即可确定一条线段，同时该对象还提供计算该线段长度的数据处理函数。

```
const line = {
	p1:{
		x:0,
		y:0
	},
	p2:{
		x:1,
		y:0
	},
	lenght:function(){
		const dx = this.p1.x - this.p2.x;
		const dy = this.p1.y - this.p2.y;
		return Math.sqrt(dx*dx + dy*dy);
	}
}

const lenght = line.lenght();
console.log(lenght);
```
在对象内添加的函数中，可以使用`this`关键字访问对象本身的属性。这样，就可以把数据和数据处理函数集合在一个对象中，使对象的功能更加强大。

通过上述的介绍，我们再次看之前构建三角形对象的代码：

```
const triangle = {
	a:{
		x:0,
		y:0
	},
	b:{
		x:1,
		y:0
	},
	c:{
		x:0,
		y:1
	},
	distance:function(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	},
	area:function(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
}
```
这段代码中，三角形的三个顶点属性通过一个对象来描述，然后将计算两个数据处理函数以键值对的方式加入了对象中，使三角形对象不仅可以描述三角形的基本信息，还可以对基本信息进行相应的处理。

但使用键值对方法构造带有数据处理函数的对象时，对代码复用问题不能很好的解决。

例如现在有三个三角形需要描述，那么我们将编写如下代码：

```
const triangle1 = {
	a:{
		x:0,
		y:0
	},
	b:{
		x:2,
		y:0
	},
	c:{
		x:0,
		y:2
	},
	distance:function(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	},
	area:function(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
}

const triangle2 = {
	a:{
		x:0,
		y:0
	},
	b:{
		x:3,
		y:0
	},
	c:{
		x:0,
		y:3
	},
	distance:function(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	},
	area:function(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
}

const triangle3 = {
	a:{
		x:0,
		y:0
	},
	b:{
		x:4,
		y:0
	},
	c:{
		x:0,
		y:4
	},
	distance:function(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	},
	area:function(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
}
```

我们发现描述这三个三角形的对象中，大部分代码都一样，只有对三角形数据部分的描述有变化。这样造成有大量重复的代码，在编写，维护和修改时都极为不方便，为了解决这个问题，JavaScript中提供了通过Class模板构造对象的方法。

### 7.2.2 Class模板构造法

Class翻译成中文称之为**类**，是对象的一种抽象描述。这里的抽象可以简单理解为数据处理过程。

```
class Point {
	constructor(x,y){
		this.x = x;
		this.y = y;
	}

	toString(){
		return `x is ${this.x}, y is ${this.y}`;
	}
}

const p = new Point(1,2);
const s = p.toString();
console.log(s);//输出结果为x is 1, y is 2;
```

上面代码演示了`class`的基本用法。

* 使用`class`定义一个类
* constructor为类的构造方法，通过该方法构造对象的属性
* 类中的方法不需要写function
* 通过`this`可以调用本身的方法和属性

我们还是用三角形作为问题背景，用Class来解决键值对构造法中代码无法复用的问题。

首先编写代码定义一个三角形类。

```
class Triangle {
	constructor(a,b,c){
		this.a = a;
		this.b = b;
		this.c = c;
	}
	
	distance(point1,point2){
		const dx = point1.x - point2.x;
		const dy = point1.y - point2.y;
		const d = Math.sqrt(dx*dx+dy*dy);
		return d;
	}
	
	area(){
		const d1 = this.distance(this.a,this.b);
		const d2 = this.distance(this.b,this.c);
		const d3 = this.distance(this.c,this.a);
		
		const p = (d1 + d2 + d3)/2;
		const s = Math.sqrt(p*(p-d1)*(p-d2)*(p-d3));
		
		return s;
	}
	
}
```

定义完类之后，便可以用类构造对象

```
const a = {
	x:0,
	y:0
}
const b = {
	x:1,
	y:0
}
const c = {
	x:0,
	y:1
}

//通过new关键字，这里的t1对象与上文中的triangle对象等价
const t1 = new Triangle(a,b,c);
const s = t1.area();
console.log(s);
```

如果有多个三角形对象需要描述，我们只需要通过`new`关键字进行构造对象即可，无需重复编写处理过程代码。

```
const t2 = new Triangle({x:0,y:0},{x:2,y:0},{x:0,y:2});
const t3 = new Triangle({x:0,y:0},{x:3,y:0},{x:0,y:3});
```
通过JavaScript提供的定义类机制，我们只需要对所描述的对象进行一次类抽象定义，然后便可以使用该类快速简洁的构造该类型的对象。


## 7.3 对象操作

JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成。无论是通过以上哪种方式进行构造，都符合上述定义。

在JavaScript中可以通过`.`运算符访问通过键对其相应的值进行读写操作。

例如：

```
//定义一个空对象
const obj = {
	name:'Tom',
	say:function(){
		console.log(`hello,my name is ${this.name}`);
	}
};

//添加一个键值对:name:'Tom'
obj.age = 20;

//修改
obj.name = 'Jhon';

//删除
obj.age = null

//访问
const name = obj.name;

//调用方法

obj.say();

```

除点语法外，还可以使用中括号对对象进行操作

```
//定义一个空对象
const obj = {};

//添加一个键值对:name:'Tom'
obj['name'] = 'Tom';

//修改
obj['name']  = 'Jhon';

//删除
obj['name']  = null

//访问
const name = obj['name'] ;
```
**使用中括号语法是需要注意一种初学者常犯错误情况：**

```
//注意，以下代码为错误
obj[name] = 'Tom'；//报错
```
我们来分析，上述代码的错误原因`obj[name] = 10；`
这个代码中，因为之前没有定义name(**所有的变量必须先定义后使用**)，所以代码运行过程中，运行环境不知道name是什么东西，从而报错。

点语法和中括号使用原则：优先使用点语法，在不能使用点语法的情况下再使用中括号，有两种情况下无法使用点语法：

* 对象中键值对中的键有特殊字符
* 使用变量的值访问对象键值对

```
const obj = {
	name:'Tom',
	'per.age':10,//key只能够包含特殊字符
}

//正确
obj.name = 'Jhon';
//错误
obj.per.age = 1;//error
obj.'per.age' = 2;//error
obj[per.age] = 3;//error
//正确
obj['per.age'] = 4;
const age = 'per.age';
obj[age] = 5
```


## 7.4 对象比较

在JavaScript中，对象与数值的储存方法不同。

首先看两段代码

```
const name1 = 'Tom';
const name2 = 'Tom';

if(name1 === name2){
	console.log('相等');
} else {
	console.log('不等');
}
```

```
c

if(person1 === person2){
	console.log('相等');
} else {
	console.log('不等');
}
```
思考一下以上代码输出结果：

* 第一段代码输出：相等
* 第二段代码输出：不等

但大部分同学都应该认为，两个输出都是相等。为了解释这个问题，我们先引入一个新的概念：**引用**

我们看下面代码

```
const a = 1;
```
对于这段代码，我们可以这样理解：a是一个变量，通过赋值操作，将1这个值写入到这个变量。

但对于设计对象的代码：

```
const obj = {
	name:'Tom',
}
```
理解起来稍费劲，因为这是obj存储的不是一个对象的值，而是一个对象的引用，

对于引用，我用一个生活中的案例来讲解：

例如我们在银行办一张银行卡，把钱存到银行卡里。这是我们通常的理解。但实际上的操作不太一样。在银行办一张银行卡的实际过程为，在银行开设了一个账号，然后用一张银行卡与这个账号关联，将钱存进银行卡实际是把钱通过银行卡存入相关联的账号内。所以，即使你把银行卡拆了，也不可能在银行卡内找到你存入的钱，因为钱都在账号里面。这个银行卡就相当于你账户的引用，账户就相当于对象，账户里的钱就相当于对象中的值。

有了这个概念，我们对对象的比较就不难理解了。

对对象的比较，都是比较其引用是否相同，或者可以理解成，银行卡是否管理的同一个账户。

我们看这段代码

```
const person1 = {
	name:'Tom',
};
const person2 = {
	name:'Tom',
};

```
这段代码中，person1是第一个大括号对象的引用，person2是第二个大括号对象的引用。这两个引用变量指向的是不同的大括号，所以比较结果自然是不同。

而非对象引用的变量其比较是变量内所存储的值的比较。

那同样定义一个变量，这个变量什么时候是对象的引用什么时候是普通变量呢？

我们只需要记住以下情况既可以，在以下情况中变量为普通变量不是引用，除此之外都为引用变量

* 变量储存数值，例如 const a = 1;
* 变量储存字符串，例如 const a = 'hello';
* 变量储存bool值，例如 const a = true;


## 7.5 对象复制

因JavaScript中对象储存类型与值不同，所以其复制过程也不一致。

先明确一下复制的概念。看下面代码

```
let a = 1;
//将a的值复制到b中
let b = a;
a = 2;
console.log(b);
```
复制操作一旦结束，源数据和目标数据应该就没有关系了。也就是说，上面代码中，我虽然改变了a变量的值，但是这个改变不会影响b变量，因为复制操作已经结束。

但我们看下面代码

```
const obj1 = {
	name:'Tom',
}
const obj2 = obj1;
obj1.name = 'Jhon';
console.log(obj2.name);//打印结果为Jhon
```
通过打印结果，我们发现，在对象复制过程结束以后，对源数据进行的修改操作仍然会影响复制后的数据，这种情况我们称之为**浅复制**。

在对象复制过程中，通过赋值语句操作的都是浅复制，因为obj1是一个引用变量，对引用变量的复制操作不能够创建新的对象，只是为对象增加一个引用，也就是说obj1和obj2都指向同一个对象，所以才会产生操作源数据影响复制后的数据的现象。

与浅复制相对于的是**深复制**的概念，在深复制后，修改源数据，复制对象不会发生变化。

```
const obj1 = {
	name:'Tom',
}
//使用Object.assign()对对象进行深复制
const obj2 = Object.assign({},obj1);
obj1.name = 'Jhon';
console.log(obj2.name);
```
经过浅复制的两个对象在比较中为相等，深复制的两个对象为不等。


## 7.6 对象数据结构

在处理复杂数据是，通常需要对对象和数组进行嵌套使用。

例如我们看一个通过网络请求回来的数据

```
{
	success:true,
	data:[
		{	
			id:1234,
			text:'这是一条测试消息1',
			images:[
				{
					id:100001
					url:'1.png',
				},
				{
					id:100002
					url:'2.png',
				},
			],
			user:{
				id:1001,
				name:'测试用户1',
				image:'user1.png',
			},
		},
		{	
			id:1239,
			text:'这是一条测试消息2',
			images:[
				{
					id:100003
					url:'3.png',
				},
				{
					id:100004
					url:'4.png',
				},
			],
			user:{
				id:1002,
				name:'测试用户2',
				image:'user2.png',
			},
		}
	]
}
```

```
{
	success:false,
	message:'参数错误',
}
```
对这样第一个复合嵌套的对象，能够准确访问其每一个属性值。

对这样复合嵌套对象，我们首先需要确定两个概念

* 消息模板
* 元数据

在本对象中：

```
{
	success:
	data:
	message:
}
```
就是消息模板，也是最外层对象，通过`success`字段表示请求结果，如成功通过`data`字段返回数据，如失败通过`message`字段返回错误原因。

```
{	
	id:1234,
	text:'这是一条测试消息1',
	images:[
		{
			id:100001
			url:'1.png',
		},
		{
			id:100002
			url:'2.png',
		},
	],
	user:{
		id:1001,
		name:'测试用户1',
		image:'user1.png',
	},
}
```
这是Message元数据

data字段对于应数组，数组中每一个元素都是一个Message元数据。元数据的对象中，所有的key都是固定并且已知的。value值未知。

且元数据之间也存在嵌套关系，分析本案例，可以得出，有3中元数据

```
//Image元数据
{
	id:100002
	url:'2.png',
}
```

```
//User元素数据
{
	id:1001,
	name:'测试用户1',
	image:'user1.png',
}
```
还有我们上面分析的Message元数据，而且Message元数据中嵌套多个Image元数据和一个User元数据。

## 7.7 对象编码与解码

JSON是JavaScript Object Notation的缩写，它是一种数据交换格式。

在JSON中，一共就一下几种数据类型：

* number：和JavaScript的 `number`完全一致；
* boolean：就是JavaScript的`true`或`false`；
* string：就是JavaScript的`string`；
* null：就是JavaScript的`null`；
* array：就是JavaScript的`Array`表示方式——`[]`；
* object：就是JavaScript的`{ ... }`表示方式。

上面的数据可以任意嵌套和组合。

由于JSON非常简单，很快就风靡Web世界，并且成为ECMA标准。几乎所有编程语言都有解析JSON的库，而在JavaScript中，我们可以直接使用JSON，因为JavaScript内置了JSON的解析。

把任何JavaScript对象变成JSON，就是把这个对象序列化成一个JSON格式的字符串，这样才能够通过网络传递给其他计算机。

如果我们收到一个JSON格式的字符串，只需要把它反序列化成一个JavaScript对象，就可以在JavaScript中直接使用这个对象了。

#### 序列化

JSON序列化是指，将JavaScript中的对象转换为JSON格式的字符串。

例如我们在数据库中查询到了一个人的信息，需要把这个信息通过网络传递到前台的App进行显示，这时，我们需要将此对象进行JSON序列化，转换成JSON字符串才能进行传输。

```
const person = {
name:'Tom',
age:10,
tel:'18612341234'
}

//JSON序列化使用JavaScript语言中自带的JSON解析器的stringify方法
const jsonData = JSON.stringify(person);
console.log(jsonData);//字符串：'{"name":"Tom","age":11,"tel":'1861234123'}'
```

#### 反序列化

JSON反序列化也叫JSON解析。

拿到一个JSON格式的字符串，我们直接用`JSON.parse()`把它变成一个JavaScript对象。

一般来说，JSON格式的字符串都是通过网络请求获取

在此，我们为了测试JSON反序列化的功能，手写一个本地的JSON格式字符串。

```
const jsonData = '{"name":"Tom","age":11,"tel":18612341234}';
const person = JSON.parse(jsonData);
console.log(person.name);//结果为Tom
```

## 7.8 对象的扩展

### 7.8.1 属性的简洁表示法

ES6 允许直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```javascript
const name = 'Tom';
const person = {name};
console.log(person); // {name: 'Tom'}

// 等同于
const person = {name: name};
```

上面代码表明，ES6 允许在对象之中，直接写变量。这时，属性名为变量名, 属性值为变量的值。下面是另一个例子。

```javascript
function f(x, y) {
  return {x, y};
}

// 等同于

function f(x, y) {
  return {x: x, y: y};
}

f(1, 2) // Object {x: 1, y: 2}
```

除了属性简写，方法也可以简写。

```javascript
const obj = {
  sayHi() {
    return "Hello!";
  }
};

// 等同于

const obj = {
  sayHi: function() {
    return "Hello!";
  }
};
```

下面是一个实际的例子。

```javascript
let age = 20;

const Person = {

  name: '张三',

  //等同于age: age
  age,

  // 等同于hello: function ()...
  hello() { console.log('我的名字是', this.name); }

};
```

这种写法用于函数的返回值，将会非常方便。

```javascript
function getPoint() {
  const x = 1;
  const y = 10;
  return {x, y};
}

getPoint()
// {x:1, y:10}
```


### 7.8.2 属性名表达式

JavaScript 定义对象的属性，有两种方法。

```javascript
// 方法一
obj.foo = true;

// 方法二
obj['a' + 'bc'] = 123;
```

上面代码的方法一是直接用标识符作为属性名，方法二是用表达式作为属性名，这时要将表达式放在方括号之内。

但是，如果使用字面量方式定义对象（使用大括号），在 ES5 中只能使用方法一（标识符）定义属性。

```javascript
var obj = {
  foo: true,
  abc: 123
};
```

ES6 允许字面量定义对象时，用方法二（表达式）作为对象的属性名，即把表达式放在方括号内。

```javascript
let propKey = 'foo';

let obj = {
  [propKey]: true,
  ['a' + 'bc']: 123
};
```

下面是另一个例子。

```javascript
let lastWord = 'last word';

const a = {
  'first word': 'hello',
  [lastWord]: 'world'
};

a['first word'] // "hello"
a[lastWord] // "world"
a['last word'] // "world"
```

表达式还可以用于定义方法名。

```javascript
let obj = {
  ['h' + 'ello']() {
    return 'hi';
  }
};

obj.hello() // hi
```

注意，属性名表达式与简洁表示法，不能同时使用，会报错。

```javascript
// 报错
const foo = 'bar';
const bar = 'abc';
const baz = { [foo] };

// 正确
const foo = 'bar';
const baz = { [foo]: 'abc'};
```

注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串`[object Object]`，这一点要特别小心。

```javascript
const keyA = {a: 1};
const keyB = {b: 2};

const myObject = {
  [keyA]: 'valueA',
  [keyB]: 'valueB'
};

myObject // Object {[object Object]: "valueB"}
```

上面代码中，`[keyA]`和`[keyB]`得到的都是`[object Object]`，所以`[keyB]`会把`[keyA]`覆盖掉，而`myObject`最后只有一个`[object Object]`属性。

### 7.8.3 方法的 name 属性

函数的`name`属性，返回函数名。对象方法也是函数，因此也有`name`属性。

```javascript
const person = {
  sayName() {
    console.log('hello!');
  },
};

person.sayName.name   // "sayName"
```

上面代码中，方法的`name`属性返回函数名（即方法名）。

如果对象的方法使用了取值函数（`getter`）和存值函数（`setter`），则`name`属性不是在该方法上面，而是该方法的属性的描述对象的`get`和`set`属性上面，返回值是方法名前加上`get`和`set`。

```javascript
const obj = {
  get foo() {},
  set foo(x) {}
};

obj.foo.name
// TypeError: Cannot read property 'name' of undefined

const descriptor = Object.getOwnPropertyDescriptor(obj, 'foo');

descriptor.get.name // "get foo"
descriptor.set.name // "set foo"
```

有两种特殊情况：`bind`方法创造的函数，`name`属性返回`bound`加上原函数的名字；`Function`构造函数创造的函数，`name`属性返回`anonymous`。

```javascript
(new Function()).name // "anonymous"

var doSomething = function() {
  // ...
};
doSomething.bind().name // "bound doSomething"
```

如果对象的方法是一个 Symbol 值，那么`name`属性返回的是这个 Symbol 值的描述。

```javascript
const key1 = Symbol('description');
const key2 = Symbol();
let obj = {
  [key1]() {},
  [key2]() {},
};
obj[key1].name // "[description]"
obj[key2].name // ""
```

上面代码中，`key1`对应的 Symbol 值有描述，`key2`没有。

### 7.8.4 Object.is()

ES5 比较两个值是否相等，只有两个运算符：相等运算符（`==`）和严格相等运算符（`===`）。它们都有缺点，前者会自动转换数据类型，后者的`NaN`不等于自身，以及`+0`等于`-0`。JavaScript 缺乏一种运算，在所有环境中，只要两个值是一样的，它们就应该相等。

ES6 提出“Same-value equality”（同值相等）算法，用来解决这个问题。`Object.is`就是部署这个算法的新方法。它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。

```javascript
Object.is('foo', 'foo')
// true
Object.is({}, {})
// false
```

不同之处只有两个：一是`+0`不等于`-0`，二是`NaN`等于自身。

```javascript
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

ES5 可以通过下面的代码，部署`Object.is`。

```javascript
Object.defineProperty(Object, 'is', {
  value: function(x, y) {
    if (x === y) {
      // 针对+0 不等于 -0的情况
      return x !== 0 || 1 / x === 1 / y;
    }
    // 针对NaN的情况
    return x !== x && y !== y;
  },
  configurable: true,
  enumerable: false,
  writable: true
});
```

### 7.8.5 Object.assign()


`Object.assign`方法用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）。

```javascript
const target = { a: 1 };

const source1 = { b: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

`Object.assign`方法的第一个参数是目标对象，后面的参数都是源对象。

注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性。

```javascript
const target = { a: 1, b: 1 };

const source1 = { b: 2, c: 2 };
const source2 = { c: 3 };

Object.assign(target, source1, source2);
target // {a:1, b:2, c:3}
```

如果只有一个参数，`Object.assign`会直接返回该参数。

```javascript
const obj = {a: 1};
Object.assign(obj) === obj // true
```

如果该参数不是对象，则会先转成对象，然后返回。

```javascript
typeof Object.assign(2) // "object"
```

由于`undefined`和`null`无法转成对象，所以如果它们作为参数，就会报错。

```javascript
Object.assign(undefined) // 报错
Object.assign(null) // 报错
```

如果非对象参数出现在源对象的位置（即非首参数），那么处理规则有所不同。首先，这些参数都会转成对象，如果无法转成对象，就会跳过。这意味着，如果`undefined`和`null`不在首参数，就不会报错。

```javascript
let obj = {a: 1};
Object.assign(obj, undefined) === obj // true
Object.assign(obj, null) === obj // true
```

其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果。

```javascript
const v1 = 'abc';
const v2 = true;
const v3 = 10;

const obj = Object.assign({}, v1, v2, v3);
console.log(obj); // { "0": "a", "1": "b", "2": "c" }
```

上面代码中，`v1`、`v2`、`v3`分别是字符串、布尔值和数值，结果只有字符串合入目标对象（以字符数组的形式），数值和布尔值都会被忽略。这是因为只有字符串的包装对象，会产生可枚举属性。

```javascript
Object(true) // {[[PrimitiveValue]]: true}
Object(10)  //  {[[PrimitiveValue]]: 10}
Object('abc') // {0: "a", 1: "b", 2: "c", length: 3, [[PrimitiveValue]]: "abc"}
```

上面代码中，布尔值、数值、字符串分别转成对应的包装对象，可以看到它们的原始值都在包装对象的内部属性`[[PrimitiveValue]]`上面，这个属性是不会被`Object.assign`拷贝的。只有字符串的包装对象，会产生可枚举的实义属性，那些属性则会被拷贝。

`Object.assign`拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（`enumerable: false`）。

```javascript
Object.assign({b: 'c'},
  Object.defineProperty({}, 'invisible', {
    enumerable: false,
    value: 'hello'
  })
)
// { b: 'c' }
```

上面代码中，`Object.assign`要拷贝的对象只有一个不可枚举属性`invisible`，这个属性并没有被拷贝进去。

属性名为 Symbol 值的属性，也会被`Object.assign`拷贝。

```javascript
Object.assign({ a: 'b' }, { [Symbol('c')]: 'd' })
// { a: 'b', Symbol(c): 'd' }
```

#### 注意点

**（1）浅拷贝**

`Object.assign`方法实行的是浅拷贝，而不是深拷贝。也就是说，如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用。

```javascript
const obj1 = {a: {b: 1}};
const obj2 = Object.assign({}, obj1);

obj1.a.b = 2;
obj2.a.b // 2
```

上面代码中，源对象`obj1`的`a`属性的值是一个对象，`Object.assign`拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面。

**（2）同名属性的替换**

对于这种嵌套的对象，一旦遇到同名属性，`Object.assign`的处理方法是替换，而不是添加。

```javascript
const target = { a: { b: 'c', d: 'e' } }
const source = { a: { b: 'hello' } }
Object.assign(target, source)
// { a: { b: 'hello' } }
```

上面代码中，`target`对象的`a`属性被`source`对象的`a`属性整个替换掉了，而不会得到`{ a: { b: 'hello', d: 'e' } }`的结果。这通常不是开发者想要的，需要特别小心。

一些函数库提供`Object.assign`的定制版本（比如 Lodash 的`_.defaultsDeep`方法），可以得到深拷贝的合并。

**（3）数组的处理**

`Object.assign`可以用来处理数组，但是会把数组视为对象。

```javascript
Object.assign([1, 2, 3], [4, 5])
// [4, 5, 3]
```

上面代码中，`Object.assign`把数组视为属性名为0、1、2的对象，因此源数组的0号属性`4`覆盖了目标数组的0号属性`1`。

**（4）取值函数的处理**

`Object.assign`只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制。

```javascript
const source = {
  get foo() { return 1 }
};
const target = {};

Object.assign(target, source)
// { foo: 1 }
```

上面代码中，`source`对象的`foo`属性是一个取值函数，`Object.assign`不会复制这个取值函数，只会拿到值以后，将这个值复制过去。

#### 常见用途

`Object.assign`方法有很多用处。

**（1）为对象添加属性**

```javascript
class Point {
  constructor(x, y) {
    Object.assign(this, {x, y});
  }
}
```

上面方法通过`Object.assign`方法，将`x`属性和`y`属性添加到`Point`类的对象实例。

**（2）为对象添加方法**

```javascript
Object.assign(SomeClass.prototype, {
  someMethod(arg1, arg2) {
    ···
  },
  anotherMethod() {
    ···
  }
});

// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
  ···
};
SomeClass.prototype.anotherMethod = function () {
  ···
};
```

上面代码使用了对象属性的简洁表示法，直接将两个函数放在大括号中，再使用`assign`方法添加到`SomeClass.prototype`之中。

**（3）克隆对象**

```javascript
function clone(origin) {
  return Object.assign({}, origin);
}
```

上面代码将原始对象拷贝到一个空对象，就得到了原始对象的克隆。

不过，采用这种方法克隆，只能克隆原始对象自身的值，不能克隆它继承的值。如果想要保持继承链，可以采用下面的代码。

```javascript
function clone(origin) {
  let originProto = Object.getPrototypeOf(origin);
  return Object.assign(Object.create(originProto), origin);
}
```

**（4）合并多个对象**

将多个对象合并到某个对象。

```javascript
const merge =
  (target, ...sources) => Object.assign(target, ...sources);
```

如果希望合并后返回一个新对象，可以改写上面函数，对一个空对象合并。

```javascript
const merge =
  (...sources) => Object.assign({}, ...sources);
```


### 7.8.6 属性的可枚举性和遍历

#### 可枚举性

对象的每个属性都有一个描述对象（Descriptor），用来控制该属性的行为。`Object.getOwnPropertyDescriptor`方法可以获取该属性的描述对象。

```javascript
let obj = { foo: 123 };
Object.getOwnPropertyDescriptor(obj, 'foo')
//  {
//    value: 123,
//    writable: true,
//    enumerable: true,
//    configurable: true
//  }
```

描述对象的`enumerable`属性，称为”可枚举性“，如果该属性为`false`，就表示某些操作会忽略当前属性。

目前，有四个操作会忽略`enumerable`为`false`的属性。

- `for...in`循环：只遍历对象自身的和继承的可枚举的属性。
- `Object.keys()`：返回对象自身的所有可枚举的属性的键名。
- `JSON.stringify()`：只串行化对象自身的可枚举的属性。
- `Object.assign()`： 忽略`enumerable`为`false`的属性，只拷贝对象自身的可枚举的属性。

这四个操作之中，前三个是 ES5 就有的，最后一个`Object.assign()`是 ES6 新增的。其中，只有`for...in`会返回继承的属性，其他三个方法都会忽略继承的属性，只处理对象自身的属性。实际上，引入“可枚举”（`enumerable`）这个概念的最初目的，就是让某些属性可以规避掉`for...in`操作，不然所有内部属性和方法都会被遍历到。比如，对象原型的`toString`方法，以及数组的`length`属性，就通过“可枚举性”，从而避免被`for...in`遍历到。

```javascript
Object.getOwnPropertyDescriptor(Object.prototype, 'toString').enumerable
// false

Object.getOwnPropertyDescriptor([], 'length').enumerable
// false
```

上面代码中，`toString`和`length`属性的`enumerable`都是`false`，因此`for...in`不会遍历到这两个继承自原型的属性。

另外，ES6 规定，所有 Class 的原型的方法都是不可枚举的。

```javascript
Object.getOwnPropertyDescriptor(class {foo() {}}.prototype, 'foo').enumerable
// false
```

总的来说，操作中引入继承的属性会让问题复杂化，大多数时候，我们只关心对象自身的属性。所以，尽量不要用`for...in`循环，而用`Object.keys()`代替。

#### 属性的遍历

ES6 一共有5种方法可以遍历对象的属性。

**（1）for...in**

`for...in`循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。

**（2）Object.keys(obj)**

`Object.keys`返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。

**（3）Object.getOwnPropertyNames(obj)**

`Object.getOwnPropertyNames`返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。

**（4）Object.getOwnPropertySymbols(obj)**

`Object.getOwnPropertySymbols`返回一个数组，包含对象自身的所有 Symbol 属性的键名。

**（5）Reflect.ownKeys(obj)**

`Reflect.ownKeys`返回一个数组，包含对象自身的所有键名，不管键名是 Symbol 或字符串，也不管是否可枚举。

以上的5种方法遍历对象的键名，都遵守同样的属性遍历的次序规则。

- 首先遍历所有数值键，按照数值升序排列。
- 其次遍历所有字符串键，按照加入时间升序排列。
- 最后遍历所有 Symbol 键，按照加入时间升序排列。

```javascript
Reflect.ownKeys({ [Symbol()]:0, b:0, 10:0, 2:0, a:0 })
// ['2', '10', 'b', 'a', Symbol()]
```

上面代码中，`Reflect.ownKeys`方法返回一个数组，包含了参数对象的所有属性。这个数组的属性次序是这样的，首先是数值属性`2`和`10`，其次是字符串属性`b`和`a`，最后是 Symbol 属性。

### 7.8.7 Object.getOwnPropertyDescriptors()

前面说过，`Object.getOwnPropertyDescriptor`方法会返回某个对象属性的描述对象（descriptor）。ES2017 引入了`Object.getOwnPropertyDescriptors`方法，返回指定对象所有自身属性（非继承属性）的描述对象。

```javascript
const obj = {
  foo: 123,
  get bar() { return 'abc' }
};

Object.getOwnPropertyDescriptors(obj)
// { foo:
//    { value: 123,
//      writable: true,
//      enumerable: true,
//      configurable: true },
//   bar:
//    { get: [Function: bar],
//      set: undefined,
//      enumerable: true,
//      configurable: true } }
```

上面代码中，`Object.getOwnPropertyDescriptors`方法返回一个对象，所有原对象的属性名都是该对象的属性名，对应的属性值就是该属性的描述对象。

该方法的实现非常容易。

```javascript
function getOwnPropertyDescriptors(obj) {
  const result = {};
  for (let key of Reflect.ownKeys(obj)) {
    result[key] = Object.getOwnPropertyDescriptor(obj, key);
  }
  return result;
}
```

该方法的引入目的，主要是为了解决`Object.assign()`无法正确拷贝`get`属性和`set`属性的问题。

```javascript
const source = {
  set foo(value) {
    console.log(value);
  }
};

const target1 = {};
Object.assign(target1, source);

Object.getOwnPropertyDescriptor(target1, 'foo')
// { value: undefined,
//   writable: true,
//   enumerable: true,
//   configurable: true }
```

上面代码中，`source`对象的`foo`属性的值是一个赋值函数，`Object.assign`方法将这个属性拷贝给`target1`对象，结果该属性的值变成了`undefined`。这是因为`Object.assign`方法总是拷贝一个属性的值，而不会拷贝它背后的赋值方法或取值方法。

这时，`Object.getOwnPropertyDescriptors`方法配合`Object.defineProperties`方法，就可以实现正确拷贝。

```javascript
const source = {
  set foo(value) {
    console.log(value);
  }
};

const target2 = {};
Object.defineProperties(target2, Object.getOwnPropertyDescriptors(source));
Object.getOwnPropertyDescriptor(target2, 'foo')
// { get: undefined,
//   set: [Function: foo],
//   enumerable: true,
//   configurable: true }
```

上面代码中，两个对象合并的逻辑可以写成一个函数。

```javascript
const shallowMerge = (target, source) => Object.defineProperties(
  target,
  Object.getOwnPropertyDescriptors(source)
);
```

`Object.getOwnPropertyDescriptors`方法的另一个用处，是配合`Object.create`方法，将对象属性克隆到一个新对象。这属于浅拷贝。

```javascript
const clone = Object.create(Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj));

// 或者

const shallowClone = (obj) => Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
);
```

上面代码会克隆对象`obj`。

另外，`Object.getOwnPropertyDescriptors`方法可以实现一个对象继承另一个对象。以前，继承另一个对象，常常写成下面这样。

```javascript
const obj = {
  __proto__: prot,
  foo: 123,
};
```

ES6 规定`__proto__`只有浏览器要部署，其他环境不用部署。如果去除`__proto__`，上面代码就要改成下面这样。

```javascript
const obj = Object.create(prot);
obj.foo = 123;

// 或者

const obj = Object.assign(
  Object.create(prot),
  {
    foo: 123,
  }
);
```

有了`Object.getOwnPropertyDescriptors`，我们就有了另一种写法。

```javascript
const obj = Object.create(
  prot,
  Object.getOwnPropertyDescriptors({
    foo: 123,
  })
);
```

`Object.getOwnPropertyDescriptors`也可以用来实现 Mixin（混入）模式。

```javascript
let mix = (object) => ({
  with: (...mixins) => mixins.reduce(
    (c, mixin) => Object.create(
      c, Object.getOwnPropertyDescriptors(mixin)
    ), object)
});

// multiple mixins example
let a = {a: 'a'};
let b = {b: 'b'};
let c = {c: 'c'};
let d = mix(c).with(a, b);

d.c // "c"
d.b // "b"
d.a // "a"
```

上面代码返回一个新的对象`d`，代表了对象`a`和`b`被混入了对象`c`的操作。

出于完整性的考虑，`Object.getOwnPropertyDescriptors`进入标准以后，以后还会新增`Reflect.getOwnPropertyDescriptors`方法。

### 7.8.8 `__proto__`属性

JavaScript 语言的对象继承是通过原型链实现的。ES6 提供了更多原型对象的操作方法。


`__proto__`属性（前后各两个下划线），用来读取或设置当前对象的`prototype`对象。目前，所有浏览器（包括 IE11）都部署了这个属性。

```javascript
// es6 的写法
const obj = {
  method: function() { ... }
};
obj.__proto__ = someOtherObj;

// es5 的写法
var obj = Object.create(someOtherObj);
obj.method = function() { ... };
```

该属性没有写入 ES6 的正文，而是写入了附录，原因是`__proto__`前后的双下划线，说明它本质上是一个内部属性，而不是一个正式的对外的 API，只是由于浏览器广泛支持，才被加入了 ES6。标准明确规定，只有浏览器必须部署这个属性，其他运行环境不一定需要部署，而且新的代码最好认为这个属性是不存在的。因此，无论从语义的角度，还是从兼容性的角度，都不要使用这个属性，而是使用下面的`Object.setPrototypeOf()`（写操作）、`Object.getPrototypeOf()`（读操作）、`Object.create()`（生成操作）代替。

实现上，`__proto__`调用的是`Object.prototype.__proto__`，具体实现如下。

```javascript
Object.defineProperty(Object.prototype, '__proto__', {
  get() {
    let _thisObj = Object(this);
    return Object.getPrototypeOf(_thisObj);
  },
  set(proto) {
    if (this === undefined || this === null) {
      throw new TypeError();
    }
    if (!isObject(this)) {
      return undefined;
    }
    if (!isObject(proto)) {
      return undefined;
    }
    let status = Reflect.setPrototypeOf(this, proto);
    if (!status) {
      throw new TypeError();
    }
  },
});

function isObject(value) {
  return Object(value) === value;
}
```

如果一个对象本身部署了`__proto__`属性，该属性的值就是对象的原型。

```javascript
Object.getPrototypeOf({ __proto__: null })
// null
```

#### Object.setPrototypeOf()

`Object.setPrototypeOf`方法的作用与`__proto__`相同，用来设置一个对象的`prototype`对象，返回参数对象本身。它是 ES6 正式推荐的设置原型对象的方法。

```javascript
// 格式
Object.setPrototypeOf(object, prototype)

// 用法
const o = Object.setPrototypeOf({}, null);
```

该方法等同于下面的函数。

```javascript
function (obj, proto) {
  obj.__proto__ = proto;
  return obj;
}
```

下面是一个例子。

```javascript
let proto = {};
let obj = { x: 10 };
Object.setPrototypeOf(obj, proto);

proto.y = 20;
proto.z = 40;

obj.x // 10
obj.y // 20
obj.z // 40
```

上面代码将`proto`对象设为`obj`对象的原型，所以从`obj`对象可以读取`proto`对象的属性。

如果第一个参数不是对象，会自动转为对象。但是由于返回的还是第一个参数，所以这个操作不会产生任何效果。

```javascript
Object.setPrototypeOf(1, {}) === 1 // true
Object.setPrototypeOf('foo', {}) === 'foo' // true
Object.setPrototypeOf(true, {}) === true // true
```

由于`undefined`和`null`无法转为对象，所以如果第一个参数是`undefined`或`null`，就会报错。

```javascript
Object.setPrototypeOf(undefined, {})
// TypeError: Object.setPrototypeOf called on null or undefined

Object.setPrototypeOf(null, {})
// TypeError: Object.setPrototypeOf called on null or undefined
```

#### Object.getPrototypeOf()

该方法与`Object.setPrototypeOf`方法配套，用于读取一个对象的原型对象。

```javascript
Object.getPrototypeOf(obj);
```

下面是一个例子。

```javascript
function Rectangle() {
  // ...
}

const rec = new Rectangle();

Object.getPrototypeOf(rec) === Rectangle.prototype
// true

Object.setPrototypeOf(rec, Object.prototype);
Object.getPrototypeOf(rec) === Rectangle.prototype
// false
```

如果参数不是对象，会被自动转为对象。

```javascript
// 等同于 Object.getPrototypeOf(Number(1))
Object.getPrototypeOf(1)
// Number {[[PrimitiveValue]]: 0}

// 等同于 Object.getPrototypeOf(String('foo'))
Object.getPrototypeOf('foo')
// String {length: 0, [[PrimitiveValue]]: ""}

// 等同于 Object.getPrototypeOf(Boolean(true))
Object.getPrototypeOf(true)
// Boolean {[[PrimitiveValue]]: false}

Object.getPrototypeOf(1) === Number.prototype // true
Object.getPrototypeOf('foo') === String.prototype // true
Object.getPrototypeOf(true) === Boolean.prototype // true
```

如果参数是`undefined`或`null`，它们无法转为对象，所以会报错。

```javascript
Object.getPrototypeOf(null)
// TypeError: Cannot convert undefined or null to object

Object.getPrototypeOf(undefined)
// TypeError: Cannot convert undefined or null to object
```


### 7.8.9 Object-Key

ES5 引入了`Object.keys`方法，返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名。

```javascript
var obj = { foo: 'bar', baz: 42 };
Object.keys(obj)
// ["foo", "baz"]
```

ES2017 [引入](https://github.com/tc39/proposal-object-values-entries)了跟`Object.keys`配套的`Object.values`和`Object.entries`，作为遍历一个对象的补充手段，供`for...of`循环使用。

```javascript
let {keys, values, entries} = Object;
let obj = { a: 1, b: 2, c: 3 };

for (let key of keys(obj)) {
  console.log(key); // 'a', 'b', 'c'
}

for (let value of values(obj)) {
  console.log(value); // 1, 2, 3
}

for (let [key, value] of entries(obj)) {
  console.log([key, value]); // ['a', 1], ['b', 2], ['c', 3]
}
```

#### Object.values()

`Object.values`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

```javascript
const obj = { foo: 'bar', baz: 42 };
Object.values(obj)
// ["bar", 42]
```

返回数组的成员顺序，与本章的《属性的遍历》部分介绍的排列规则一致。

```javascript
const obj = { 100: 'a', 2: 'b', 7: 'c' };
Object.values(obj)
// ["b", "c", "a"]
```

上面代码中，属性名为数值的属性，是按照数值大小，从小到大遍历的，因此返回的顺序是`b`、`c`、`a`。

`Object.values`只返回对象自身的可遍历属性。

```javascript
const obj = Object.create({}, {p: {value: 42}});
Object.values(obj) // []
```

上面代码中，`Object.create`方法的第二个参数添加的对象属性（属性`p`），如果不显式声明，默认是不可遍历的，因为`p`的属性描述对象的`enumerable`默认是`false`，`Object.values`不会返回这个属性。只要把`enumerable`改成`true`，`Object.values`就会返回属性`p`的值。

```javascript
const obj = Object.create({}, {p:
  {
    value: 42,
    enumerable: true
  }
});
Object.values(obj) // [42]
```

`Object.values`会过滤属性名为 Symbol 值的属性。

```javascript
Object.values({ [Symbol()]: 123, foo: 'abc' });
// ['abc']
```

如果`Object.values`方法的参数是一个字符串，会返回各个字符组成的一个数组。

```javascript
Object.values('foo')
// ['f', 'o', 'o']
```

上面代码中，字符串会先转成一个类似数组的对象。字符串的每个字符，就是该对象的一个属性。因此，`Object.values`返回每个属性的键值，就是各个字符组成的一个数组。

如果参数不是对象，`Object.values`会先将其转为对象。由于数值和布尔值的包装对象，都不会为实例添加非继承的属性。所以，`Object.values`会返回空数组。

```javascript
Object.values(42) // []
Object.values(true) // []
```

#### Object.entries

`Object.entries`方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

```javascript
const obj = { foo: 'bar', baz: 42 };
Object.entries(obj)
// [ ["foo", "bar"], ["baz", 42] ]
```

除了返回值不一样，该方法的行为与`Object.values`基本一致。

如果原对象的属性名是一个 Symbol 值，该属性会被忽略。

```javascript
Object.entries({ [Symbol()]: 123, foo: 'abc' });
// [ [ 'foo', 'abc' ] ]
```

上面代码中，原对象有两个属性，`Object.entries`只输出属性名非 Symbol 值的属性。将来可能会有`Reflect.ownEntries()`方法，返回对象自身的所有属性。

`Object.entries`的基本用途是遍历对象的属性。

```javascript
let obj = { one: 1, two: 2 };
for (let [k, v] of Object.entries(obj)) {
  console.log(
    `${JSON.stringify(k)}: ${JSON.stringify(v)}`
  );
}
// "one": 1
// "two": 2
```

`Object.entries`方法的另一个用处是，将对象转为真正的`Map`结构。

```javascript
const obj = { foo: 'bar', baz: 42 };
const map = new Map(Object.entries(obj));
map // Map { foo: "bar", baz: 42 }
```

自己实现`Object.entries`方法，非常简单。

```javascript
// Generator函数的版本
function* entries(obj) {
  for (let key of Object.keys(obj)) {
    yield [key, obj[key]];
  }
}

// 非Generator函数的版本
function entries(obj) {
  let arr = [];
  for (let key of Object.keys(obj)) {
    arr.push([key, obj[key]]);
  }
  return arr;
}
```

### 7.8.10 对象的扩展运算符

之前内容已经介绍过扩展运算符（`...`）。

```javascript
const [a, ...b] = [1, 2, 3];
a // 1
b // [2, 3]
```

ES2017 将这个运算符[引入](https://github.com/sebmarkbage/ecmascript-rest-spread)了对象。

**（1）解构赋值**

对象的解构赋值用于从一个对象取值，相当于将所有可遍历的、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面。

```javascript
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 4 }
```

上面代码中，变量`z`是解构赋值所在的对象。它获取等号右边的所有尚未读取的键（`a`和`b`），将它们连同值一起拷贝过来。

由于解构赋值要求等号右边是一个对象，所以如果等号右边是`undefined`或`null`，就会报错，因为它们无法转为对象。

```javascript
let { x, y, ...z } = null; // 运行时错误
let { x, y, ...z } = undefined; // 运行时错误
```

解构赋值必须是最后一个参数，否则会报错。

```javascript
let { ...x, y, z } = obj; // 句法错误
let { x, ...y, ...z } = obj; // 句法错误
```

上面代码中，解构赋值不是最后一个参数，所以会报错。

注意，解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数）、那么解构赋值拷贝的是这个值的引用，而不是这个值的副本。

```javascript
let obj = { a: { b: 1 } };
let { ...x } = obj;
obj.a.b = 2;
x.a.b // 2
```

上面代码中，`x`是解构赋值所在的对象，拷贝了对象`obj`的`a`属性。`a`属性引用了一个对象，修改这个对象的值，会影响到解构赋值对它的引用。

另外，扩展运算符的解构赋值，不能复制继承自原型对象的属性。

```javascript
let o1 = { a: 1 };
let o2 = { b: 2 };
o2.__proto__ = o1;
let { ...o3 } = o2;
o3 // { b: 2 }
o3.a // undefined
```

上面代码中，对象`o3`复制了`o2`，但是只复制了`o2`自身的属性，没有复制它的原型对象`o1`的属性。

下面是另一个例子。

```javascript
const o = Object.create({ x: 1, y: 2 });
o.z = 3;

let { x, ...{ y, z } } = o;
x // 1
y // undefined
z // 3
```

上面代码中，变量`x`是单纯的解构赋值，所以可以读取对象`o`继承的属性；变量`y`和`z`是扩展运算符的解构赋值，只能读取对象`o`自身的属性，所以变量`z`可以赋值成功，变量`y`取不到值。

解构赋值的一个用处，是扩展某个函数的参数，引入其他操作。

```javascript
function baseFunction({ a, b }) {
  // ...
}
function wrapperFunction({ x, y, ...restConfig }) {
  // 使用x和y参数进行操作
  // 其余参数传给原始函数
  return baseFunction(restConfig);
}
```

上面代码中，原始函数`baseFunction`接受`a`和`b`作为参数，函数`wrapperFunction`在`baseFunction`的基础上进行了扩展，能够接受多余的参数，并且保留原始函数的行为。

**（2）扩展运算符**

扩展运算符（`...`）用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```javascript
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }
```

这等同于使用`Object.assign`方法。

```javascript
let aClone = { ...a };
// 等同于
let aClone = Object.assign({}, a);
```

上面的例子只是拷贝了对象实例的属性，如果想完整克隆一个对象，还拷贝对象原型的属性，可以采用下面的写法。

```javascript
// 写法一
const clone1 = {
  __proto__: Object.getPrototypeOf(obj),
  ...obj
};

// 写法二
const clone2 = Object.assign(
  Object.create(Object.getPrototypeOf(obj)),
  obj
);
```

上面代码中，写法一的`__proto__`属性在非浏览器的环境不一定部署，因此推荐使用写法二。

扩展运算符可以用于合并两个对象。

```javascript
let ab = { ...a, ...b };
// 等同于
let ab = Object.assign({}, a, b);
```

如果用户自定义的属性，放在扩展运算符后面，则扩展运算符内部的同名属性会被覆盖掉。

```javascript
let aWithOverrides = { ...a, x: 1, y: 2 };
// 等同于
let aWithOverrides = { ...a, ...{ x: 1, y: 2 } };
// 等同于
let x = 1, y = 2, aWithOverrides = { ...a, x, y };
// 等同于
let aWithOverrides = Object.assign({}, a, { x: 1, y: 2 });
```

上面代码中，`a`对象的`x`属性和`y`属性，拷贝到新对象后会被覆盖掉。

这用来修改现有对象部分的属性就很方便了。

```javascript
let newVersion = {
  ...previousVersion,
  name: 'New Name' // Override the name property
};
```

上面代码中，`newVersion`对象自定义了`name`属性，其他属性全部复制自`previousVersion`对象。

如果把自定义属性放在扩展运算符前面，就变成了设置新对象的默认属性值。

```javascript
let aWithDefaults = { x: 1, y: 2, ...a };
// 等同于
let aWithDefaults = Object.assign({}, { x: 1, y: 2 }, a);
// 等同于
let aWithDefaults = Object.assign({ x: 1, y: 2 }, a);
```

与数组的扩展运算符一样，对象的扩展运算符后面可以跟表达式。

```javascript
const obj = {
  ...(x > 1 ? {a: 1} : {}),
  b: 2,
};
```

如果扩展运算符后面是一个空对象，则没有任何效果。

```javascript
{...{}, a: 1}
// { a: 1 }
```

如果扩展运算符的参数是`null`或`undefined`，这两个值会被忽略，不会报错。

```javascript
let emptyObject = { ...null, ...undefined }; // 不报错
```

扩展运算符的参数对象之中，如果有取值函数`get`，这个函数是会执行的。

```javascript
// 并不会抛出错误，因为 x 属性只是被定义，但没执行
let aWithXGetter = {
  ...a,
  get x() {
    throw new Error('not throw yet');
  }
};

// 会抛出错误，因为 x 属性被执行了
let runtimeError = {
  ...a,
  ...{
    get x() {
      throw new Error('throw now');
    }
  }
};
```

## 项目实战：随机摇号系统

### 项目背景

随机摇号系统最早起源于彩票销售。用于随机获取一系列数字。因彩票销售涉及资金较多。所以彩票的摇号系统一直采用的是物理摇号系统。用乒乓球加辅助装置以保证摇号的随机性和公正性。但随着社会的发展，越来越多的资源需要通过摇号的随机性保证分配的公正。例如现在北京小汽车车牌的指标就是通过摇号系统产生。而且现在越来越多的商品房在限售时也会采用摇号方式保证分配的公正性。

### 项目技术要求

系统为一个小型的摇号系统，摇号系统有两种运行模式：

* 号池模式：随机从号池中抽取号码，已抽取的号码不再参与抽取
* 编码模式：随机从0-9中抽取号码，已抽取的号码扔会参与抽取

在系统运行时，严格保证每次抽取动作的随机性。且在多次动作之后仍保证随机性。以保证最后结果为严格随机状态下产生。


### 系统技术设计

在号池模式下，需要考虑号池中号码减少之后仍保证随机过程。设计中需要每次都能够产生范围可控的随机数用来抽取号码，抽取号码之后，需要及时将号码从号池中删除，以满足系统指标要求。

在编码模式中，需要确定抽取次数及每次抽取的随机数即可，实现相对简单。

### 随机数实现

预备知识

```
Math.ceil();  //向上取整。

Math.floor();  //向下取整。

Math.round();  //四舍五入。

Math.random();  //0.0 ~ 1.0 之间的一个伪随机数。【包含0不包含1】 //比如0.8647578968666494

Math.ceil(Math.random()*10);      // 获取从1到10的随机整数 ，取0的概率极小。

Math.round(Math.random());   //可均衡获取0到1的随机整数。

Math.floor(Math.random()*10);  //可均衡获取0到9的随机整数。

Math.round(Math.random()*10);  //基本均衡获取0到10的随机整数，其中获取最小值0和最大值10的几率少一半。

因为结果在0~0.4 为0，0.5到1.4为1...8.5到9.4为9，9.5到9.9为10。所以头尾的分布区间只有其他数字的一半。

```

生成[n,m]的随机整数

```
function randomNum(minNum,maxNum){ 

    return parseInt(Math.random()*(maxNum-minNum+1)+minNum,10); 

} 
```

 过程分析：
 
 Math.random()生成[0,1)的数，所以

Math.random()*5生成{0,5)的数。

通常期望得到整数，所以要对得到的结果处理一下。

parseInt()，Math.floor()，Math.ceil()和Math.round()都可得到整数。

parseInt()和Math.floor()结果都是向下取整。

所以Math.random()*5生成的都是[0,4] 的随机整数。

所以生成[1,max]的随机数，公式如下：

```
// max - 期望的最大值
parseInt(Math.random()*max,10)+1;
Math.floor(Math.random()*max)+1;
Math.ceil(Math.random()*max);
```
所以生成[0,max]到任意数的随机数，公式如下：

```
// max - 期望的最大值
parseInt(Math.random()*(max+1),10);
Math.floor(Math.random()*(max+1));
```
所以希望生成[min,max]的随机数，公式如下：

```
// max - 期望的最大值
// min - 期望的最小值
parseInt(Math.random()*(max-min+1)+min,10);
Math.floor(Math.random()*(max-min+1)+min);
```

### 号池模式实现

```
//以1-15，15个号码作为号池
const numbers = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15];

//抽取结果保存数组
const result = [];

//随机抽取5个号码
for(let i=0;i<5;i++){
	//获取随机数
	const r = randomNum(0,14-i);
	//将抽取的号码加入结果集
	result.push(numbers[r]);
	//把抽取的号码从号池中删除
	arr.splice(i, 1);
	
}

//打印结果
console.log(result)
```

### 编码模式

```
//抽取结果保存数组
const result = [];

//随机抽取5个号码
for(let i=0;i<5;i++){
	//获取随机数
	const r = randomNum(0,9);
	//将抽取的号码加入结果集
	result.push(numbers[r]);
	
}

//打印结果
console.log(result)
```


### 项目总结

本项目在实现过程中，需要严格保证随机的状态，以确保在大数据量测试时，随机数据分布是平均的。


