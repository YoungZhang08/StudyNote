### 1. 基础组件
- `router components`（路由器组件）
- `router matching components`（路由匹配组件）
- `navigation components`（导航组件）
> 所有的组件使用前提是引入 `react-router-dom`

  #### 路由器组件
  `react-router` 是 `react-router-dom` 的基础，`react-router-dom` 提供两种路由，分别是 `<BrowserRouter>` 和 `<HashRouter>`。通常来讲，如果你有服务端的动态支持建议使用 `<BrowserRouter>`，否则建议使用 `<HashRouter>`。

  #### 路由匹配组件
  - `<Route>`
  - `<Switch>` ：`<Switch>` 组件一般负责将 `<Route>` 组件组合到一起
  > 路由匹配是通过将 `<Route>` 的 path 与当前位置的路径名进行比较来完成路由匹配。`<Switch>` 将迭代其所有的子 `<Route>` 元素，并仅渲染与当前位置匹配的第一个元素。当多个路径的路径匹配相同的路径名，动态路由转换的时候没有识别到与当前位置匹配的路径时，会渲染 404 组件。

  #### 路由渲染属性
  - `component`（有要呈现的现有组件或者无状态功能组件就使用 `component` 属性）
  - `render`（只有在必须将范围内变量传递给要渲染的组件时才应使用 `render`，它采用内联函数。不能使用带有内联函数的组件 `prop` 来传递范围内变量，因为得将不需要的组件卸载/重新安装）
  - `children`

  #### 导航组件
  - `<Link>`（`<link>` 组件用来创建链接，无论在哪儿使用 `<Link>`，在 `HTML` 中都会呈现出 `<a>`。）
  - `<NavLink>`（`<NavLink>` 是 `<Link>` 的一种特殊类型，它可以和 `prop` 动态匹配当前位置。要想强制导航，可以使用 `<Redirect>`，`<Redirect>` 将使用 `prop` 进行导航）。

### 2. 常用 API

  #### `<BrowserRouter>`
  > 使用 H5 的 `pushState`， `replaceState` 和 `popState` 事件保持 UI 和 URL 的同步。
  ```
  <BrowserRouter 
    basename={optionalString} // 如果 URL 不在网站根目录，而是子目录，需要设置这个属性
    forceRefresh={optionalBool} // 在不支持 H5 history API 的浏览器中，需要设置这个属性
    getUserConfirmation={optionalFunc} // 用于确认导航的功能，默认使用 window.confirm
    keyLength={optionalNumber} // location.key 的长度，默认为 6
  />
  ```

  #### `<HashRouter>`
  > 使用 URL 的哈希部分（也就是 `window.location.hash` ）保持 UI 和 URL 的同步，用于支持旧版浏览器。
  ```
  <HashRouter 
    basename={optionalString} // 如果 URL 不在网站根目录，而是子目录，需要设置这个属性
    getUserConfirmation={optionalFunc} // 用于确认导航的功能，默认使用 window.confirm
    hashType={optionalString} // 可用值包括：slash（创建像 #/ 和 #/sunshine/lollipops 这样的哈希），noslash（创建像 # 和 #sunshine/lollipops 这样的哈希） 和 hashbang（创建像 #!/ 和 #!/sunshine/lollipops 这样的哈希，默认 slash）
  />
  ```

  #### `<Link>`
  `to` 属性：控制跳转地址，可传入字符串或者对象
  ```
  <Link
    to={{
      pathname: "/courses",
      search: "?sort=name",
      hash: "#the-hash",
      state: { fromDashboard: true }
    }}
  />
  ```
  
  #### `<NavLink>`
  ```
  <NavLink
    to="/faq" // path
    exact // 如果为 true，仅在位置完全匹配时才应用动态类/样式
    activeClassName="selected" // 动态类名
    activeStyle={{
      fontWeight: "bold",
      color: "red"
    }} // 动态类的样式
    strict // 如果为 true，则在确定位置是否与当前 URL 匹配时，将考虑 path 尾部的斜杠
    isActive={oddEvent} // 用于添加额外逻辑以确定链接是否处于活动状态的功能
  >
    FAQs
  </NavLink>
  ```

  #### `<Redirect>`
  > 将导航重定向到新位置，新服务将覆盖历史堆栈中的当前位置，如服务端重定向（HTTP 3xx）
  ```
  <Redirect
    push // 如果为true，重定向将把新条目推送到历史记录而不是替换当前的条目
    from
    exact // 完全匹配
    strict // 严格匹配
    sensitive // 大小写敏感
    to={{
      pathname: "/login",
      search: "?utm=your+face",
      state: { referrer: currentLocation }
    }}
  />
  ```




