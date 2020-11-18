# typescript面试

### ts是什么？
TypeScript 是微软开发的 JavaScript 的超集，TypeScript兼容JavaScript，可以载入JavaScript代码然后运行。TypeScript 通过类型注解提供编译时的静态类型检查。TypeScript可处理已有的JavaScript代码，并只对其中的TypeScript代码进行编译。TypeScript可编译成可读的、标准的JavaScript。
### ts的优势
TypeScript的设计解决了JavaScript的“痛点”：弱类型和没有命名空间；这导致程序很难模块化，不适合开发大型程序。
### 基础数据类型
boolean，number，string，数组，元祖，enum，any，void，null和undefined，never，object
### 类型断言有几种方式：
两种：  
- “尖括号”语法
```js
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```
- as语法
```js
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```
### 元祖与数组的区别
- 元素个数：数组元素不确定，元祖已知元素数量
- 元素类型：数组类型相同，元祖类型不同