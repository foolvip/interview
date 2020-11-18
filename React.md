## react
### react 优点
提高了应用的性能减少重绘次数、可以方便的在客户端和服务器端使用、提升开发效率、代码可维护性和可阅读性增强。
### 生命周期函数
#### 16.3+版本的声明周期
#### 挂载（当组件实例被创建并插入DOM中）
- constructor()
- static getDerivedStateFromProps()
- render()
- componentDidMount()
#### 更新（当组件的 props 或 state 发生变化时会触发更新）
当组件的 props 或 state 发生变化时会触发更新  
- static getDerivedStateFromProps()
- shouldComponentUpdate()
- render()
- getSnapshotBeforeUpdate()
- componentDidUpdate()
#### 卸载（当组件从 DOM 中移除时）
componentWillUnmount()
#### 错误处理（当渲染过程，生命周期，或子组件的构造函数中抛出错误时）
- static getDerivedStateFromError()
- componentDidCatch()

### 区分Real DOM和Virtual DOM
Real DOM  
- 更新缓慢。
- 可以直接更新 HTML。
- 如果元素更新，则创建新DOM。
- DOM操作代价很高。
- 消耗的内存较多。  
Virtual DOM
- 更新更快。
- 无法直接更新 HTML。
- 如果元素更新，则更新 JSX 。
- DOM 操作非常简单。
- 很少的内存消耗
### 理解虚拟DOM
Virtual DOM是一个模拟了DOM树的JavaScript对象。它最初只是real DOM的副本。它是一个节点树，它将元素、它们的属性和内容作为对象及其属性。 React的渲染函数从React组件中创建一个节点树。然后它响应数据模型中的变化来更新该树，该变化是由用户或系统完成的各种动作引起的。
#### Virtual DOM 工作过程有三个简单的步骤
- 每当底层数据发生改变时，整个 UI 都将在Virtual DOM描述中重新渲染。
- 计算之前 DOM 表示与新表示的之间的差异。
- 完成计算后，将只用实际更改的内容更新 real DOM。
### 父组件和子组件的componentDidMount哪一个先执行
父组件render->componentDidMount，父组件render的时候调用子组件，
### 你怎样理解“在React中，一切都是组件”这句话。
组件允许你将UI拆分为独立可复用的代码片段，并对每个片段进行独立构思。  
组件是 React应用UI的构建块。这些组件将整个UI分成小的独立并可重用的部分。每个组件彼此独立，而不会影响 UI 的其余部分。
### 怎样解释 React 中 render() 的目的。
每个React组件强制要求必须有一个 render()。它返回一个 React 元素，是原生 DOM 组件的表示。如果需要渲染多个 HTML 元素，则必须将它们组合在一个封闭标记内，例如 <form>、<group>、<div> 等。此函数必须保持纯净，即必须每次调用时都返回相同的结果。
### react中的状态是什么？它是如何使用的？
状态时React组件的核心，是数据的来源，必须尽可能的简单。基本上状态时确定组件呈现和行为的对象。可以通过this.state()访问他们。与Props不同，状态是可变的，并创建动态和交互式组件。
### React中的箭头函数是什么？怎么用？
箭头函数是用于编写函数表达式的简短语法。这些函数允许正确绑定组件的上下文，因为在ES6中默认不能使用自动绑定。
### 区分有状态和无状态组件
#### 有状态组件
- 在内存中存储有关组件状态变化的信息
- 有权改变状态
- 包含过去、现在和未来的状态变化情况
- 接受无状态组件状态变化要求的通知，然后将props发送给他们。
#### 无状态组件
- 计算组件的内部的状态
- 无权改变状态
- 不包含过去，现在和未来可能发生的状态变化情况
- 从有状态组件接受props并将其视为回调函数。
### 你对 React 的 refs 有什么了解？
Refs提供了一种方式，允许我们访问 DOM 节点或在render方法中创建的 React元素。
#### 何时使用 Refs
1.管理焦点，文本选择或媒体播放。 2.触发强制动画。3.集成第三方 DOM 库。  
避免使用 refs 来做任何可以通过声明式实现来完成的事情。你不能在函数组件上使用 ref 属性，因为他们没有实例。可以在函数组件内部使用 ref 属性，只要它指向一个 DOM 元素或 class 组件
###  你对受控组件和非受控组件了解多少
#### 受控组件
- 没有维持自己的状态
- 数据由父组件控制
- 通过props获取当前值，然后通过回调通知更改
#### 非受控组件
- 保持着自己的状态
- 数据由DOM控制
- Refs用于获取当前值
### react高阶组件
https://segmentfault.com/a/1190000010371752    
高阶组件是复用组件逻辑的高级方法，是一种源于 React 的组件模式。 HOC是自定义组件，在它之内包含另一个组件。它们可以接受子组件提供的任何动态，但不会修改或复制其输入组件中的任何行为。你可以认为 HOC 是“纯（Pure）”组件。    
高阶组件是参数为组件，返回值为新组件的函数。  
- 代码重用，逻辑和引导抽象
- 渲染劫持
- 状态抽象和控制
- Props 控制
### 什么是纯组件？
纯（Pure） 组件是可以编写的最简单、最快的组件。它们可以替换任何只有 render() 的组件。这些组件增强了代码的简单性和应用的性能。
### React 中 key 的重要性是什么？
key 用于识别唯一的 Virtual DOM 元素及其驱动 UI 的相应数据。它们通过回收 DOM 中当前所有的元素来帮助 React 优化渲染。这些 key 必须是唯一的数字或字符串，React只是重新排序元素而不是重新渲染它们。这可以提高应用程序的性能。
### MVC框架的主要问题是什么？
- 对 DOM 操作的代价非常高
- 程序运行缓慢且效率低下
- 内存浪费严重
- 由于循环依赖性，组件模型需要围绕 models 和 views 进行创建
### 解释下FLux
Flux 是一种强制单向数据流的架构模式。它控制派生数据，并使用具有所有数据权限的中心 store 实现多个组件之间的通信。整个应用中的数据更新必须只能在此处进行。 Flux 为应用提供稳定性并减少运行时的错误。
### Redux遵循的三个原则
- 单一数据源：整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序。
- 状态(state)是只读的：唯一改变 state 的方法就是触发 action，action 是一个用于描述已发生事件的普通对象。改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示。
- 使用纯函数来执行修改：为了描述 action 如何改变 state tree ，你需要编写 reducers。为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数。
###  列出 Redux 的组件。
Redux 由以下组件组成：
- Action – 这是一个用来描述发生了什么事情的对象。
- Reducer – 这是一个确定状态将如何变化的地方。
- Store – 整个程序的状态/对象树保存在Store中。
- View – 只显示 Store 提供的数据。
### 如何在 Redux 中定义 Action？
React 中的 Action 必须具有 type 属性，该属性指示正在执行的 ACTION 的类型。必须将它们定义为字符串常量，并且还可以向其添加更多的属性。在 Redux 中，action 被名为 Action Creators 的函数所创建。以下是 Action 和Action Creator 的示例：
```js
function addTodo(text) {
  return {
    type: ADD_TODO,    
    text
  }
}
```
### 解释 Reducer 的作用。
Reducers 是纯函数，它规定应用程序的状态怎样因响应 ACTION 而改变。Reducers 通过接受先前的状态和 action 来工作，然后它返回一个新的状态。它根据操作的类型确定需要执行哪种更新，然后返回新的值。如果不需要完成任务，它会返回原来的状态。
### Store 在 Redux 中的意义是什么？
Store 是一个 JavaScript 对象，它可以保存程序的状态，并提供一些方法来访问状态、调度操作和注册侦听器。应用程序的整个状态/对象树保存在单一存储中。因此，Redux 非常简单且是可预测的。我们可以将中间件传递到 store 来处理数据，并记录改变存储状态的各种操作。所有操作都通过 reducer 返回一个新状态。
### Redux与Flux有何不同？
Flux | Redux
:-:  | :-:
Store包含状态和更改逻辑 | Store和更改逻辑是分开的
有多个Store | 只有一个Store
所有Store都互不影响而且是平级的 | 带有分层reducer的单一Store
有单一调度器 | 没有调度器概念
React组件订阅store | 容器组件是有联系的
状态是可变的 | 状态是不可变的

### Redux 有哪些优点？
- 结果的可预测性 - 由于总是存在一个真实来源，即 store ，因此不存在如何将当前状态与动作和应用的其他部分同步的问题。
- 可维护性 - 代码变得更容易维护，具有可预测的结果和严格的结构。
- 服务器端渲染 - 你只需将服务器上创建的 store 传到客户端即可。这对初始渲染非常有用，并且可以优化应用性能，从而提供更好的用户体验。
- 开发人员工具 - 从操作到状态更改，开发人员可以实时跟踪应用中发生的所有事情。
- 社区和生态系统 - Redux 背后有一个巨大的社区，这使得它更加迷人。一个由才华横溢的人组成的大型社区为库的改进做出了贡献，并开发了各种应用。
- 易于测试 - Redux 的代码主要是小巧、纯粹和独立的功能。这使代码可测试且独立。
- 组织 - Redux 准确地说明了代码的组织方式，这使得代码在团队使用时更加一致和简单。

### 面试总结
https://segmentfault.com/a/1190000016885832?utm_source=tag-newest  
### 什么是JSX
JSX 是JavaScript XML 的简写。JSX是一个 JavaScript 的语法扩展。JSX可以很好地描述UI应该呈现出它应有交互的本质形式。JSX可能会使人联想到模版语言，但它具有JavaScript的全部功能。
### JSX优点
- JSX 执行更快，因为它在编译为JavaScript代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- JSX 防止注入攻击。React DOM 在渲染所有输入内容之前，默认会进行转义。它可以确保在你的应用中，永远不会注入那些并非自己明确编写的内容。所有的内容在渲染之前都被转换成了字符串。这样可以有效地防止 XSS（cross-site-scripting, 跨站脚本）攻击。
- 使用JSX编写模板更加简单快速
### react中使用typescript
https://simonknott.de/articles/Using-TypeScript-with-React.html  
TypeScript 是 JavaScript 的超集。TypeScript通过类型注解提供编译时的静态类型检查。

### Why import React from “react” in a functional component?
https://hackernoon.com/why-import-react-from-react-in-a-functional-component-657aed821f7a   
函数组件中使用的JSX语法只是语法糖，最终会被转译成纯粹的js语法，因此在babel转译之后，我们的代码就变成了：
```js
var App = function App() {
  return React.createElement(
    "div",
    null,
    "Hello World!!!"
  );
};
```
这里出现了React.createElement，这就是为什么我们需要在函数式组件开头引入React的原因。
