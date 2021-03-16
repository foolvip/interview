### 类型转换
```js
null == undefined // 结果是ture

[] 转为字符串是 ""       // String([]) 返回""
[] 转为数字是 0            // Number([]) 返回0
[] 转为布尔值是 true        // Boolean([]) 返回true
true 转为数字是 1       // Number(true) 返回1
false 转为数字是 0      // Number(false) 返回0

// 如果一个值是对象，另一个值是数字或字符串，则将对象转换为原始值，然后再进行比较。
```
[ ] 转数字是0,转布尔值是true

### call,apply,bind函数实现
#### call
```js
// 自己实现一个es6的新类型 Symbol   fn = Symbol()
function mySymbol(obj) {
    // 不要问我为什么这么写，我也不知道就感觉这样nb
    let unique = (Math.random() + new Date().getTime()).toString(32).slice(0, 8)
        // 牛逼也要严谨
    if (obj.hasOwnProperty(unique)) {
        return mySymbol(obj) //递归调用
    } else {
        return unique
    }
}
//接下来我们一并把多参数和执行完删除自定义方法删除掉一块搞定
Function.prototype.myCall = function(context) {
  console.log(this); // this指向调用myCall方法的对象
    // 如果没有传或传的值为空对象 context指向window
    context = context || window // context不传值时，默认window
    let fn = mySymbol(context) // 
    context[fn] = this //给context添加一个方法即是this，调用该方法时this便指向context
    // 处理参数 去除第一个参数this 其它传入fn函数
    let arg = [...arguments].slice(1) //[...xxx]把类数组变成数组，arguments为啥不是数组自行搜索 slice返回一个新数组
    context[fn](...arg) //执行fn，this便指向context了
    delete context[fn] //删除方法
}

let Person = {
    name: 'Tom',
    say(age) {
        console.log(this)
        console.log(`我叫${this.name}我今年${age}`)
    }
}

Person1 = {
    name: 'Tom1'
}

Person.say.call(Person1, 18)//我叫Tom1我今年18
```
#### apply
```js
  Function.prototype.myApply = function(context) {
      // 如果没有传或传的值为空对象 context指向window
      if (typeof context === "undefined" || context === null) {
          context = window
      }
      let fn = mySymbol(context)
      context[fn] = this //给context添加一个方法 指向this
          // 处理参数 去除第一个参数this 其它传入fn函数
      let arg = [...arguments].slice(1) //[...xxx]把类数组变成数组，arguments为啥不是数组自行搜索 slice返回一个新数组
      context[fn](...arg) //执行fn
      delete context[fn] //删除方法

  }

```
#### bind
特点 :
1. 函数调用，改变this 
2. 返回一个绑定this的函数
3. 接收多个参数
4. 支持柯里化形式传参 fn(1)(2)
```js
Function.prototype.bind = function(context) {
  //返回一个绑定this的函数，我们需要在此保存this
  let self = this
  // 可以支持柯里化传参，保存参数
  let arg = [...arguments].slice(1)
      // 返回一个函数
  return function() {
    //同样因为支持柯里化形式传参我们需要再次获取存储参数
    let newArg = [...arguments]
    console.log(newArg)
    // 返回函数绑定this，传入两次保存的参数
    //考虑返回函数有返回值做了return
    return self.apply(context, arg.concat(newArg))
  }
}
// 搞定测试
let fn = Person.say.bind(Person1)
fn()
fn(18)

```

### 实现new
https://github.com/mqyqingfeng/Blog/issues/13  
https://juejin.cn/post/6844903704663949325#heading-6  
```js
function objectFactory() {
  var obj = new Object(),
  Constructor = [].shift.call(arguments);
  obj.__proto__ = Constructor.prototype;
  var ret = Constructor.apply(obj, arguments);
  return typeof ret === 'object' ? ret : obj;  // 判断原因如下
};

// ----- 例子解释 ----------------- 构造函数返回了一个对象：
function Otaku (name, age) {
    this.strength = 60;
    this.age = age;

    return {
        name: name,
        habit: 'Games'
    }
}

var person = new Otaku('Kevin', '18');

console.log(person.name) // Kevin
console.log(person.habit) // Games
console.log(person.strength) // undefined
console.log(person.age) // undefined
// ----- 例子 2 -------------- 构造函数返回了一个基本类型的值
function Otaku (name, age) {
    this.strength = 60;
    this.age = age;

    return 'handsome boy';
}

var person = new Otaku('Kevin', '18');

console.log(person.name) // undefined
console.log(person.habit) // undefined
console.log(person.strength) // 60
console.log(person.age) // 18

```
### js的节流和防抖动  
  知乎解释：https://zhuanlan.zhihu.com/p/38313717  
  理解动画demo：http://demo.nimius.net/debounce_throttle/   
  https://mp.weixin.qq.com/s/Vkshf-nEDwo2ODUJhxgzVA  
  
  ```js
  <!-- 防抖 -->
  <!-- 应用场合：提交按钮的点击事件，input输入，window触发resize的时候，不断的调整浏览器窗口大小会不断的触发这个事件，用防抖来让其只触发一次 -->
  function debounce(func, delay) {
    let timeout;
    return function(e) {
      clearTimeout(timeout);
      let context = this, args = arguments;
      timeout = setTimeout(function() {
        func.apply(context, args);
      }, delay);
    }
  }

  var validate = debounce(function(e) {
    console.log("change", e.target.value, new Date-0)
  }, 380);
  // 绑定监听
  document.querySelector("input").addEventListener('input', validate);

  <!-- 节流 -->
  <!-- 应用场景：频繁触发的事件中，如resize, touchmove, mousemove, scroll。throttle 会强制函数以固定的速率执行。因此这个方法比较适合应用于动画相关的场景。 -->
  // 时间戳版(第一次就触发)
  function throttle(fn, wait) {
    var previous = Data.now();
    return function() {
      let now = Data.now();
      let context = this;
      let args = arguments;
      if (now - prevvious > wait) {
        fn.apply(context, args);
        previous = now;
      }
    }
  }
  // 定时器版本
  function throttle(fn, threshold) {
    let timeout;
    return function() {
      let context = this;
      let args = arguments;
      if(!timeout) {
        timeout = setTimeout(() => {
          fn.apply(context, args);
          timeout = null;
        }，threshold);
      }
    }
  }
  
  // 合并版本
  function throttle(fn, threshhold) {
    var timeout;
    var start = +new Date();
    var threshhold = threshhold || 160;
    return function() {
      var context = this, args = arguments, curr = +new Date();
      clearTimeout(timeout);
      if (curr - start >= threshhold) {
        console.log("now", curr, curr - start) //注意这里相减的结果，都差不多是160左右
        fn.apply(context, args);
        start = curr;
      } else {
        <!-- 让方法在脱离事件后也能执行一次 -->
        timeout = setTimeout(function(){
          fn.apply(context, args) 
        }, threshhold);
      }
    }
  }
```
### 深度克隆
https://blog.csdn.net/liuyan19891230/article/details/100789588
```js
// https://github.com/ConardLi/ConardLi.github.io/blob/master/demo/deepClone/src/clone_6.js
// 简易版本
function clone(target, map = new WeakMap()) {
    if (typeof target === 'object') {	
        const isArray = Array.isArray(target);	
        let cloneTarget = isArray ? [] : {};	
        if (map.get(target)) {	
            return target;	
        }	
        map.set(target, cloneTarget);	
        const keys = isArray ? target : Object.keys(target);	
        keys.forEach((value, key) => {
            if (!isArray) {	
                key = value;	
            }	
            cloneTarget[key] = clone(target[key], map);	
        });	
        return cloneTarget;	
    } else {	
        return target;	
    }	
}
// 判断是否为引用类型，我们还需要考虑 function和 null两种特殊的数据类型：
function isObject(target) {	
  const type = typeof target;	
  return target !== null && (type === 'object' || type === 'function');	
}
// 获取数据类型：可以使用 toString来获取准确的引用类型：
// 每一个引用类型都有 toString方法，默认情况下， toString()方法被每个 Object对象继承。如果此方法在自定义对象中未被覆盖，t oString()返回 "[object type]"，其中type是对象的类型。
function getType(target) {	
    return Object.prototype.toString.call(target);	
}

const mapTag = '[object Map]';	
const setTag = '[object Set]';	
const numberTag = '[object Number]';	
const stringTag = '[object String]';	
const arrayTag = '[object Array]';	
const objectTag = '[object Object]';	
const dateTag = '[object Date]';	
const regexpTag = '[object RegExp]';	
const symbolTag = '[object Symbol]';
const boolTag = '[object Boolean]';	
const undefinedTag = '[object Undefined]';
const nullTag = '[object Null]';
const errorTag = '[object Error]';	

// 克隆函数
// 函数的话就会直接返回了，没有做特殊的处理，
 const isFunc = typeof value == 'function'	
 if (isFunc || !cloneableTags[tag]) {	
  return object ? value : {}	
 }

```
### 实现generator函数
```js
function makeIterator(array) {
  var nextIndex = 0;
  return {
    next: function() {
      return nextIndex < array.length ?
        { 
            value: array[nextIndex++],
            done: false
        } 
        :
        {
            value: undefined,
            done: true
        };
    }
  };
}
const it = makeIterator(['a', 'b']);

it.next() 
// { value: "a", done: false }
it.next() 
// { value: "b", done: false }
it.next() 
// { value: undefined, done: true }
```

### 惰性单例模式
```js
let getSingle = function(fn) {
  let result;
  return function() {
    return result || (result = fn.apply(this, arguments));
  }
}
```

### instanceof
```js
function instanceof(left, right) {
    //基本数据类型直接返回false
    if(typeof left !== 'object' || left === null) return false;
    // 获得类型的原型
    let prototype = right.prototype
    // 获得对象的原型
    left = left.__proto__ // left = Object.getPrototypeOf(left)
    // 判断对象的类型是否等于类型的原型
    while (true) {
        if (left === null) return false
        if (prototype === left) return true
        left = left.__proto__ // left = Object.getPrototypeOf(left)
    }
}

```

### promise的实现
https://juejin.im/post/5afd2ff26fb9a07aaa11786c
```js
function handlePromise(promise2, x, resolve, reject) {
  if (promise2 === x) {
    return reject(new TypeError('circular reference'));
  }
  // 判断x不是bull且x是对象或者函数
  if (x !== null && (typeof x === 'object' || typeof x === 'function')) {
    let called; // called控制resolve或reject只执行一次，多次调用没有任何作用。
    try {
      let then = x.then;
      if (typeof then === 'function') { // 如果是函数，就认为他是返回新的promise
        then.call(x, y => {
          if (called) return;
          called = true;
          handlePromise(promise2, y, resolve, reject); // 递归解析promise
        }, r => {
          if(called) return;
          called = true;
          reject(r);
        })
      } else { // 不是函数，就是普通对象
        resolve(x) // 直接将对象返回
      }
    } catch(e) {
      if (called) return;
      called = true;
      reject(e);
    }
  } else { // x是普通值，直接走then的成功回调
    resolve(x);
  }
}

class Promise {
  constructor(fn) {
    // 三个状态
    this.state = 'peding'
    this.value = undefined
    this.reason = undefined
    //  解决setTimeout调用问题
    this.successStore = []; // 定义一个成功函数的数组
    this.failStore = []; // 定义一个存放失败函数的数组
    let resolve = value => {
      if (this.state === 'pending') {
        this.state = 'fulfilled';
        this.value = value;
        this.successStore.forEach(fnc => fnc()); //  依次执行数组中的成功函数
      }
    }
    let reject = value => {
      if (this.state === 'pending') {
        this.state = 'rejected'
        this.reason = value;
        this.failStore.forEach(fnc => fnc()) // 依次执行数组中的失败函数
      }
    }
    //  自动执行函数
    try {
      fn(resolve, reject)
    } catch (e) {
      reject(e)
    }
  }
  // then
  then(onFulfilled, onRejected) {
    let promise2; // 返回的新的promise
    switch(this.state) {
      case 'fulfilled':
        promise2 = new Promise((resolve, reject) => {
          try {
            let x = onFulfilled(this.value);
            handlePromise(promise2, x, resolve, reject);
          } catch(e) {
            reject(e);
          }
        })
        break
      case 'rejected':
        promise2 = new Promise((resolve, reject) => {
          try {
            let x = onRejected(this.reason); //x存放返回的结果
            handlePromise(promise2, x, resolve, reject); 
          } catch {
            reject(e);//报错执行reject
          }
        })
        onRejected()
        break
      case 'pending':
        promise2 = new Promise((resolve, reject) => {
          this.successStore.push(() => {
            try {
              let x = onFulfilled(this.value);
              handlePromise(promise2, x, resolve, reject);
            } catch(e) {
              reject(e); //报错执行reject
            }
          })
          this.failStore.push(() => {
            onRejected(this.reason);
            try {
              let x = onRejected(this.reason);
              handlePromise(promise2, x, resolve, reject);
            } catch(e) {
              reject(e); //报错执行reject
            }
          }) 
        })
    }
    return promise2; //返回新的promise
  }
}

module.exports = Promise; //将Promise导出

// promise.all 实现
Promise.all = function(arr){
    return new Promise((resolve,reject)=>{
        let resolvList=[];
        arr.forEach((item)=>{
            item.then((data)=>{
                resolvList.push(data);
                console.log(data);
                if(arr.length == resolvList.length){
                    resolve(resolvList);
                }
            },(reason)=>{
                reject(reason);
            })
        })
    })
}
```
### 深度遍历、广度遍历
```js
const DFS = function(node) {
  if (!node) {
    return
  }
  let deep = arguments[1] || 1
  console.log(`${node.nodeName}.${node.classList} ${deep}`)

  if (!node.children.length) {
    return
  }
  Array.from(node.children).forEach(item => DFS(item, deep + 1))
}

const BFS = root => {
  if (!root) {
    return
  }
  let queue = [{item: root, depth: 1}] 
  while(queue.length) {
    let node = queue.shift()
    console.log(`${node.item.nodeName}.${node.item.classList} ${node.depth}`)
    if (!node.item.children.length) {
      continue;
    }
    Array.from(node.item.children).forEach((item, index, arr) => {
      queue.push({
        item,
        depth: node.depth + 1
      })
    })
  }
}
```

### 转化为驼峰命名
```js
var s1 = "get-element-by-id"
//转化为 getElementById
var f = function(s){
    return s.replace(/-\w/g,function(x){
      return x.slice(1).toUpperCase(); 
    })
}

```