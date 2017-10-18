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

## 7.2 构造对象

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


## 7.8 标准对象