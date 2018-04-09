
## 这是 react 组件的生命周期
#### 一、生命周期介绍
1. 在组件的整个生命周期中，随着该组件的props或者state发生改变，它的DOM表现也将有相应的改变，一个组件就是一个状态机，对于特定的输入，它总会返回一致的输出。
2. React为每个组件提供了生命周期钩子函数去响应不同的时刻——实例化期、存在期及销毁时。

#### 二、生命周期方法

实例化期    存在期   销毁期
>  组件的生命周期，包含的主要几种情况：
>  组件被实例化的时候
>  组件属性改变的时候
>  组件状态被改变的时候
>  组件被销毁的时候


#### 生命周期图示

![Image react-life](http:////)

#### 实例化期

```react
首次调用组件时，有以下方法会被调用（注意顺序，从上到下先后执行）：
    getDefaultProps
这个方法是用来设置组件默认的props，组件生命周期只会调用一次。但是只适合React.createClass直接创建的组件，使用ES6/ES7创建的这个方法不可使用，ES6/ES7可以使用下面方式：
```
```react
    //es7
    class Component {
    static defaultProps = {}
    }
    //或者也可以在外面定义es6
    //Compnent.defaultProps
```
```react
componentWillMount
条件：第一次渲染阶段在调用 render 方法前会被调用
作用：该方法在整个组件生命周期只会被调用一次，所以可以利用该方法做一些组件内部的初始化工作,这个是在render方法调用前可修改state的最后一次机会。
render
JSX通过这里，解析成对应的虚拟DOM，渲染成最终效果。
```
```react
componentDidMount
条件：第一次渲染成功过后，组件对应的 DOM 已经添加到页面后调用
作用：这个阶段表示组件对应的 DOM 已经存在，我们可以在这个时候做一些依赖 DOM 的操作或者其他的一些如请求数据，和第三方库整合的操作。如果嵌套了子组件，子组件会比父组件优先渲染，所以这个时候可以获取子组件对应的 DOM。
```

----------------------------------------------
#### 存在期
```react
实例化后，当props或者state发生变化时，下面方法依次被调用：
componentWillReceiveProps(newProps)
条件： 当组件获取新属性的时候，第一次渲染不会调用
用处： 这个时候可以根据新的属性来修改组件状态
```
shouldComponentUpdate(nextProps, nextState)
条件： 接收到新属性或者新状态的时候在 render 前会被调用（除了调用 forceUpdate 和初始化渲染以外）
用处： 该方法让我们有机会决定是否重渲染组件，如果返回 false，那么不会重渲染组件，借此可以优化应用性能（在组件很多的情况）.
```react
componentWillUpdate
条件：当组件确定要更新，在 render 之前调用
用处：这个时候可以确定一定会更新组件，可以执行更新前的操作
注意：方法中不能使用 setState ，setState 的操作应该在 componentWillReceiveProps 方法中调用
Render
和实例化时的render一样

```
```react
componentDidUpdate
条件：更新被应用到 DOM 之后
用处：这个方法在更新真实的DOM成功后调用，当我们需要访问真实的DOM时，这个方法就也经常用到。
```
```react
销毁阶段，只有一个函数被调用：
componentWillUnmount
没当组件使用完成，这个组件就必须从DOM中销毁，此时该方法就会被调用。当我们在组件中使用了setInterval，那我们就需要在这个方法中调用clearTimeout。

```