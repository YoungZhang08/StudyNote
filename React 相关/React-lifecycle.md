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

