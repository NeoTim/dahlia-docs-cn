---
name: 自定义 webpack 配置
order: 960
---

# 自定义 webpack 配置

为了自定义 webpack 配置，需要在项目根目录新建配置文件 `dahlia.config.js`，然后在 config 对象中定义一个名为 webpack 的函数。

```js
// dahlia.config.js
module.exports = {
  webpack(config, env) {
    return {
      ...config,
      // to custom origin config
    }
  },
}
```

## 自定义原理

原理非常简单，在 webpack 函数返回新的 `config` 即可。因为 dahlia-cli 是基于 create-react-app 开发的，所以原始的配置对象可以看 react-scripts 中的 [`webpack.config.js`](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/config/webpack.config.js#L126)。

下面是个简单的例子，修改 webpack 的 publicPath 配置:

```js
// dahlia.config.js
module.exports = {
  webpack(config, env) {
    const newConfig = {
      ...config,
      // 自定义 webpack publicPath
      publicPath: 'http://0.0.0.0',
    }
    return newConfig
  },
}
```

## 使用 override 工具简化配置

上面介绍了如何修改 webpack 配置，但是修改原始的配置对象并不简单，下面介绍如何借助一些工具简化修改配置的过程。

安装覆写 config 的工具库:

```bash
yarn add dahlia-webpack-override
```

安装修改 config 的 operator:

```bash
yarn add dahlia-webpack-less
```

让 dahlia 支持 Less:

```js
// dahlia.config.js
const override = require('dahlia-webpack-override')
const less = require('dahlia-webpack-less')

module.exports = {
  webpack(config, env) {
    const newConfig = override(config, env).pipe(less())
    return newConfig
  },
}
```

## 使用多个 operator

下面展示了如何同时使用多个 operator，让 ant-design 支持修改主题：

```js
const override = require('dahlia-webpack-override')
const antd = require('dahlia-webpack-antd')
const less = require('dahlia-webpack-less')

module.exports = {
  webpack(config, env) {
    const newConfig = override(config, env).pipe(
      less({
        modifyVars: {
          'primary-color': 'black',
          'link-color': '#1DA57A',
          'border-radius-base': '10px',
        },
        javascriptEnabled: true,
      }),
      antd({
        style: true,
      }),
    )

    return newConfig
  },
}
```

## 如何编写自己的 operator

operator 是一个函数：

```js
const myOperator = (options?: any) => config => {
  const newConfig = {
    ...config,
    // to customize
  }
  return newConfig
}

export default myOperator
```

## dahlia 提供 config operater

- [dahlia-webpack-less](https://github.com/forsigner/dahlia-webpack-override/blob/master/packages/dahlia-webpack-less/README.md)
- [dahlia-webpack-antd](https://github.com/forsigner/dahlia-webpack-override/blob/master/packages/dahlia-webpack-antd/README.md)
- [dahlia-webpack-styled-components](https://github.com/forsigner/dahlia-webpack-override/blob/master/packages/dahlia-webpack-styled-components/README.md)
