## init

用来初始化 Dahlia，推荐在入口文件初始化，这里为什么不使用 Provider 的方式来初始化，因为初始化的配置跟子组件并没有关系，所以没必要，使用 "**Programmatically**" 的方式初始化会更清晰。

```js
import dahlia from 'dahlia'

dahlia.init({
  graphql: {
    endpoint: 'https://graphql-compose.herokuapp.com/user',
  },
  rest: {
    endpoint: 'https://jsonplaceholder.typicode.com',
  },
})
```