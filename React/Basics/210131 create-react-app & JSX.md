tags: #React #JavaScript #JSX #english

<hr />

## create-react-app
I wanted to set-up my own environment instead of using JSFiddle or Codepen, so I used `create-react-app`.

```shell
$ npx create-react-app my-app
```

Detail explanations can be find at the [official website](https://create-react-app.dev).

You can edit `/src/App.js`. 

## Hello World
Run your server. It'll probably use the port 3000 by default.
```shell
$ cd my-app
$ yarn start
```

Change the body of `App.js` and save it. It will automatically reload and you'll see `Hello, World!` displayed on the page.
```js
function App() {
  return (
    <div className="App">
      <h1>Hello, World!</h1>
    </div>
  );
}

export default App;
```

## Introducing JSX

```js
const element = <h1>Hello, World!</h1>
```

This funky style is neither a JavaScript string nor HTML. It's a syntax extension to JavaScript and JSX stands for _JavaScript XML_.

It allows us to write HTML code in React which makes it easier to read and write the HTML in React.

### embedding JSX
```js
function App() {
	const name = "Eubug";
	const element = <h1>Hello, {name}!</h1>;
	
	return (
		<div className="App">
			{element}
		</div>
	);
}

export default App;
```

When you reload, you will see `Hello, Eubug!`.

We can use curly braces to embed any valid JS expressions in JSX like the variable `name` we used above in the code.

In the example below, we embed the result of a function call from `formatName()`.

```js
function App() {
  function formatName(user) {
    return user.firstName + ' ' + user.lastName;
  }

  const user = {
    firstName: "Bug",
    lastName: "Eu"
  };
  
  const element = (
    <h1>
      Hello, {formatName(user)}!
    </h1>
  );

  return (
    <div className="App">
      {element}
    </div>
  );
}

export default App;

```

### style recommendation
Take a look at the JSX code below:
```js
const element = (
	<h1>
		Hello, {formatName(user)}!
	</h1>
);
```

When splitting codes in JSX, react community (or the official doc) recommends to wrap the code with a parenthesis to avoid the pitfalls of [automatic semicolon insertion](https://stackoverflow.com/questions/2846283/what-are-the-rules-for-javascripts-automatic-semicolon-insertion-asi).

### JSX is an expression too!
After compilation, JSX expressions become a regular JS function calls and objects. So we can use JSX inside conditionals, loops, assign it to variables, accept it as arguments, and return it from functions.

```js
function getGreeting(user) {
	if( user.name === "Eubug" ) {
		return <div>Nice to meet you, {user.name}!</div>
	} else {
		return <div>Uhh... yeah :) Hello!</div>
	}
}
```

### Specifying attributes in JSX
1. quotes -> use quotes to specify string literals as attributes.
	```html
	const element = <div tabIndex="0"></div>;
	```
2. curly braces -> use curly braces to embed expression in an attribute.
	```html
	const element = <img src={user.avatarUrl}></img>;
	```

We cannot use both. 

### JSX prevents [Injection Attacks](https://www.acunetix.com/blog/articles/injection-attacks/)

```js
const userInput = response.potentialMaliciousUserInput;

// this is safe
const element = <h1>{userInput}</h1>
```

By default, React DOM [escapes](https://stackoverflow.com/questions/7381974/which-characters-need-to-be-escaped-in-html) any values embedded in JSX before rendering them. Everything is converted into a string before rendering them; therefore, it is safe from [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting) attacks.

### JSX represents objects
Babel compiles JSX down to `React.createElement()` calls.

These two examples are identical:
- JSX
	```js
	const element = (
		<h1 classname="greeting">
			Hello, World!
		</h1>
	);
	```
- `React.createElement()`
	```js
	const element = React.createElement(
		'h1',
		{className: 'greeting'},
		'Hello, World!'
	);
	```

`.createElement()` performs a few checks to help you write the bug-free code, but essentially it creates an object like this:
```js
/* Note: this is simplied */
const element = {
	type: 'h1',
	props: {
		className: 'greeting',
		children: 'Hello, World!'
	}
};
```

These objects are called **React elements**.

## Reference
- https://www.freecodecamp.org/news/learning-react-roadmap-from-scratch-to-advanced-bff7735531b6/
- https://reactjs.org/docs/hello-world.html