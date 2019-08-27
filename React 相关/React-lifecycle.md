### 挂载（当组件实例被创建并插入 `DOM` 中时，其生命周期调用顺序如下）：
  - `constructor()`
  - `static getDerivedStateFromProps()`
  - `render()`
  - `componentDidMount()`

### 更新（当组件的 `props` 或 `state` 发生变化时会触发更新。组件更新的生命周期调用顺序如下）:
  - `static getDerivedStateFromProps()`
  - `shouldComponentUpdate()`
  - `render()`
  - `getSnapshotBeforeUpdate()`
  - `componentDidUpdate()`

### 卸载（当一个组件被从 `DOM` 中移除时，该方法被调用）：
  - `componentWillUnmount()`

### 错误处理（当渲染过程，生命周期，或子组件的构造函数中抛出错误时，会调用如下方法）：
  - `static getDerivedStateFromError()`
  - `componentDidCatch()`

### 1. `constructor()`
  ```
  constructor(props) {
    super(props);
    // 不要在这里调用 this.setState()，直接使用 this.state 赋值初始化 state，在其他方法中赋值需要使用 this.setState()
    this.state = { counter: 0 };
    this.handleClick = this.handleClick.bind(this);
  }
  ```

  > 如果不初始化 `state` 或不进行方法绑定，则不需要为 `React` 组件实现构造函数。在 `React` 组件挂在前，会先调用它的构造函数。在为 `React.Component` 子类实现构造函数的时候，应该在其他语句之前先调用 `super(props)`，否则，`this.props` 在构造函数中可能会出现未定义的 `bug`。如果 `state` 依赖 `props`，使用 `static getDerivedStateFromProps()` 来处理。

  > `React` 中，构造函数仅用于：1. 通过 `this.state` 初始化组件内部的 `state` 2. 为事件处理函数绑定实例

  > 组件加载的时候调用一次，初始化 `state`

### 2. `static getDerivedStateFromProps()`
  ```
  static getDerivedStateFromProps(props, state)
  ```

  > 组件每次被 `rerender` 的时候，包括在组件构建之后（虚拟 `DOM` 之后，实际 `DOM` 挂载之前），每次获取新的 `props` 或 `state` 之后；每次接收新的 `props` 之后都会返回一个对象作为新的 `state`，返回 `null` 则说明不需要更新 `state`；配合 `componentDidUpdate`，可以覆盖 `componentWillReceiveProps` 的所有用法。

### 3. `render()`
  > 创建虚拟 `DOM` ，进行 `diff` 算法，更新 `DOM` 树。`render()` 函数应该为纯函数，也就是在不修改组件 `state` 的情况下，每次调用都返回相同的结果，不会直接与浏览器交互。和浏览器交互的操作尽量放在 `componentDidMount()` 或者其他生命周期中执行。如果 `shouldComponentUpdate()` 返回 `false`，则不会调用 `render()`。

### 4. `componentDidMount()`
  > `componentDidMount()` 会在组件挂载后（也就是组件插入 `DOM` 树中）立即调用，且只调用一次。依赖于 `DOM` 节点的初始化（比如：网络请求）应该在这里处理。适合添加订阅，在 `componentWillUnmount()` 取消订阅。

### 5. `shouldComponentUpdate()`
  ```
  shouldComponentUpdate(nextProps, nextState)
  ```
  > 当 `props` 和 `state` 发生变化时，`shouldComponentUpdate()` 会在渲染执行前被调用，返回值默认为 `true`，为 `false` 时不渲染，但是并不会阻止子组件在 `state` 更改时重新渲染。首次渲染或者使用 `forceUpdate()` 时不会调用此方法。 
 
### 6. `getSnapshotBeforeUpdate()`
  ```
  getSnapshotBeforeUpdate(prevProps, prevState)
  ```
  > 在 `render()` 之后和组件 `DOM` 渲染输出之前调用。能够在组件发生更新之前从 `DOM` 中获取一些位置信息。其返回值将作为 `componentDidUpdate()` 的第三个参数。

### 7. `componentDidUpdate()`
  ```
  componentDidUpdate(prevProps, prevState, snapshot)
  ```
  > 组件加载时不调用，组件更新完成后会被立即调用。可以在这里对 `DOM` 进行操作，也可以在这里进行网络请求（如果比较了更新前后的 `props`）。首次渲染不会调用此方法。如果组件没有使用 `getSnapshotBeforeUpdate()` 生命周期，也就是说没有返回值，第三个参数将为 `undefined`。同时，如果 `shouldComponentUpdate()` 返回 `false`，则不会调用此方法。

### 8. `componentWillUnmount()`
  > 组件卸载及销毁之前直接调用。在这里应该执行必要的清理操作，比如：timer、网络请求或者在 `componentDidMount()` 中的订阅 。

### 9. `getDerivedStateFromError()`
  ```
  static getDerivedStateFromError(error)
  ```
  > 在后代组件抛出错误之后被调用，也就是说会在渲染阶段调用。它将抛出的错误作为参数，返回一个值更新 `state`。

### 10. `componentDidCatch()`
  ```
  componentDidCatch(error, info)
  ```
  > 任何一处的 `javascript` 报错都会触发。

### 总结

1. 组件基本写法
  ```
  import React, { Component } from 'react'

  export default class NewReactComponent extends Component {
      constructor(props) {
          super(props)
          // getDefaultProps：接收初始props
          // getInitialState：初始化state
      }
      state = {

      }
      static getDerivedStateFromProps(props, state) { // 组件每次被rerender的时候，包括在组件构建之后(虚拟dom之后，实际dom挂载之前)，每次获取新的props或state之后；;每次接收新的props之后都会返回一个对象作为新的state，返回null则说明不需要更新state
          return state
      }
      componentDidCatch(error, info) { // 获取到javascript错误

      }
      render() {
          return (
              <h2>New React.Component</h2>
          )
      }
      componentDidMount() { // 挂载后
          
      }   
      shouldComponentUpdate(nextProps, nextState) { // 组件Props或者state改变时触发，true：更新，false：不更新
          return true
      }
      getSnapshotBeforeUpdate(prevProps, prevState) { // 组件更新前触发

      }
      componentDidUpdate() { // 组件更新后触发

      }
      componentWillUnmount() { // 组件卸载时触发

      }
  }
  ```
2. 生命周期图示（[生命周期图示](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)）