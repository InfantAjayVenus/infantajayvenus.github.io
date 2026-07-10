**Tags**: #react #core #web-dev 

---

#### Re-Renders
A Re-Render is when a component that is already mounted, is being repainted/remounted to the DOM.

A necessary re-render would've been triggered by an update in the direct dependency of a component, i.e., some data that the component is dependent on to display the correct info.

An un-necessary re-render would've been caused by an inefficient app architecture or incorrect state management, where one or more components are being re-rendered despite none of the data those components depend on, has been changed.

### Causes of Re-Renders
1. State Change
2. Parent Re-Render
3. Context Change
4. Hook Changes (state or context inside a hook changes)

> Note: `prop` changes don't trigger a re-render on it's own, unless the component is memoized. `prop` changes are usually caused by a re-render on the parent.

#### Dos and Don'ts to Prevent Re-Render
##### 1. Don't create components inside the render method
##### 2. Keep the State as Low as required
##### 3. Passing children as props prevents re-renders of the children


---
Reference: [# React re-renders guide](https://www.developerway.com/posts/react-re-renders-guide?ref=dailydev#part3.1)