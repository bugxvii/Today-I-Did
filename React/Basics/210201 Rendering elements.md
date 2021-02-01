tags: #JavaScript #React

<hr />

## Rendering Elements
An element describes what you want to see on the screen
```js
const element = <h1>Hello, world</h1>;
```

React elements are plain objects and cheap to create unlike browser DOM elements. **React DOM takes care of updating the DOM to match the react elements**.

Don't get confuse React elements with a *component*. Components are *made of* React elements.

<hr />

## Rendering an Element into the DOM
Applications built with just React normally have a single "root" DOM node.

```html
<div id="root">
	<!-- everything inside will be managed by React DOM -->
</div>
```

To render a React element into a DOM node, we pass both to `ReactDOM.render()`.
```js
const element = <h1>Hello, World!</h1>
ReactDOM.render(element, document.getElementById('root'));
```

<hr />

## Updating the Rendered Element
React elements are *immutable*. It is like a single frame in a movie. Once it's created, you cannot change its children nor attributes.

At this point, the only way to update them is to create a new element and pass it to `ReactDOM.render()`.

For example:
```js
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));}

setInterval(tick, 1000);
```
This code calls `ReactDOM.render()` every second from `setInterval()` callback.

In practice, most React apps will run `ReactDOM.render()` only once. We will soon learn how to update rendered elements without calling `ReactDOM.render()` multiple times.

<hr />

## React Only Updates What’s Necessary
React DOM compares the elements and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state.

For example, go ahead and run the previous `tick()` function and inspect it with the browser tools. Although you passed the whole `element`, you can see that only the  `Date()` (text) node whose contents have changed gets updated by React DOM.