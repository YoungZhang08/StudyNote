### 1. entry
  ```
  // entry 设置 webpack 的编译入口
  module.exports = {
    entry: './path/to/my/entry/file.js'
  };

  // 单页应用（分离应用程序入口和第三方库入口）
  const config = {
    entry: {
      app: './src/app.js', // 应用程序入口
      vendors: ['react', 'react-dom'] // 第三方库入口
    }
  };

  // 多页应用
  const config = {
    entry: {
      pageOne: './src/pageOne/index.js',
      pageTwo: './src/pageTwo/index.js',
      pageThree: './src/pageThree/index.js'
    }
  };
  ```

### 2. output
  ```
  // output 设置 webpack 在哪里输出 bundles，以及如何命名这些文件，默认值为 ./dist
  const path = require('path');

  module.exports = {
    entry: './path/to/my/entry/file.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'my-first-webpack.bundle.js'
    }
  };

  // 创建了多个单独的 chunk，并使用 hash 输出文件
  {
    output: {
      filename: '[name].[hash].js',
      path: '[name].[hash].js'
    }
  }
  ```

### 3. loader
  ```
  // 处理非 js 文件，loader 可以将所有类型的文件转换成 webpack 能够处理的有效模块
  const path = require('path');

  module.exports = {
    entry: './path/to/my/entry/file.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'my-first-webpack.bundle.js'
    },
    module: {
      rules: [
        {
          test: /\.css$/,
          use: [
            { loader: 'style-loader' },
            {
              loader: 'css-loader',
              options: {
                modules: true
              }
            }
          ]
        }
      ]
    }
  };
  ```

  > loader 支持链式传递。能够对资源使用流水线(pipeline)。一组链式的 loader 将按照相反的顺序执行。loader 链中的第一个 loader 返回值给下一个 loader。在最后一个 loader，返回 webpack 所预期的 JavaScript。

  > loader 可以是同步的，也可以是异步的。

  > loader 运行在 Node.js 中，并且能够执行任何可能的操作。

  > loader 接收查询参数。用于对 loader 传递配置。

  > loader 也能够使用 options 对象进行配置。

  > 除了使用 package.json 常见的 main 属性，还可以将普通的 npm 模块导出为 loader，做法是在 package.json 里定义一个 loader 字段。

  > loader 能够产生额外的任意文件。

### 4. plugins
  ```
  // 打包优化和压缩，重新定义环境中的变量
  const path = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
  const webpack = require('webpack'); // 用于访问内置插件

  module.exports = {
    entry: './path/to/my/entry/file.js',
    output: {
      path: path.resolve(__dirname, 'dist'),
      filename: 'my-first-webpack.bundle.js'
    },
    module: {
      rules: [
        { 
          test: /\.txt$/, // 标识转换哪些文件
          use: 'raw-loader' // 用哪个 loader 进行转换
        }
      ]
    },
    plugins: [
      new webpack.optimize.UglifyJsPlugin(),
      new HtmlWebpackPlugin({template: './src/index.html'}) // 可以在一个配置文件中因为不同目的而多次使用同一个插件，需要通过使用 new 操作符来创建它的一个实例。
    ]
  };
  ```

### 5. mode
  ```
  // webpack.development.config.js
  module.exports = {
    mode: 'development'
    plugins: [
      new webpack.NamedModulesPlugin(),
      new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("development") }),
    ]
  }

  // webpack.production.config.js
  module.exports = {
    mode: 'production',
    plugins: [
      new UglifyJsPlugin(/* ... */),
      new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("production") }),
      new webpack.optimize.ModuleConcatenationPlugin(),
      new webpack.NoEmitOnErrorsPlugin()
    ]
  }
  ```