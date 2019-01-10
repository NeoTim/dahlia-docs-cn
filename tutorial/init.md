# Init

如果你没有安装 Dahlia CLI，请看 [安装 Dahlia CLI](getting-started#di-yi-bu-an-zhuang-dahlia-cli)。

使用 Dahlia CLI 初始化应用:

```bash
dh new friends
```

初始化成功后，启动本地开发服务器：

```bash
cd friends
dh dev
```

启动成功后，在浏览器中你可以预览应用的运行效果，代码和运行效果如下：

{% code-tabs %}
{% code-tabs-item title="index.ts" %}

```typescript
import Dahlia from 'dahlia'
import { routes } from './routes'

Dahlia.bootstrap({
  routes,
  selector: '#root',
})
```

{% endcode-tabs-item %}

{% code-tabs-item title="routes.ts" %}

```typescript
import { Routes } from 'dahlia'
import { Home } from './pages/Home'

export const routes: Routes = [
  {
    path: '/',
    component: Home,
  },
]
```

{% endcode-tabs-item %}

{% code-tabs-item title="Home.tsx" %}

```typescript
import React from 'react'

export const Home = () => <div>Hi, Dahlia</div>
```

{% endcode-tabs-item %}
{% endcode-tabs %}

查看完整代码：

[![Edit dahlia-tutorial-01](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/k570o3p4jo)


