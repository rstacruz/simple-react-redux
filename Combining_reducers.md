# Chained stores

Keep your reducers in an object.

```js
function counter (state = {}, action) {
  switch (action.type) {
  case '@@redux/INIT': /* special event emitted by redux */
    return { ...state, counter: 0 }

  case 'counter:increment':
    return { ...state, counter: state.counter + 1 }

  case 'counter:set':
    const { value } = action
    return { ...state, counter: value }
  }
})
```

Combine them using [combineReducers](http://rackt.github.io/redux/docs/api/combineReducers.html).

```js
import { createStore, combineReducers } from 'redux'
const Store = createStore(combineReducers({
  counter
})
```
