# Chained stores

Keep your reducers in an object. Each one manages a *"slice"* of the state.

```js
function counter (state = 0, action) {
  switch (action.type) {
  case 'counter:increment':
    return state + 1

  case 'counter:set':
    return action.value

  default:
    return state
  }
})

function audio (state = { status: 'stopped' }, action) {
  switch (action.type) {
    case 'audio:play':
      return { status: 'playing', position: 0 }
    case 'audio:fastforward':
      return { ...state, position: state.position + 5000 }
    default:
      return state
  }
}
```

Combine them using [combineReducers](http://rackt.github.io/redux/docs/api/combineReducers.html).

```js
import { createStore, combineReducers } from 'redux'
const Store = createStore(combineReducers({
  counter, audio
})

Store.getState()
//=> { counter: 0, audio: { status: 'stopped' } }
```

There's also [reduce-reducers] which fulfills a similar use-case.

[reduce-reducers]: https://github.com/acdlite/reduce-reducers
