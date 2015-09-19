# Async

TODO. For now, read [the documentation](http://rackt.github.io/redux/docs/advanced/AsyncActions.html).

## redux-promise

[redux-promise] is a middleware to accept promise payloads.

[redux-promise]: https://github.com/acdlite/redux-promise

Assuming `fetchProfile()` returns a promise, create an action with a promise as a payload:

```js
Store.dispatch({
  type: 'profile:load',
  payload: fetchProfile()
})
```

Then initialize your store with react-promise middleware:

```js
import { applyMiddleware, createStore } from 'redux'
import reactPromise from 'react-promise'

const myStore = applyMiddleware(reactPromise)(createStore)

const Store = myStore((state, action) => {
  switch (action.type) {
    case 'profile:load':
      if (action.error) {
        /* error. do something with action.error */
      } else if (action.payload.then) {
        /* pending */
      } else {
        /* success. do something with action.payload */
      }
  }
})
```

Other implementations include:

- [redux-simple-promise](https://github.com/alanrubin/redux-simple-promise)
- [redux-promise-middleware](https://github.com/pburtchaell/redux-promise-middleware)
