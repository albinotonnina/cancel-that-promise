# Cancel that promise
Inspired by [this](https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html) article from React blog.

## isMounted is an Antipattern
The primary use case for isMounted() is to avoid calling setState() after a component has unmounted, because calling setState() after a component has unmounted will emit a warning. The “setState warning” exists to help you catch bugs, because calling setState() on an unmounted component is an indication that your app/component has somehow failed to clean up properly. Specifically, calling setState() in an unmounted component means that your app is still holding a reference to the component after the component has been unmounted - which often indicates a memory leak!


```
Warning: Can only update a mounted or mounting component. This usually means you called setState, replaceState, or forceUpdate on an unmounted component. This is a no-op.
```

# Usage
`npm install cancel-that-promise`

```javascript

import cancelable from 'cancel-that-promise'

componentDidMount() {
  this.cancelablePromise = cancelable(
    getSomethingAsync(),
    result => {
      this.setState(result)
    },
    error => console.error(error)
  );
}
componentWillUnmount() {
  this.cancelablePromise();
}

```

## TODO
- write the README!
