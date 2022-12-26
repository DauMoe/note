- `Pure function` is function doesn't raise any side effect (update global variable) when executing

- Why couldn't use `async` inside `useEffect`? (refer [here](https://ultimatecourses.com/blog/using-async-await-inside-react-use-effect-hook))
   - React expects `useEffect` returns the cleanup function or nothing but `async` return a Promise so we will raise the memory leak here

- `useEffect` and `useLayoutEffect`
   - `useEffect` run after render component. Suppose, we click button -> setState -> re-render -> update UI -> trigger useEffect (if setState inside useEffect, component will be re-rendered again)
   - `useLayoutEffect` has the same function as `useEffect` BUT run **BEFORE** update the UI (before re-render). Same example, button is clicked -> setState -> render component -> trigger useLayoutEffect -> update UI

- `useImperativeHandle`: customize the instance value and exposed *(expose: trưng bày)* to parent component when using `ref`