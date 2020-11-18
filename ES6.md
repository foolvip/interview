
### 数组去重
```js
// 去除数组的重复成员
[...new Set(array)]
```
### function与class的区别
#### class
- ES6 的class可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的class写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。  
- 使用的时候，是直接对类使用new命令，跟构造函数的用法完全一致。
- 类必须使用new调用
- 类不存在变量提升

### 箭头函数和普通函数的区别
- 箭头函数是匿名函数，不能作为构造函数，不能使用new
- 箭头函数不能绑定arguments,取而代之用rest参数...解决
```js
function A(a){
  console.log(arguments);
}
A(1,2,3,4,5,8);  //  [1, 2, 3, 4, 5, 8, callee: ƒ, Symbol(Symbol.iterator): ƒ]
let B = (b)=>{
  console.log(arguments);
}
B(2,92,32,32);   // Uncaught ReferenceError: arguments is not defined
let C = (...c) => {
  console.log(c);
}
C(3,82,32,11323);  // [3, 82, 32, 11323]
```
- 箭头函数不绑定this,会捕获其所在的上下文的this值，作为自己的this值
- 箭头函数通过call（）或者apply（）方法调用一个函数时，只传入一个个参数，对this并没有影响。
```js
let obj2 = {
    a: 10,
    b: function(n) {
        let f = (n) => n + this.a;
        return f(n);
    },
    c: function(n) {
        let f = (n) => n + this.a;
        let m = {
          a: 20
        };
        return f.call(m,n);
    }
};
console.log(obj2.b(1));  // 11
console.log(obj2.c(1)); // 11
```
- 箭头函数没有原型属性
- 箭头函数不能当做Generator函数,不能使用yield关键字
#### 总结
箭头函数的 this 永远指向其上下文的  this ，任何方法都改变不了其指向，如 call() ,  bind() ,  apply() 
普通函数的this指向调用它的那个对象
### Map和weakMap的区别