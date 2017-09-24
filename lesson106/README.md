# Todo List v2.0

我们在上一章已经配置好了一个比较完整的开发环境了，后面的开发我们都可以直接使用上一章的示例中的 .babelrc 
.eslintrc package.json webpack.config.js 等文件中的相关配置，根据需要添加或修改即可 (说白了，把这些文
件拿过来，`npm install` 一下环境就搭好了) 。当然，网上也有很多类似的脚手架工具，其中开发 React 最方便的脚
手架莫过于官方的 [create-react-app](https://github.com/facebookincubator/create-react-app) 工具
了，基本上可以一键搭建好一个现成的 React 开发环境。其配置的内容和方便程度也是远胜与之前章节提到的 (其实前面
章节都是在熟悉和使用脚手架里面用到的一些工具) 。

在引言里我们提到要实现一个多人共享的开发的 Todo List 应用，现在就让我们开始完善我们的代码。在这一章里我们还是
使用原生的两个库，然后尝试按官方文档里 `thinking-in-react` 的思路来设计我们的应用。

## thinking-in-react

1. 画模型图

~~作为一个程序猿直男，你让我画模型图？算了吧，放弃这一步，等以后找个美工女盆友再说吧 (***伪命题***) 。~~

既然不画模型图，这里就头脑风暴一下我们的数据结构怎么设计吧，其实这也可以是一个设计的入口。我们要做一个多人共享的 
Todo List 应用，所以至少我们应该有两部分数据: 1)用户，姑且叫做 `doer` 吧 (个人不喜欢用 `user` 容易和数据库
的关键字冲突)； 2)待办，姑且叫做 `todo` 吧。两个的关联关系应该是 `doer` 1 - N `todo` ，当然如果以后要做多人
协作的 Todo 可能还需是要改成 M - N 的关系，到时候加个中间表吧，这里先不考虑。 `doer` 和 `todo` 在数据库通过
外键关联，在前台我们可以直接将 `doer` 对象赋值在 `todo` 内部，不过为了减少冗余数据，我们暂时将两组数据分开。
这样我们暂定的数据结构如下，接着就可以根据这个结构去 Mock 数据了。

```javascript
// ./src/api/data.js
export const doers = [
  { uid: 0, name: 'anonymous', pswd: '' },
  { uid: 1, name: 'admin', pswd: 'admin' },
];

export const todos = [
  { tid: 0, uid: 0, done: false, content: 'eat' },
  { tid: 1, uid: 0, done: false, content: 'code' },
  { tid: 2, uid: 1, done: false, content: 'sleep' },
];
```

关于数据结构的问题，这里多一句。向上面的数据结构我们看到 `doer` 和 `todo` 是两个集合，这种组织方式对数据库和后端
比较友好，但是在前端使用并不是很方便。由于 `todo` 需要引用 `doer` 所以在前台更常见的 `doer` 的组织方式可能是 
`{[uid]: doer}` 的形式，当然两种结构的转换其实也很简单，这里就不展开了，我们在完善功能的时候再说。

2. 将模型图拆分成组件

由于并没有真的模型图，这一部分我们还是以整理思路为主。结合 1. 中的数据，我们很自然的会想到我们应该有一个主组件 
(TodoApp) 来组织所有的功能组件，同时需要有用户部分 (Doer) 用来处理用户身份的区分，然后是代办部分 (Todo) ，这
一部分需要处理输入，所以我们可以再区分为交互部分 (AddTodo) 和展示部分 (TodoList) ，当然考虑到展示部分后续还会增
加排序、筛选等功能，这里的 (TodoList) 最好只用来整理数据，而真正要展示数据的部分，我们再单独起个组件 (TodoView)。

3. 实现静态版本的程序和组件

经过 2. 的拆分，我们大致需要的组件已经明确，接下来我们就可以根据~~(模型图)~~我们的设想去实现静态的版本。

4. 组合静态版本

5. 设计 state 的组成和实现

6. 添加交互方法

## 扩展阅读