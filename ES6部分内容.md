# ES6部分内容

标签（空格分隔）： ES6

---

##**ECMAScript6**
###**声明变量**
- 可以使用let、const关键字声明变量，而不推荐使用var声明变量
#### **var声明变量的问题**：
-  可以多次重复声明同一个变量名，存在覆盖的风险
-  在全局声明的变量会挂在全局对象上
-  **`var不能形成块级作用域`**，例如：if、for范围外依然可以使用var声明的变量
-  var声明的变量具备变量提升（hoisting）`/hɔɪst/升起，提起;`特性— 允许使用在前，声明在后
```
// 变量提升

var miaov = 123;

document.onclick = function (){
	console.log(miaov)//456
}

var miaov = 456;
```
<br/>
```
if(false){
    // 变量提升
	var miaov = 'ketang';
}

console.log(miaov);//undefined
```
<br/>
```
for( var i = 0; i < 10; i++ ){}
console.log(i);//10
```
####**let声明变量**
- 同一个作用域只能声明一个名字的变量：不允许重复声明
- **不挂在window上**,是放在内存里的
- 不存在变量提升
- 会在离最近的大括号形成块级作用域 
```
let miaov = 123;
let miaov = 456;//Uncaught SyntaxError: Identifier 'miaov' has already been declared

syntax /ˈsɪntæks/ 
n.	语法; 句法; 句法规则[分析]; 语构;
```
```
var abc = 10;
let abc = 20;//Uncaught SyntaxError: Identifier 'abc' has already been declared
```
<br/>
```
console.log(	window );//Window对象
console.log(	miaov1 );//Uncaught ReferenceError: miaov is not defined 
let miaov1 = 10;
```
<br/>
```
if(true){  // 块级作用域
	var miaov =123;
  	let foo = 'ketang';
  	console.log(foo);//ketang
  	if(true){
  		let bar = 456;
  	}
  	//console.log(bar);//Uncaught ReferenceError: bar is not defined
}
console.log(miaov );//123
console.log(foo );//Uncaught ReferenceError: foo is not defined
```
<br/>
```
// 循环体执行了5次，给document绑定了5个事件处理函数
for( var i = 0; i < 5; i++ ){
	document.addEventListener('click',function 	(){
		alert(i);//点击	document弹 五次5
	})
}
```
<br/>
```
for( let i = 0; i < 5; i++ ){
	document.addEventListener('click',function 	(){
		alert(i);//点击	document弹 弹5次分别是 0、 1 、 2 、 3 、4
	})
}
```
```
<body>
	<ul class="list">
		<li>123</li>
		<li>123</li>
		<li>123</li>
		<li>123</li>
	</ul>
	<script>
		var lis = document.querySelectorAll('.list li');
		/*
		  用let:
			第一次，声明初始的i=0 i++ = 1;
			第2次，重新声明变量i=1 i++ = 2;
			第3次，重新声明变量i=2 i++ = 3;
			第4次，重新声明变量i=3 

			每次循环都会重新声明一个i，这个i的值是上一次循环的最终值，这个最终值作为新的i的初始值
		*/
		for( let i = 0; i < lis.length; i++ ){
			lis[i].onclick = function 	(){
				lis[i].style.background = 'red';	
			}
		}
        //用var声明，可以用函数自执行传参解决
		for( var j = 0; j < lis.length; j++ ){
			(function 	(j){
				lis[j].onclick = function 	(){
					lis[j].style.background = 'red';	
				}		
			})(j);
		}
	</script>
</body>
```
#####**块级作用域**
- let允许创建块级作用域，let声明的变量只在它所在的代码块内有效
```
{
	let a = 10;
	let b = 20;
	console.log(a);//10
	console.log(b);//20
	{
		{
			{
				console.log(a);//10
				console.log(b);//20
			}
		}
	}
}
console.log(a);//Uncaught ReferenceError: a is not defined
```
- 在if中使用：
```
{
  let test = 10;
  var foo = 1;
}

console.log(test) // ReferenceError: miaov is not defined.
console.log(foo) // 1


if(false){
  let test1 = 10;  // 只在这个代码块内有效，形成了块级作用域
  var foo1 = 1;//即使是走不进if里面，还是有了变量提升
}

console.log(test1) // ReferenceError: miaov is not defined.
console.log(foo1) // undefined【变量什么未赋值即为undefined】
```
- 在for中使用,i只能在循环体内使用，循环体外会报错：
```
for (let i = 0; i < 10; i++) {
  // ...
}
console.log(i); // ReferenceError: i is not defined
//如果是用var声明的i，for循环结束之后找到的i就是10
```
####**const 声明常量**
- constant	`[ˈkɑ:nstənt]`adj.持续的; 永恒的; 坚定; 忠实的;n.[数] 常量; 永恒值;
- 同一个作用域只能声明一个名字的常量：不允许重复声明;
- 不挂在window上;
- 不存在常量提升;
- 会在离最近的大括号形成块级作用域
- const声明的是常量/恒量
	- 声明的常量不能重新赋值
	- 声明常量必须赋值
```
const USERS = 6;  // 声明的是常量
USERS = 20;  // 不能重新赋值 Uncaught TypeError: Assignment to constant variable.
```
<br/>
```
let miaov;

miaov = 123;

console.log(miaov);//123
//声明变量必须赋值 
const ketang;  // Uncaught SyntaxError: Missing initializer in const declaration
```
- 如果赋的值是引用类型，那么可以通过变量来修改引用类型的值：
```
const test = {};
test.a = 1;
test.b = 2;
console.log(test);  // {a: 1, b: 2}
```
####**总结let和const**
- 总结let和const:
    - 声明的变量不具备变量提升（hoisting）特性
    - 只在声明所在的块级作用域内有效
    - 不允许重复声明
    - 暂时性死区（TDZ`temporal dead zone`）所声明的变量绑定在定义的区域，使用let命令声明变量之前，该变量都是不可用的
    - const 在声明时必须被赋值值    
```
function fn(miaov){  // 形参就是声明局部变量，不能重复声明
	/*let miaov  = 10;
	console.log(miaov);////Uncaught SyntaxError: Identifier 'miaov' has already been declared
	*/

	// 总之，在代码块内，使用let/const命令声明变量/常量之前，该变量/常量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）
	// 只能在变量声明之后才能使用
	ketang = 10; 
	console.log(	ketang );//10
	let ketang;//写到这行，ketang=10 那行就会报错 Uncaught ReferenceError: ketang is not defined
}

fn(1)
```
###**解构赋值**
####**数组的结构赋值**
```
function test(){
    return [1,2,3,4];
}

var [a,b] = test();
console.log(a,b); // 1,2
```
test函数执行后，返回的是一个数组。取数组前两个值分别存在变量中，根据解构赋值的规则，在左侧声明变量，放在中括号中，会把右边数组中的值一一对应赋值给左边的变量。

####**对象的解构赋值**
```
let o = {miaov:1,ketang:2,foo:3,abc:10,k:'leo'};
// ，没有与之对应的属性，赋一个默认值
// 用A:B 把A对用的值赋值给变量B，不能使用A，要使用B。
let {ketang,miaov,foo,abc=12345,k:user="momo"} = o;  

console.log(abc);//10
console.log(k);//Uncaught ReferenceError: k is not defined
console.log(user);//momo
```
<br/>
```
function test1(){
    return {a:1,b:2,c:3};
}

var {a,b} = test();
console.log(a,b); // 1,2
```
test1函数执行后，返回的是一个对象。分别取出对象中属性为a和b的值，根据解构赋值的规则，在左侧声明变量，放在大括号中，变量名要和属性名保持一致。

####**函数参数的解构赋值**
```
function test({a,b}){
    console.log(a,b);//1,2
}

test({a:1,b:2,c:3})
```
在形参中定义变量，得到实参对象指定的属性。
####**默认值**
可以给变量设置默认值和另声明一个变量
```
var {a:otherVar,b,d=11111} = {a:1,b:2,c:3};
console.log(d); // 11111【11111是默认值，在解构的对象中有d属性，就去拿的d属性的值，没有就是默认设置的11111；d属性的值是null，找到的还是null；如果d属性的值原本是undefined占位，那最后d解构赋值的是默认值11111】
console.log(otherVar); // 1
console.log(a); // Uncaught ReferenceError: a is not defined
```
- 使用 等号`=`给变量赋一个默认值，如果右边对象中没有与之对应的属性，则按默认值来。
- 使用`:`重新声明一个变量，会把匹配到的a的值赋给新的变量otherVar，此时在外面使用时候，不能使用a。
- 也可以连着一起使用：
```
var {a,b,d:foo='默认值'} = {a:1,b:2,c:3};
console.log(foo); // '默认值'
```
###**箭头函数 Arrow Functions**
在ES6中，箭头函数就是函数的一种**简写形式**,允许使用“箭头”（=>）**定义函数**。
```
=> "箭头"
	使用“箭头”（=>）定义函数
```
之前声明函数：
```
function foo(){
    return 1;
}
```
改造为箭头函数:
```
let foo = () => 1;
```
####**箭头函数的参数**
上面使用“箭头”（=>）定义的函数，左侧的()包裹函数的形参，如果定义的函数**没有形参**或者**多个形参**，一定要使用括号：
```
// 没有参数，要使用()
let test = () => 1;

// 多个参数，要使用()
let foo = (a,b) => a + b;
let bar = (a,b,c) => a + b + c;
```
如果只有**一个形参**，可以省略括号：
```
let foo = a => a;
```
####**箭头函数return返回值**
“箭头”（=>）的右侧是函数体代码，会在函数执行后作为函数的返回值，不需要显示的使用return:
```
let foo = (a,b) => a + b;
console.log(foo(1,2)); // 3
```
```
let arr = [1,2,3];  
let newArr = arr.map(item => item * 2);
console.log(newArr); // [2,4,6]
```
有多行代码，可以写在一对{}中，手动调用return返回值:
```
let foo = (a,b) => {
    console.log(a)
    console.log(b)
    return a + b; 
}
```
当要返回的是对象时，又不想手动调用return，记得加上()保证是一个对象整体，而不被误以为是函数体：
```
var obj = () => ({a:1,b:2})
console.log(obj());  // {a:1,b:2}
```
####**箭头函数中this指向**
- 函数的this是在调用的时候决定this的值
- 箭头函数，绑定的是所定义时在的作用域的this
    - 箭头函数内的this，绑定定义时所在的作用域的this，并不是在调用时候决定this的指向。
```
document.onclick = function (){
    setTimeout(function (){
        console.log(this); // 定时器执行的函数，在非严格模式下this指向window  
    },1000) 
}
```
<br/>
```
let o = {
	fn:function (){
		console.log(this);	//对象o
	},
	f: () => {
		console.log(this);//window
	}
}

o.fn();
o.f();
```
如果要在setTimeout中使用点击时的元素，通常需要存一个变量。
```
document.onclick = function (){
    var that = this;
    setTimeout(function (){
        console.log(that); // that变量存的就是触发事件的元素document
    },1000) 
}
```
如果使用箭头函数，一切将会变得非常简单：
```
document.onclick = function (){
    setTimeout( () => {
        console.log(this); //document
    },1000) 
}
```
箭头函数是在事件处理函数中定义，事件处理函数this指向的是触发事件的元素，所以这个this，也就是触发事件的元素。
####**使用箭头函数的特性**：
- 函数体内的this值，绑定定义时所在的作用域的this
- 不可以当作构造函数
- 不可以使用arguments对象
```
//把上一个例子都换成箭头函数的写法
document.onclick = () => setTimeout( () => {
        console.log(this); //this指向Window，这个大括号里面找this没有找到，向外找，就是全局，全局的this指向window
},1000)  
```
<br/>
```

function fn(){
	console.log(arguments)//Arguments(5) [1, 2, 3, 4, 5, callee: ƒ, Symbol(Symbol.iterator): ƒ]
}
fn(1,2,3,4,5)


let f = () => {
	// 箭头函数中没有arguments
	console.log(arguments);  //Uncaught ReferenceError: arguments is not defined
}
f(1,2,3,4,5);
```





