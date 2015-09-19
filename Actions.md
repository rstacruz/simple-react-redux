# Actions

Action creators are functions that return action objects.

```js
function addTodo (title) {
  return {
    type: 'todo:add',
    title: title
  }
}
```

You can use them in `Store.dispatch()`.

```js
Store.dispatch(addTodo('Make React work'))
```

You can use [bindActionCreators()](http://rackt.github.io/redux/docs/api/bindActionCreators.html), but it's not really recommended.

```js
creators = { addTodo }
Actions = bindActionCreators(creators, Store.dispatch)

Actions.addTodo('Hello')
```

