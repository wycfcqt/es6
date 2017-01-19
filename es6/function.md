# Function #
1. 可以为函数赋默认值
```
function (x,y=10){
 console.log(x+y;)
}
```
- 初始值的好处
- 清晰参数的类型
- 方便以后接口的更改
2. 参数是默认有了声明，因此**不能再次使用var或let声明**
3. 可与解构赋值一起使用
```
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined, 5,对应位置进行赋值，没值则undefined
foo({x: 1}) // 1, 5
foo({x: 1, y: 2}) // 1, 2
foo() // TypeError: Cannot read property 'x' of undefined
//在看下面的例子
// 写法一
function m1({x = 0, y = 0} = {}) {
  return [x, y];
}

// 写法二
function m2({x, y} = { x: 0, y: 0 }) {
  return [x, y];
}
//上面两种写法都对函数的参数设定了默认值，区别是写法一函数参数的默认值是空对象，但是设置了对象解构赋值的默认值；
//写法二函数参数的默认值是一个有具体属性的对象，但是没有设置对象解构赋值的默认值。

// 函数没有参数的情况
m1() // [0, 0]
m2() // [0, 0]

// x和y都有值的情况
m1({x: 3, y: 8}) // [3, 8]
m2({x: 3, y: 8}) // [3, 8]

// x有值，y无值的情况
m1({x: 3}) // [3, 0]
m2({x: 3}) // [3, undefined]

// x和y都无值的情况
m1({}) // [0, 0];
m2({}) // [undefined, undefined]

m1({z: 3}) // [0, 0]
m2({z: 3}) // [undefined, undefined]
/*解构赋值同样可以赋初始值，在“=”后边没有给值的情况下，会取得自己的默认值，否则得到undefined*/
```
4. **一般省略的参数都在尾部，如果缺省参数不在尾部，那就无法省略，除非传入明确的undefined，只有传入undefined才能触发默认值，null则无效果 **
5. 函数的length属性，只返回没有指定默认值的参数个数，而不是全部
```
(function (a) {}).length // 1
(function (a = 5) {}).length // 0
(function (a, b, c = 5) {}).length // 2
```
*rest参数同样也不会计入参数个数*

----------
**同样，默认值不在参数的尾部，也将不再计入参数个数，就是遇到默认参数就停止计数**
6. 可指定参数不得省略，省略就抛出错误或是其他操作等
```
function throwIfMissing() {
  throw new Error('Missing parameter');
}

function foo(mustBeProvided = throwIfMissing()) {
  return mustBeProvided;
}

foo()
// Error: Missing parameter
/*参数的默认值是在函数运行时赋值而非定义时*/
```
7.rest参数	

- rest参数也只能在函数参数的尾部声明
- rest参数写法 **...args**
- rest参数表示函数多余的参数，以一个数组的方式返回
- 在无其他参数只有声明了rest参数时，rest参数可以代表arguments
 ```
	function add(...values) {
	  let sum = 0;
	
	  for (var val of values) {
	    sum += val;
	  }
	
	  return sum;
	}

add(2, 5, 3) // 10
 ```
- 数组性体现在，和arguments相比，rest是一个数组，而非类数组
```
// arguments变量的写法
function sortNumbers() {
  return Array.prototype.slice.call(arguments).sort();
}

// rest参数的写法
const sortNumbers = (...numbers) => numbers.sort();
```
### 扩展运算符 ###
1. 写法...[1,2,3]，作用是将一个数组转换成用逗号分隔的参数序列
2. 该运算符主要用于函数调用。
3. 由于扩展运算符可以展开数组，所以不再需要apply方法，将数组转为函数的参数了。
```
// ES5的写法
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2];
f.apply(null, args);

// ES6的写法
function f(x, y, z) {
  // ...
}
var args = [0, 1, 2];
f(...args);

//下面是扩展运算符取代apply方法的一个实际的例子，应用Math.max方法，简化求出一个数组最大元素的写法。

// ES5的写法
Math.max.apply(null, [14, 3, 77])

// ES6的写法
Math.max(...[14, 3, 77])

// 等同于
Math.max(14, 3, 77);
```