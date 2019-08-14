### 1. 组件的实现与挂载
  > `React` 中组件声明基于 `React` 和 `Component`，我们在 `import React from 'react'` 的时候就是在引入以下源码暴露出来的 `React` 对象。`TS` 下需要使用 `import * as React from 'react'`。

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
  > 在 `extends Component` 的时候就是继承了 `React` 的 `Component` 类。`extends Component` 也可以写成 `extends React.Component`。

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

### 小结
![image](./React-picture/161da3ac88e17b3e)