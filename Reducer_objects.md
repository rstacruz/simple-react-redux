# Reducer objects

Use [redux-action]. The [handleActions()] is particularly useful.

```js
createStore(handleActions({
  'counter:increment': (state) => ({
    ...state,
    counter: state.counter + 1
  }),
  'counter:set': (state, action) => ({
    ...state,
    counter: action.value
  })
}, { counter: 0 })

[redux-action]: https://github.com/acdlite/redux-actions
[handleActions()]: https://github.com/acdlite/redux-actions#handleactionsreducermap-defaultstate
