### 装载（这些方法会在组件实例被创建和插入 `DOM` 中时被调用）：
  - `constructor()`
  - `static getDerivedStateFromProps()`
  - `componentWillMount()` / `UNSAFE_componentWillMount()`
  - `render()`
  - `componentDidMount()`
### 更新（属性或状态的改变会触发一次更新。当一个组件在被重渲时，这些方法将会被调用）:
  - `componentWillReceiveProps()` / `UNSAFE_componentWillReceiveProps()`
  - `static getDerivedStateFromProps()`
  - `shouldComponentUpdate()`
  - `componentWillUpdate()` / `UNSAFE_componentWillUpdate()`
  - `render()`
  - `getSnapshotBeforeUpdate()`
  - `componentDidUpdate()`
### 卸载（当一个组件被从DOM中移除时，该方法被调用）：
  - `componentWillUnmount()`


### 1. constructor()

