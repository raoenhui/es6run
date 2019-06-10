# es6run
# 变量与字符串

let是ES6中新增关键字。
它的作用类似于var，用来声明变量，但是所声明的变量，只在let命令所在的代码块内有效。
### Example1
```
/*E1*/
if(true){
    var a = 1;
    let b = 2;
}
document.write(a+'<br/>');
document.write(b+'<br/>'); // Uncaught ReferenceError: b is not defined
```
### Example2
```
/*E2*/
function f1() {
  var a = 8;
  let n = 5;
  if (true) {
      let n = 10;
      var a = 20
  }
  document.write(n); // 5
  document.write(a); // 20
}
f1();
```

>Q1：用let声明a变量默认为5，在if判断中let声明a为10，看a输出结果。
```
/*Exercises1*/
let a = 5;
if (true) {
    let a = 10;
}
document.write(a);//5
```
for循环的计数器，就很合适使用let命令。
```
/*E3*/
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    document.write(i);
  };
}
a[6](); 

var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    document.write(i);
  };
}
a[6](); 

```
### const
const 声明的是常量，一旦声明，值将是不可变的。
```
const PI = 3.1415;
PI // 3.1415
 
PI = 3;
PI // 3.1415
 
const PI = 3.1;
PI // 3.1415
```
const 也具有块级作用域
```
/*E4*/
if (true) {
  const max = 5;
}
document.write(max);  //Uncaught ReferenceError: max is not defined

if (true) {
  const max = 5;
  document.write(max);  //5
}
```
* const 不可重复声明
```
/*E5*/
var message = "Hello!";
let age = 25;
 
const message = "Goodbye!";
const age = 30;//cli:Duplicate declaration "age"
```
const 指令指向变量所在的地址，所以对该变量进行属性设置是可行的（未改变变量地址），如果想完全不可变化（包括属性），那么可以使用冻结
```
/*E6*/
const C1 = {};
C1.a = 1;
document.write(C1.a); // 1 
C1 = {};  // cli: C1 = {};  // 报错  重新赋值，地址改变

const C2 = Object.freeze({}); 
C2.a = 1; 
document.write(C2.a);//Uncaught TypeError: Can't add property a, object is not extensible
```
>Q2:在if (true) { 声明一个const变量a，并为赋值为5， }在块级作用域中和外面，分别打印变量a看结果。
```
/*Exercises2*/
if(true){
  const a=5;
  document.write('a1:'+a);
}
document.write('a2:'+a);//Uncaught ReferenceError: a is not defined
```
是否包含字符串三种新方法
传统上，JavaScript只有 indexOf 方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6又提供了三种新方法。
* includes()：返回布尔值，表示是否找到了参数字符串。
* startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
* endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。
```
var str = "Hello world!";
 
str.startsWith("Hello") // true
str.endsWith("!") // true
str.includes("o") // true
```
这三个方法都支持第二个参数，表示开始搜索的位置。
* 上面代码表示，使用第二个参数n时，endsWith 的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。
```
var str = "Hello world!";
 
str.startsWith("world", 6) // true
str.endsWith("Hello", 5) // true
str.includes("Hello", 6) // false
```
repeat()原字符串重复
```
var str = "x";
str.repeat(3) // "xxx"
 
var str1 = "hello";
str1.repeat(2) // "hellohello"
```
标签模板
模板字符串前面有一个标识名tag，它是一个函数。整个表达式的返回值，就是tag函数处理模板字符串后的返回值。
```
var a = 5;
var b = 10;
 
tag`Hello ${ a + b } world ${ a * b }`;
```
tag函数所有参数的实际值如下。
- 第一个参数：['Hello ', ' world ']
- 第二个参数: 15
- 第三个参数：50

也就是说，tag函数实际上以下面的形式调用。
```
tag(['Hello ', ' world '], 15, 50)
```
tag用法
```
/*E7*/
var a = 5;
var b = 10;
 
function tag(s, v1, v2) {
  document.write(s[0]+'<br/>');
  document.write(s[1]+'<br/>');
  document.write(v1+'<br/>');
  document.write(v2+'<br/>');
 
  return "OK";
}
 
tag`Hello ${ a + b } world ${ a * b}`;
// "Hello "
// " world "
// 15
// 50
// "OK"
```
模板字符串可以是原始的
ES6还为原生的String对象，提供了一个raw方法。
若使用String.raw 作为模板字符串的前缀，则模板字符串可以是原始(raw)的。反斜线也不再是特殊字符，\n 也不会被解释成换行符：
```
/*E8*/
var raw =String('Not a newline: \n');
document.write(raw === 'Not a newline: \\n');// false

 let raw = String.raw`Not a newline: \n`;
 document.write(raw === 'Not a newline: \\n'); // true
```
