### 1. 组件简介
  > `React` 中的组件声明基于 `React` 和 `Component` —— 我们在 `import React from 'react'` 的时候就是在引入以下源码暴露出来的 `React` 对象。`TS` 下需要使用 `import * as React from 'react'` 来声明。

  ```
  // /packages/react/src/React.js

  import {Component} from './ReactBaseClasses';
  import {createRef} from './ReactCreateRef';

  const React = {
    Component,
    createContext,
    ···
  };

  export default React;
  ```
  > 在 `class A extends Component` 或者 `class A extends React.Component` 的时候就是在继承 `React` 的 `Component` 类。而 `setState` 是定义在 `Component` 原型上的方法。

  ```
  // /packages/react/src/ReactBaseClasses.js

  function Component(props, context, updater) {
    this.props = props;
    this.context = context;
    this.refs = emptyObject;
    this.updater = updater || ReactNoopUpdateQueue;
  }

  Component.prototype.isReactComponent = {};
  Component.prototype.setState = function(partialState, callback) {cC};
  Component.prototype.forceUpdate = function(callback) {};

  export {Component};
  ```
  > 当我们声明组件 `A` 的时候，其实就是继承了 `React.Component` 类，组件 `A` 拥有自己的四个属性：`props`，`context`， `refs`， `updater`，同时，也具有 `React.Component` 类原型上的方法 `setState`。

### 小结（图片源自网络）
![image](./React-picture/161da3ac88e17b3e)

### 2. 组件初始化
> 每一个 `React` 组件对象都源于 `React.createElement` 创建的 `ReactElement` 类型的对象。

```
// /packages/react/src/React.js

import {createElement} from './ReactElement';
```

> 也就是说，我们每声明一个组件，它都将拥有 `ReactElement` 对象的如下属性。在解析成真实 DOM 之前一直是 `ReactElement` 类型对象。

```
// /packages/react/src/ReactElement.js

const ReactElement = function(type, key, ref, self, source, owner, props) {
  const element = {
    type: type, // 组件的标识信息
    key: key, // DOM 结构标识，提升 update 性能
    ref: ref, // 真实 DOM 的引用
    props: props, // 子结构相关信息（有则拥有 children 字段，没有则为空）和组件属性（例如 style）
    _owner: owner, // _owner === ReactCurrentOwner.current（ReactCurrentOwner.js），值为创建当前组件的对象，默认值为 null
  };

  return element;
};
```

### 小结（图片源自网络）
![image](./React-picture/161da4dc2977eb50)


