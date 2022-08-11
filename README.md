# Following along the ReactJS Library's tutorial - Tic Tac Toe
THis is my follow along on the [official react tutorial] to get familiar to react and it's syntax before starting my BeCode exercise to make a quiz app in React

## The Start
- I already miss angular
    - I used `npx create-react-app tic-tac-toe" and instantly npm is giving me warnings about outdate packages.... Ah well,.... I guess react is exactly what I feared.
    - After running out npm start and having a look in the files, I followed the tutorial's next step. `rm -rf src/*` rip boilerplate.
    - Now I have to setup the files for the tutorial
        - `touch /src/index.css`
        - `touch /src/index.js`
        - Copy pasta [the provided code....](https://codepen.io/gaearon/pen/oWWQNa)
    - And add React to the index.js file.
        - `import React from 'react';`
        - `import ReactDOM from 'react-dom/client';`
    - Link the css file
        - `import './index.css';`
    - Run `npm start` to test the server
        - Got the little square now.

## What Is React?
    - a JavaScript Library to build UIs
    - Component based

## First impressions
    - This is hell
    - Seems like they had lovely potatoes, and mashed them with a hammer and then without showing the process gave us a lovely plate of mashed potatoes
    - `React has a few different kinds of components, but we’ll start with React.Component subclasses:`
        - At least please just give me a link to the different kinds. Ah well, let's join the hipster train. grow a beard and follow along

## React.Component Subclasses
    - I get an example.
    - apparently I am now working with a 
        - `React Component Class` - Also called - `React Component Type`
            - Class Components take in Parameters
                - React calls them props for properties
                **Gotta love them hipsters, now paramaters are properties ?damn zucker so this is how you came up with - The Metaverse -`**
            - Class Components return a view trough a `render()` method.
                - Render returns a _React Element_
                    - Basicly a little description of what to render.
            - JSX
                - React advices the use of JSX since it makes the html structure easier to write.
                - Example of JSX in the return function, since its pretty unclear in the tutorial.(Yes I will hate untill you show me that trough your popularity you can get me a better guide towards using your library than Angular or Svelte.) :
```js
    //Call the return function
    return (
        //Crate a div. since it's a class component I give it a name
        React.createElement('div',{className:'shopping-list'},
        //Add elements to the div
        //Adding a hello world
        React.createElement('h1',
            'Hello World'
        );
        //Adding a list
        React.createElement('ul',
        //Adding list items
            react.createElement('li','List item one')
            react.createElement('li','List item two')
            react.createElement('li','List item  three')
        )
        //close the div
        )
    )
```
- This tutorial uses JSX instead of createElement() - No reason given - 
    - JSX comes with the full power of JavaScript
        - JSX allows any JavaScript expression within braces
        - Every React element is a JavaScript object
        - JSX also allows the rendering of custom React components.
            - For Example: `<ShoppingList />`
            - Every component is encapsulated and can operate independently

## Inspecting the starter code.
    - The code contains 3 components
        - Square
            - Renders one button
        - Board
            - Reneders 9 squares
        - Game
            - Renders a board with a placeholder.
    - The code is static, there is no interaction

## Passing Data Trough Props
    - Change the board's `renderSquare()` method so it passes a value to the square
    - Now make the square render the passed in prop
        - Its so weird we do not have a constructor, looks like a lot of magic numbers being replaced by the magical prop for now...
RECAP - Passing the magical props is how information flows in React

## Making a Component interactive
    - Mission: Fill the square with an X, when it's clicked turn it into an 'O'
        - Adding the event listener
            - `<button onClick={()=>{console.log('Hello click')}}></button>
            - ! writing onClick={console.log('click)} will fire every time the component rerenders. aka bad
    
    - Make the square _remember_ that it got clicked
        - STATE
            - COmponents can have state by setting this.state in their constructors
            - this.state should be handled as a private to a React component it's defined in.

        - Finally Adding the constructor!
```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```
- When you call setState in a component, React automatically updates the child components inside of it too.

## Lifting State up - AKA split dumb n smart components.
! I got hope! now, look at this. They admit everything up untill now should be itchy to me.
```the best approach is to store the game’s state in the parent Board component instead of in each Square. ```

- To collect data from multiple children
- To have two children communicate with eachother
    - We declare the shared state in their parent component
    - The parent component can pass in the shared state by using props
    - This way every component stays in sync

## Why Immutability is important
- When changing data, chainging it without mutation is important.
    - We do not change the original data directly
        - We copy, apply changes, replace the original because:
            - Complexity becomes simplicity
                - A big benefit is for example being able to undo a change, since we never destroyed the previous values.
                - Detecting changes
                    - When we change something underlying code can look at the difference between the new and the old value, since we never changed the old value.
                - When to Re-Render in react
                    - Immutabilty helps building _pure components_
                        - Immutable data can determine if changes were made.
                            - This helps determine when to re-render
***
## Functional Components
    - Funcitonal components are a simpler way to write components that:
        - Only contain a render method
        - Do not have their own state
    - We create one by:
        - Writing a function that:
            - Takes 'props' as input.
            - returns JSX that has to be rendered


## Copy Pasta la magica
    - Turn the square into a functional component
- Use provided algorithm
    - Use it to do some if checks to determine the winner.
    - Make sure the same square cannot be clicked twice.

## Adding Time travel.
- IMMUTABLE DATA SEEMS VERY IMPORTANT TO REACT
```
Unlike the array push() method you might be more familiar with, the concat() method doesn’t mutate the original array, so we prefer it.
```

- MAP()
```js
/*
In JavaScript, arrays have a map() method that is commonly used for mapping data to other data, for example:*/
const numbers = [1, 2, 3];
const doubled = numbers.map(x => x * 2); // [2, 4, 6]
```