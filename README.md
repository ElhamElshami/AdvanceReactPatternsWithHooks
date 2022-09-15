# Advance React Patterns With Hooks
### Preventing Unnecessary Renders

Let’s prevent any future performance issues by memoizing the callback:
```js
import React, { createContext, useState, useCallback } from 'react'

const ExpandableContext = createContext()
const { Provider } = ExpandableContext

const Expandable = ({children}) => {
  const [expanded, setExpanded] = useState(false)
  // look here 👇 we just use toggle in header component
  const toggle = useCallback(
    () => setExpanded(prevExpanded => !prevExpanded),
    []
  )
  const value = { expanded, toggle }
  return <Provider>{children}</Provider>
}

export default Expandable
```
[Look at here to know more about useCallback](https://react-hooks-cheatsheet.com/usecallback)
This works, but the ```value``` reference will be different on every re-render causing the Provider to re-render its children.
```
const value = useMemo(
	() => ({ expanded, toggle }), 
	[expanded, toggle]
  )
  ```
  So what means memoization in React?
  Prevent unnecessary rerenders when the props or input values stay the same.
  - Memozing things in React using?
   1- useMemo(()=>{},[array depandancy])
   2- useCallBack(()=>fun,[])
