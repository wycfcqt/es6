# es6-学习笔记 #
# let #
1. 声明变量，只在自己的作用域（代码块）中有效
2. for循环引用 循环外使用变量 报错
3. 必须先声明后使用，上面声明，下面才能使用，否则报错
4. 不存在变量提升
5. 暂时性死区
6. 不能重复声明，比如
```
var a=10;
let a=11;//报错
let b=10;
let b=11;//报错
```
7. 存在块级作用域

# const #
1. 是一个常量，一旦声明就不能更改，即不能被赋值
2. 声明的同时就必须初始化
3. 对象冻结函数
```
var constantize = (obj) => {     
Object.freeze(obj);  
  Object.keys(obj).forEach( (key, value) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```
4. 获取顶层对象兼容写法
```
// 方法一
(typeof window !== 'undefined'
   ? window
   : (typeof process === 'object' &&
      typeof require === 'function' &&
      typeof global === 'object')
     ? global
     : this);

// 方法二
var getGlobal = function () {
  if (typeof self !== 'undefined') { return self; }
  if (typeof window !== 'undefined') { return window; }
  if (typeof global !== 'undefined') { return global; }
  throw new Error('unable to locate global object');
};
```