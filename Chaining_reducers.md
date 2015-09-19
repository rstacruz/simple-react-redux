# Chained stores

Keep your reducers in an object.

```js
const CounterReducers = {
  'counter:increment': (state) => {
    return { ...state, counter: state.counter + 1 }
  },

  'counter:set': (state, {value}) => {
    return { ...state, counter: value }
  }
}
```

Build your store from these reducer sets.

```js
const Store = createChainStore([
  CounterReducers
])
```

Here's what will make it work.

```js
import { createStore } from 'redux'

function createChainStore (reducers) {
  let store = createStore((state = {}, action) => {
    let reduced

    reducers.forEach(function (red) {
      if (red[action.type]) {
        reduced = true
        state = red[action.type].call(store, state, action)
      }
    })

    if (!reduced && action.type.substr(0, 2) !== '@@') {
      throw new Error(`Store: unknown action type '${action.type}'`)
    }

    return state
  })

  return store
}
```
