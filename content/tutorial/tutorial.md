---
id: tutorial
title: "Tutorial: Intro to React"
layout: tutorial
sectionid: tutorial
permalink: tutorial/tutorial.html
redirect_from:
  - "docs/tutorial.html"
  - "docs/why-react.html"
  - "docs/tutorial-ja-JP.html"
  - "docs/tutorial-ko-KR.html"
  - "docs/tutorial-zh-CN.html"
---

This tutorial doesn't assume any existing React knowledge.

>Note
>
> This tutorial is adapted from the [Official React tutorial](https://reactjs.org/tutorial/tutorial.html). It's been updated to reflect more modern development practices.

## Before We Start the Tutorial {#before-we-start-the-tutorial}

We will build a small game during this tutorial. **You might be tempted to skip it because you're not building games -- but give it a chance.** The techniques you'll learn in the tutorial are fundamental to building any React app, and mastering it will give you a deep understanding of React.

>Tip
>
>This tutorial is designed for people who prefer to **learn by doing**. If you prefer learning concepts from the ground up, you might find the official [step-by-step guide](reactjs.org/docs/hello-world.html) helpful. This tutorial and the guide can also be taken as complementary to each other.

The tutorial is divided into several sections:

* [Setup for the Tutorial](#setup-for-the-tutorial) will give you **a starting point** to follow the tutorial.
* [Overview](#overview) will teach you **the fundamentals** of React: components, props, and state.
* [Completing the Game](#completing-the-game) will teach you **the most common techniques** in React development.
* [Adding Time Travel](#adding-time-travel) will give you **a deeper insight** into the unique strengths of React.

You don't have to complete all of the sections at once to get the value out of this tutorial. Try to get as far as you can -- even if it's one or two sections.

### What Are We Building? {#what-are-we-building}

In this tutorial, we'll show how to build an interactive tic-tac-toe game with React.

You can see what we'll be building here: **[Final Result](https://codesandbox.io/s/react-tutorial-template-forked-unr3i?file=/src/index.js)**. If the code doesn't make sense to you, or if you are unfamiliar with the code's syntax, don't worry! The goal of this tutorial is to help you understand React and its syntax.

We recommend that you check out the tic-tac-toe game before continuing with the tutorial. One of the features that you'll notice is that there is a numbered list to the right of the game's board. This list gives you a history of all of the moves that have occurred in the game, and it is updated as the game progresses.

You can close the tic-tac-toe game once you're familiar with it. We'll be starting from a simpler template in this tutorial. Our next step is to set you up so that you can start building the game.

### Prerequisites {#prerequisites}

We'll assume that you have some familiarity with HTML and JavaScript, but you should be able to follow along even if you're coming from a different programming language. We'll also assume that you're familiar with programming concepts like functions, objects, and arrays.

If you need to review JavaScript, we recommend reading [this guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript). Note that we're also using some features from ES6 -- a recent version of JavaScript. In this tutorial, we're using [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), [`let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), and [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) statements.

## Setup for the Tutorial {#setup-for-the-tutorial}

To quickly get started learning, you'll write code in your browser during this tutorial.

First, open this **[Starter Code](https://codesandbox.io/s/react-tutorial-template-bbcex?file=/src/index.js)** in a new tab. The new tab should display an empty tic-tac-toe game board and React code. We will be editing the React code in this tutorial.

You can now skip the second setup option, and go to the [Overview](#overview) section to get an overview of React.

### Help, I'm Stuck! {#help-im-stuck}

If you get stuck, ask in Slack! `#help-frontend` is a great place to ask questions and learn.

## Overview {#overview}

Now that you're set up, let's get an overview of React!

### What Is React? {#what-is-react}

React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called "components".

Most React components you'll see in modern React code are functions
<!--, but instead of returning a
normal JavaScript value, a component function returns what looks like HTML. Components are reusable
in exactly the same way as normal functions: when you call a component function, you run all its
logic again and you get a new copy of its return value. -->

```javascript
function ShoppingList(props) {
  return (
    <div className="shopping-list">
      <h1>Shopping List for {props.name}</h1>
      <ul>
        <li>Instagram</li>
        <li>WhatsApp</li>
        <li>Oculus</li>
      </ul>
    </div>
  );
}
// Example usage: <ShoppingList name="Mark" />
```

We'll get to the funny HTML-like tags soon. We use components to tell React what we want to see on the screen. When our data changes, React will efficiently update and re-render our components.

Here, ShoppingList is a **React component function**, which is just a normal function that happens to represent a React component. A component function takes in parameters (called `props` in React&mdash;short for "properties"), and returns a hierarchy of views to display.

A React component function returns a *description* of what you want to see on the screen. React takes the description and displays the result. In particular, a component function returns a **React element**, which is a lightweight description of what to render.

Most React developers use a special syntax called "JSX" which makes these structures easier to write. JSX is the HTML-like syntax inside the return value of this component. If this doesn't look like valid JavaScript to you, it's because it’s not: when we “build” the version of the app that gets sent to a real web browser, the `<div />` syntax is automatically transformed into a series of function calls that look like `React.createElement('div')`. The example above is equivalent to:

```javascript
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```

If you're curious, `createElement()` is described in more detail in the [API reference](https://reactjs.org/docs/react-api.html#createelement), but we won't be using it in this tutorial. Instead, we will keep using JSX.

JSX comes with the full power of JavaScript. You can put *any* JavaScript expressions within braces inside JSX. And each React element returned by a call to `createElement` is a JavaScript object that you can store in a variable or pass around in your program.

The `ShoppingList` component above only renders built-in DOM components like `<div />` and `<li />`. But you can compose and render custom React components too. For example, we can now refer to the whole shopping list by writing `<ShoppingList />`. Each React component is encapsulated and can operate independently; this allows you to build complex UIs from simple components.

### Inspecting the Starter Code {#inspecting-the-starter-code}

You should have the **[Starter Code](https://codesandbox.io/s/react-tutorial-template-bbcex?file=/src/index.js)** open in a new tab.

This Starter Code is the base of what we're building. We've provided the CSS styling so that you only need to focus on learning React and programming the tic-tac-toe game.

By inspecting the code, you'll notice that we have three React components:

* Square
* Board
* Game

The Square component renders a single `<button>` and the Board renders 9 squares. The Game component renders a board with placeholder values which we'll modify later. There are currently no interactive components.

### Passing Data Through Props {#passing-data-through-props}

To get our feet wet, let's try passing some data from our Board component to our Square component.

We strongly recommend typing code by hand as you're working through the tutorial and not using copy/paste. This will help you develop muscle memory and a stronger understanding.

In the `renderSquare` function inside the Board component, change the code to pass a prop called `value` to the Square:

```js
function Board() {
  const renderSquare = (i) => <Square value={i} />;
  ...
}
```

With function components, props are passed as an object which is the function’s first parameter. Add the `props` parameter to the Square component function, and change the Square component to show that value by replacing `{/* TODO */}` with `{props.value}`:

```js
function Square(props) {
  return <button className="square">{props.value}</button>;
}
```

Before:

![React Devtools](../images/tutorial/tictac-empty.png)

After: You should see a number in each square in the rendered output.

![React Devtools](../images/tutorial/tictac-numbers.png)

Congratulations! You've just "passed a prop" from a parent Board component to a child Square component. Passing props is how information flows in React apps, from parents to children.

### Making an Interactive Component {#making-an-interactive-component}

Let's fill the Square component with an "X" when we click it.
First, change the button tag that is returned from the Square component's `render()` function to this:

```javascript
function Square(props) {
  return (
    <button className="square" onClick={() => console.log('click')}>
      {props.value}
    </button>
  );
}
```

If you click on a Square now, you should see 'click' in your browser's devtools console.

>Note
>
>We’re using the [arrow function syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) for an easier way to define functions inline.
>
>Notice that when we write `onClick={() => console.log('click')}`, we're passing *a function* as the `onClick` prop. React will only call this function after a click. Forgetting `() =>` and writing `onClick={console.log('click')}` is a common mistake, which would lead `console.log('click')` to fire every time the component re-renders.

As a next step, we want the Square component to "remember" that it got clicked, and fill it with an "X" mark. To "remember" things, components use **state**.

A normal function’s behavior is only controlled by the arguments it's passed. When a function is used as a React component, we can augment its behavior with special functions called **hooks**. The state hook will allow a specific square to remember whether it's been clicked, between renders.

Function components can have a piece of state by calling `useState`. Let's store the current value of the Square as a piece of state, and change it when the Square is clicked.

First, import the `useState` hook from React. Change the first line to
```javascript
import React, { useState } from 'react';
```

Now, all we need to do to access state is call `useState` and pass it an initial value:

```javascript
function Square(props) {
  const [value, setValue] = useState(null);

  return (
    <button className="square" onClick={() => { console.log('click'); }}>
      {props.value}
    </button>
  );
}
```

Now we'll change the Square component to display the value we're keeping track of in state, and to change its state when clicked:

* Replace `props.value` (the value we're passed) with `value` (the internal value we're "remembering") inside the `<button>` tag.
* Replace the `onClick={...}` event handler with `onClick={() => setValue('X')}`.

After these changes, the Square component looks like this:

```javascript
function Square(props) {
  const [value, setValue] = useState(null);
  return (
    <button className="square" onClick={() => setValue("X")}>
      {value}
    </button>
  );
}
```

By calling `setValue` from an `onClick` handler in the Square's `render` method, we tell React to re-render that Square whenever its `<button>` is clicked. After we call `setValue`, React runs our whole component function again, but this time it gives us (through the `useState` hook) the updated `value` of `'X'`, rather than the initial value of `null`. We'll see the `X` on the game board where we told React to display `value`. If you click on any Square, an `X` should show up.

### Developer Tools {#developer-tools}

The React Devtools extension for [Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) and [Firefox](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/) lets you inspect a React component tree with your browser's developer tools.

<img src="../images/tutorial/devtools.png" alt="React Devtools" style="max-width: 100%">

The React DevTools let you check the props and the state of your React components.

After installing React DevTools, you can right-click on any element on the page, click "Inspect" to open the developer tools, and the React tabs ("⚛️ Components" and "⚛️ Profiler") will appear as the last tabs to the right. Use "⚛️ Components" to inspect the component tree.

**However, note there are a few extra steps to get it working on CodeSandbox:**

1. Save the file you're editing
2. Copy the URL (something like https://xxxxx.csb.app/) from the embedded preview window and open it in a new tab
3. In this new tab, your app should be open as the full page. Use the "⚛️ Components" devtools pane in that new tab.

## Completing the Game {#completing-the-game}

We now have the basic building blocks for our tic-tac-toe game. To have a complete game, we now need to alternate placing "X"s and "O"s on the board, and we need a way to determine a winner.

### Lifting State Up {#lifting-state-up}

Currently, each Square component maintains its own state. To check for a winner, we'll maintain the value of each of the nine squares in one location, rather than in nine separate places.

You may think that Board should just ask each Square for the Square's state. Although this approach is possible in React, we discourage it because the code becomes difficult to understand, susceptible to bugs, and hard to refactor. Instead, the best approach is to store the game's state in the parent Board component instead of in each Square. The Board component can tell each Square what to display by passing a prop, [just like we did when we passed a number to each Square](#passing-data-through-props).

**To collect data from multiple children, or to have two child components communicate with each other, you need to declare the shared state in their parent component instead. The parent component can pass the state back down to the children by using props; this keeps the child components in sync with each other and with the parent component.**

Lifting state into a parent component is common when React components are refactored -- let's take this opportunity to try it out.

Add a piece of state to the board and set the its initial value to contain an array of 9 nulls corresponding to the 9 squares:

```javascript
function Board() {
  const [squareValues, setSquareValues] = useState(new Array(9).fill(null));
  ...
```

When we fill the board in later, the `squareValues` array will look something like this:

```javascript
[
  'O', null, 'X',
  'X', 'X', 'O',
  'O', null, null,
]
```

The `renderSquare` function in the Board currently looks like this:

```javascript
  renderSquare(i) {
    return <Square value={i} />;
  }
```

In the beginning, we [passed the `value` prop down](#passing-data-through-props) from the Board to show numbers from 0 to 8 in every Square. In a different previous step, we replaced the numbers with an "X" mark [determined by Square's own state](#making-an-interactive-component). This is why Square currently ignores the `value` prop passed to it by the Board.

We will now use the prop passing mechanism again. We will modify the Board to instruct each individual Square about its current value (`'X'`, `'O'`, or `null`). We have already defined the `squares` array in the Board's constructor, and we will modify the Board's `renderSquare` method to read from it:

```javascript
  const renderSquare = (i) => <Square value={squareValues[i]} />;
```

Each Square will now receive a `value` prop that will either be `'X'`, `'O'`, or `null` for empty squares.

Next, we need to change what happens when a Square is clicked. The Board component now maintains which squares are filled. We need to create a way for the Square to update the Board's state. Since state is considered to be private to a component that defines it, we cannot update the Board's state directly from Square.

Instead, we'll pass down a function from the Board to the Square, and we'll have Square call that function when a square is clicked. We'll change the `renderSquare` method in Board to:

```javascript{5}
  const renderSquare = (i) => (
    <Square
      value={squareValues[i]}
      onClick={() => handleClick(i)}
    />
  );
```

>Note
>
>We split the returned element into multiple lines for readability. Wrapping parentheses are required whenever JSX code spans multiple lines.

Now we're passing down two props from Board to Square: `value` and `onClick`. The `onClick` prop is a function that Square can call when clicked. We'll make the following changes to Square:

* Replace `value` with `props.value`
* Replace `setValue()` with `props.onClick()` in Square's `render` method
* Delete the `useState` call from Square because Square no longer keeps track of the game's state

After these changes, the Square component looks like this:

```javascript
function Square(props) {
  return (
    <button className="square" onClick={() => props.onClick()}>
      {props.value}
    </button>
  );
}
```

When a Square is clicked, the `onClick` function provided by the Board is called. Here's a review of how this is achieved:

1. The `onClick` prop on the built-in DOM `<button>` component tells React to set up a click event listener.
2. When the button is clicked, React will call the `onClick` event handler that is defined in Square's `render()` method.
3. This event handler calls `props.onClick()`. The value of the Square's `onClick` prop was specified by the Board.
4. Since the Board passed `onClick={() => handleClick(i)}` to Square, the Square calls `handleClick(i)` in Board when clicked.
5. We have not defined the `handleClick()` method yet, so our code crashes. If you click a square now, you should see a red error screen saying something like "handleClick is not a function".

>Note
>
>The DOM `<button>` element's `onClick` attribute has a special meaning to React because it is a built-in component. For custom components like Square, the naming is up to you. We could give any name to the Square's `onClick` prop or Board's `handleClick` method, and the code would work the same. In React, it's conventional to use `on[Event]` names for props which represent events and `handle[Event]` for the methods which handle the events.

When we try to click a Square, we should get an error because we haven't defined `handleClick` yet. We'll now add `handleClick` to the Board class:

```javascript{4-8}
function Board() {
  const [squareValues, setSquareValues] = useState(new Array(9).fill(null));

  const handleClick = (i) => {
    const newSquareValues = squareValues.slice();
    newSquareValues[i] = 'X';
    setSquareValues(newSquareValues);
  }
  const renderSquare = (i) => (
    <Square value={squareValues[i]} onClick={() => handleClick(i)} />
  );

  const status = "Next player: X";
  return (
    <div>
      <div className="status">{status}</div>
      <div className="board-row">
        {renderSquare(0)}
        {renderSquare(1)}
        {renderSquare(2)}
      </div>
      <div className="board-row">
        {renderSquare(3)}
        {renderSquare(4)}
        {renderSquare(5)}
      </div>
      <div className="board-row">
        {renderSquare(6)}
        {renderSquare(7)}
        {renderSquare(8)}
      </div>
    </div>
  );
}
```

After these changes, we're again able to click on the Squares to fill them, the same as we had before. However, now the state is stored in the Board component instead of the individual Square components. When the Board's state changes, the Square components re-render automatically. Keeping the state of all squares in the Board component will allow it to determine the winner in the future.

Since the Square components no longer maintain state, the Square components receive values from the Board component and inform the Board component when they're clicked. In React terms, the Square components are now **controlled components**. The Board has full control over them.

Note how in `handleClick`, we call `.slice()` to create a copy of the `squares` array to modify instead of modifying the existing array. We will explain why we create a copy of the `squares` array in the next section.

### Why Immutability Is Important {#why-immutability-is-important}

In the previous code example, we suggested that you create a copy of the `squares` array using the `slice()` method instead of modifying the existing array. We'll now discuss immutability and why immutability is important to learn.

There are generally two approaches to changing data. The first approach is to *mutate* the data by directly changing the data's values. The second approach is to replace the data with a new copy which has the desired changes.

#### Data Change with Mutation {#data-change-with-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};
player.score = 2;
// Now player is {score: 2, name: 'Jeff'}
```

#### Data Change without Mutation {#data-change-without-mutation}
```javascript
var player = {score: 1, name: 'Jeff'};

var newPlayer = {...player, score: 2};
// Now player is unchanged, but newPlayer is {score: 2, name: 'Jeff'}
// See https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax for details on this syntax
```

The end result is the same but by not mutating (or changing the underlying data) directly, we gain several benefits described below.

#### Complex Features Become Simple {#complex-features-become-simple}

Immutability makes complex features much easier to implement. Later in this tutorial, we will implement a "time travel" feature that allows us to review the tic-tac-toe game's history and "jump back" to previous moves. This functionality isn't specific to games -- an ability to undo and redo certain actions is a common requirement in applications. Avoiding direct data mutation lets us keep previous versions of the game's history intact, and reuse them later.

#### Detecting Changes {#detecting-changes}

Detecting changes in mutable objects is difficult because they are modified directly. This detection requires the mutable object to be compared to previous copies of itself and the entire object tree to be traversed. If we mutate objects directly, we also may not even *have* previous copies of the object.

Detecting changes in immutable objects is considerably easier. If the immutable object that is being referenced is different than the previous one, then the object has changed.

#### Determining When to Re-Render in React {#determining-when-to-re-render-in-react}

The main benefit of immutability is that it helps you build _pure components_ in React. Immutable data can easily determine if changes have been made, which helps to determine when a component requires re-rendering.

You can learn more about `shouldComponentUpdate()` and how you can build *pure components* by reading [Optimizing Performance](https://reactjs.org/docs/optimizing-performance.html#examples).

### Taking Turns {#taking-turns}

We now need to fix an obvious defect in our tic-tac-toe game: the "O"s cannot be marked on the board.

We'll keep track of whose move it is, and set the first move to be "X" by default. We can add another piece of state to our Board:

```javascript{3}
function Board() {
  const [squareValues, setSquareValues] = useState(new Array(9).fill(null));
  const [xIsNext, setXIsNext] = useState(true);
```

Each time a player moves, `xIsNext` (a boolean) will be flipped to determine which player goes next and the game's state will be saved. We'll update the Board's `handleClick` function to flip the value of `xIsNext`:

```javascript{3,5}
  const handleClick = (i) => {
    const newSquareValues = squareValues.slice();
    newSquareValues[i] = xIsNext ? 'X' : 'O';
    setSquareValues(newSquareValues);
    setXIsNext(!xIsNext);
  };
```

With this change, "X"s and "O"s can take turns. Try it!

Let's also change the "status" text in Board so that it displays which player has the next turn:

```javascript{1}
  const status = `Next player: ${xIsNext ? 'X' : 'O'}`;

  return (
    // the rest has not changed
```

After applying these changes, you should have this Board component:

```javascript{3,6-9,15}
function Board() {
  const [squareValues, setSquareValues] = useState(new Array(9).fill(null));
  const [xIsNext, setXIsNext] = useState(true);

  const handleClick = (i) => {
    const newSquareValues = squareValues.slice();
    newSquareValues[i] = xIsNext ? 'X' : 'O';
    setSquareValues(newSquareValues);
    setXIsNext(!xIsNext);
  };
  const renderSquare = (i) => (
    <Square value={squareValues[i]} onClick={() => handleClick(i)} />
  );

  const status = `Next player: ${xIsNext ? 'X' : 'O'}`;
  return (
    <div>
      <div className="status">{status}</div>
      <div className="board-row">
        {renderSquare(0)}
        {renderSquare(1)}
        {renderSquare(2)}
      </div>
      <div className="board-row">
        {renderSquare(3)}
        {renderSquare(4)}
        {renderSquare(5)}
      </div>
      <div className="board-row">
        {renderSquare(6)}
        {renderSquare(7)}
        {renderSquare(8)}
      </div>
    </div>
  );
}
```

### Declaring a Winner {#declaring-a-winner}

Now that we show which player's turn is next, we should also show when the game is won and there are no more turns to make. Copy this helper function and paste it before the Board function:

```javascript
function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  const matchingLine = lines.find(([a, b, c]) => squares[a] && squares[a] === squares[b] && squares[a] === squares[c]);
  const winner = matchingLine ? squares[matchingLine[0]] : null;
  return winner;
}
```

Given an array of 9 squares, this function will check for a winner and return `'X'`, `'O'`, or `null` as appropriate.

We will call `calculateWinner(squareValues)` in the Board's `render` function to check if a player has won. If a player has won, we can display text such as "Winner: X" or "Winner: O". We'll replace the `status` declaration in the Board component with this code:

```javascript{1-7}
  const winner = calculateWinner(squareValues);
  let status;
  if (winner) {
    status = `Winner: ${winner}`;
  } else {
    status = `Next player: ${xIsNext ? 'X' : 'O'}`;
  }

  return (
    // the rest has not changed
```

We can now change the Board's `handleClick` function to ignore a click (by returning early) if someone has won the game or if a Square is already filled:

```javascript{3-5}
  const handleClick = (i) => {
    const newSquareValues = squareValues.slice();
    // Return early if someone has won or if a square is filled
    if (calculateWinner(squareValues) || squareValues[i]) return;
    newSquareValues[i] = xIsNext ? 'X' : 'O';
    setSquareValues(newSquareValues);
    setXIsNext(!xIsNext);
  };
```

Congratulations! You now have a working tic-tac-toe game. And you've just learned the basics of React too. So *you're* probably the real winner here.

## Wrapping Up {#wrapping-up}

Congratulations! You've created a tic-tac-toe game that:

* Lets you play tic-tac-toe,
* Indicates when a player has won the game,

Nice work! We hope you now feel like you have a decent grasp of how React works.

Check out the final result here: **[Final Result](https://codesandbox.io/s/react-tutorial-template-forked-unr3i?file=/src/index.js)**.

If you have extra time or want to practice your new React skills, here are some ideas for improvements that you could make to the tic-tac-toe game which are listed in order of increasing difficulty:

1. Rewrite Board to use two loops to make the squares instead of hardcoding them.
2. When someone wins, highlight the three squares that caused the win.
3. When no one wins, display a message about the result being a draw.

Throughout this tutorial, we touched on React concepts including elements, components, props, and state. For a more detailed explanation of each of these topics, check out [the official React docs](https://reactjs.org/docs/hello-world.html).
