# 风格指南

每个人写代码都有自己的个性和风格，为了让项目有更好的可维护性，我们应该减少个人风格，Dahlia 推荐大家使用以下风格。

## TypeScript

Dahlia 建议使用 TypeScript 来开发你的项目，**Type safety** 是 Dahlia 的重要特点之一，Dahlia 为 **TypeScript** 提供了一等的支持，Dahlia 内置的状态管理有完善类型支持，你几乎不需要写任何类型定义，就可以享受完整的类型智能提示。

**Type safety** 也是我创建 Dahlia 的最大初衷之一，如果你使用过 TypeScript 的方式开发 React 项目，不管是搭配 Redux 还是 Mobx，都会有些蹩脚，你很容易会因为要写各种类型定义而变得心情烦躁。


## 目录结构

Dahlia 推荐是如下的目录结构组织项目：


// TODO:
```bash
.
├── package.json
├── public
│   ├── favicon.ico
│   └── index.html
├── src
│   ├── components
│   │   └── Nav.tsx
│   ├── index.ts
│   ├── pages
│   │   ├── About.tsx
│   │   └── Home.tsx
│   ├── routes.tsx
│   └── stores
│       └── counterStore.ts
├── tsconfig.json
└── yarn.lock

```


## createStore

把 store 的分拆成属性导出，同时保留默认导出，这样你在组件内使用 store 时会更加优雅和灵活。

```javascript
// bad
import { createStore } from 'dahlia'
const counterStore = createStore({
  // options
})

export default counterStore
```

```javascript
// good
import { createStore } from 'dahlia'

export const { useStore, dispatch } = createStore({
  // options
})

export default { useStore, dispatch }
```

## state selector

使用 state selector 选择所需的 state，可以减少重复渲染的可能，提高组件的性能。

```javascript
// bad
const state = useStore(S => S)
```

```javascript
// good
const count = useStore(S => S.count)
const { count, step } = useStore(S => ({ count: S.count, step: S.step }))
```

## action selector 
使用 action selector 选择所需 dispatch 的 action，用字符串智能提示更弱，而且不能跳转到定义处，使用 action selector 你可以放心的进行代码重构，代码可维护性增加。

```javascript
// bad
dispatch('increment')
```

```javascript
// good
dispatch(A => A.increment)
```

## GraphQL String

为 GraphQL 查询命名，方便工具自动生成 typings。

```javascript
// bad
const GET_HERO = gql`
  {
    hero {
      name
    }
  }
`
```

```javascript
// good
const GET_HERO = gql`
  query Hero {
    hero {
      name
    }
  }
`
```

## useQuery·useMutate

分离 GraphQL query 字符串，把他们放在一个单独的文件个好习惯。

```javascript
// bad
const { loading, data, error } = useQuery(`
  {
    hero {
      name
    }
  }
`)
```

```javascript
// good
const GET_HERO = gql`
  query Hero {
    hero {
      name
    }
  }
`

const { loading, data, error } = useQuery(GET_HERO)
```

