### 1. React.Component
  > `React` 中的组件声明基于 `React` 和 `Component` —— 我们在 `import React from 'react'` 的时候就是在引入以下源码暴露出来的 `React` 对象。`TS` 下需要使用 `import * as React from 'react'` 来声明。

  ```
  // /packages/react/src/React.js

  import {Component, PureComponent} from './ReactBaseClasses';
  import {createRef} from './ReactCreateRef';

  import {
    createElement,
    createFactory,
    cloneElement,
    isValidElement,
    jsx,
  } from './ReactElement';

  const React = {
    Component,
    PureComponent,
    createContext,

    createElement: __DEV__ ? createElementWithValidation : createElement,
    cloneElement: __DEV__ ? cloneElementWithValidation : cloneElement,
    createFactory: __DEV__ ? createFactoryWithValidation : createFactory,
    isValidElement: isValidElement,
  };

  export default React;
  ```
  > 在 `class A extends Component` 或者 `class A extends React.Component` 的时候就是在继承 `React` 的 `Component` 类。而 `setState` 是定义在 `Component` 原型上的方法。

  > `React.PureComponent` 与 `React.Component` 几乎完全相同，但 `React.PureComponent` 通过 `prop` 和 `state` 的浅对比来实现 `shouldComponentUpate()`。使用 `React.PureComponent` 的时候，当对象包含复杂的数据结构，可能会因为深层的数据已改变但是视图没有更新而导致错误。当只有简单的 `prop` 和 `state` 时，才继承 `PureComponent`，或者在知道深层的数据结构已经发生改变时使用 `forceUpate()`。此外,`React.PureComponent` 的 `shouldComponentUpate()` 会忽略整个组件的子级。要确保整个子组件都是 `Pure` 的。

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

### 2. React.createElement
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
### 3. React.cloneElement()
  ```
  export function cloneElement(element, config, children) {
    invariant(
      !(element === null || element === undefined),
      'React.cloneElement(...): The argument must be a React element, but you passed %s.',
      element,
    );

    let propName;
    const props = Object.assign({}, element.props);
    let key = element.key;
    let ref = element.ref;
    const source = element._source;
    let owner = element._owner;

    return ReactElement(element.type, key, ref, self, source, owner, props);
  }
  ```

  > 以 `element` 作为起点，克隆并返回一个新的 `React` 元素（`React Element`）。生成的元素将会拥有原始元素 `props` 与新 `props` 的浅合并。新的子级会替换现有的子级。来自原始元素的 `key` 和 `ref` 将会保留。

### 4. React.isValidElement()
  ```
  export function isValidElement(object) {
    return (
      typeof object === 'object' &&
      object !== null &&
      object.$$typeof === REACT_ELEMENT_TYPE
    );
  }
  ```

  > 验证对象是否是一个 `React` 元素。返回 `true` 或 `false` 。



