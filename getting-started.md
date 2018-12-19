# 快速上手

欢迎使用 Dahlia，在本指南，你将花 1 分钟左右，学会使用 Dahlia CLI 构建并运行一个简单的 Dahlia 应用。

## 第一步: 安装 Dahlia CLI

推荐使用 yarn 安装

```bash
yarn global add dahlia-cli
```

国内用户可以用淘宝镜像，先设置 alias:

```bash
alias tyarn="yarn --registry https://registry.npm.taobao.org"
yarn global add dahlia-cli
```

## 第二步: 初始化应用

```bash
dh new my-app
```

它将在当前文件夹中创建一个名为 my-app 的目录，目录结构如下：

```bash
.
├── README.md
├── node_modules
├── package.json
├── public
│   └── index.html
├── src
│   ├── pages
│   ├── routes.ts
│   └── index.tsx
└── tsconfig.json
```

## 第三步: 启动开发服务器

```bash
cd my-app
dh dev
```

启动成功后，然后访问浏览器：

![](http://forsigner.com/images/dahlia/dahlia-app.png)

查看完整代码：

[![Edit dahlia-tutorial-01](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/k570o3p4jo)

至此，你已经完成了 Dahlia 的基本体验。

