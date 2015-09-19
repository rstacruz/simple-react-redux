# react-redux example

Simple example connecting [redux] and [react-redux] to [React].

[React]: https://facebook.github.io/react/
[redux]: https://www.npmjs.com/package/redux
[react-redux]: https://www.npmjs.com/package/react-redux

<br>

## Store

This store will dispatch any action to any number of reducers that will transform your state.

```js
import { createStore } from 'redux'

const Store = createStore(function (state = {}, action) {
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

<br>

## App

Your main component. This will listen to events from the Store.

```js
import React from 'react'
import { connect } from 'react-redux'

let App = React.createClass({
  render () {
    <div>
      Counter is {this.props.counter}
      <button onClick={this.reset}>Reset</button>
      <button onClick={this.increment}>Add</button>
    </div>
  },

  increment (e) {
    e.preventDefault()
    Store.dispatch({ type: 'counter:increment' })
  },

  reset (e) {
    e.preventDefault()
    Store.dispatch({ type: 'counter:reset', value: 0 })
  }
})

App = connect((state) => {
  return state
})(App)
```

<br>

## Mounting

Mounting your App via `React.render()` and React-Redux's `Provider` component.

```js
import { Provider } from 'react-redux'

React.render(<Provider store={Store}>
  {() => <App />}
</Provider>, document.getElementById('container'))
```
