### 任务队列
```js
async function foo() {
    console.log('foo')
}
async function bar() {
    console.log('bar start'); 
    await foo(); 
    console.log('bar end')
}
console.log('scrpt start');
setTimeout(function() {
    console.log("setTimeout")
}, 0);
bar();
new Promise(function(resolve){
    console.log('promise executor'); 
    resolve();
}).then(function(){
    console.log('promise then')
});
console.log('scriptr end');
```
### this调用
```js
const module = {
  x: 42,
  getX: function() {
    return this.x;
  }
};

const unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope(该函数在全局范围内被调用)
// output: undefined
```
### call、apply、bind
#### call
```js

```
