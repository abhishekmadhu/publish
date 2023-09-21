---
share: "true"
---
# React Notes

```toc
	style: number
	title: "## Table of Contents"
```
# Topics
## Section 1: Introduction
--
## Section 2: React Key Concepts

### Before React

We first had complex JS
Then we had jQuery
We got AngularJS. Good but messy as all the operations were “functional”.

### Why do we need react?

React was the first to introduce “declarative” definitions of state, and “map” it to a state of the user interface.

Angular and other frameworks quickly followed suit, but React already had the early mover advantage that it needed.

### Basic concepts

1. React will do all DOM manipulations
2. Re-usable components
3. Unidirectional data flow - from state to top component and then to child components
4. React is only for the UI

### Important skills for a React Developer

1. Decide what the components will be.
    1. How granular should they be
2. Decide the state (and where it will live)
3. What to change based on change of state
    1. Performance requirements - updating constraints


## Section 3: React Basics
### NVM and NPM
- `nvm` - Node Version Manager (manage different versions of node simultaneously) - yarn is an alternative
- `npm` - Node Package Manager - manage different packages
- `npx` - install a package, run the command, and remove the package instantly

1. **Lesson 13 - 19:** Basic settings

### Create React App
2. **Lesson 20:** `create-react-app` makes life easier by creating a boilerplate application for us. It has all the necessary folder structure and git

### How React manipulates the DOM
3. **Lesson 21:**
    1. `react` package acts as the framework
    2. `react-dom` is to work with the DOM using the react framework. `react-native` is for native components, etc.
    3. react finds an element in the body, and renders the entire apps inside that element

    `<div id="root"></div>` in `public/index.html`

    `const root = ReactDOM.createRoot(document.getElementById('root'));` in `src/index.js`
    4. there can be sister non-react elements in `public/index.js` in the application

### Builds, babel, and webpack
4. **Lesson 22:**
    1. `build`-ing a script: creates an optimised production build, and puts all into the `build` folder - generally uses babel and webpack (and some others)
        1. babel - Translate JS to basic JS that most web browsers can parse
        2. webpack - breaks the JS into smaller chunks that are navigationally separate (for example, the js of homepage should be in the homepage). It will manage all.

### How JSX works
5. **Lesson 23:**
    1. React JSX is basically HTML, but with functions that can return more HTML inside the HTML at runtime

### Ejecting Components
6. **Lesson 24:**
    1. Question:
    How is ejecting a problem? Say, I use  `npx create-react-app hello` and then start working on my project.
    Now consider two scenarios.
    **Scenario 1>>** I do not eject, and there is a new way of working with the "hidden files" (say, the web pack configuration).
    **Scenario 2>>** I eject.
    How are the two scenarios different? How will my project be updated in scenario #1, and what benefit does scenario #1 have over scenario #2?

    I used `npx`, so I do not event have create-react-app installed.

7. **Lesson 25:** Classes vs hooks - hooks are new and slightly complex
8. **Lesson 27-28:**
    1. When is react rendering and re-rendering components and which ones is the most important.
    2. Functional Components and Class Components
9. **Lesson 29-31:**
    1. When changing the state, always use `setState()` because react will only update if the object in memory is a new object
        1. `setState()` works with shallow merge - all the keys that are not provided to the object passed as parameter are not touched

### Creating multiple elements of one component
10. **Lesson 32:** `map` **-** iterates over a list of objects, and created JSX elements from each of the objects
11. **Lesson 33-34**: Key in a list
    1. Elements in a react list must have a `key` property, that denotes the unique identifier for the list element.
    2. React will use this “key” to understand what was updated and which element needs to be updated, instead of updating all the elements/nodes in the list

        ```jsx
        	<div className="App">
                {
                  this.state.monsters.map(
                    (monster) => {
                      return <div key={monster.name}>
                        <h1>{monster.name}</h1>
                      </div>
                    })
                }
            </div>
        ```

12. **Lesson 35:** Data source for applications
    1. Earlier architectures relied on multiple calls to get different web pages
    2. How SPAs work
        1. One request (theoretically) to get the code for the entire website
            1. Of course authentication and other requests are made to servers.

### Life Cycle Methods
13. **Lesson 36:**
    1. Life Cycle Methods - Events during the life cycle of a component, like getting mounted (`componentDidMount()` - details at [this link](https://reactjs.org/docs/react-component.html#componentdidmount)) or getting updated (`componentDidUpdate()`) and many more
        1. Take a look at the API reference at

            [React.Component - React](https://reactjs.org/docs/react-component.html#overview)

    2. Use native `fetch` to easily get data from a URL
    3. Promises can be chained

### Brief Order of Execution
14. Lesson 37:
    1. Order of execution of the code elements in our example
        1. `constructor()` runs first
        2. `render()`
        3. `componentDidMount()`
        4. `render()` - run again as `componentDidMount()` changed the state
15. Lesson 38

### Functionality before styling - how to think
16. Lesson 39:
    1. Always work on functionality before working on styling for frontend projects
    2. Break down the functionality of the entire app into smaller components
        1. Monster rolodex has
            1. Input field
                1. Data is filtered on each change
                2. X mark to delete data in the box
            2. Cards

### Protected Keywords
3. `class` is a protected keyword in JS, so JSX components use `className` instead of `class` from their HTML counterparts
    4. When input fields are changed, a `change event` is triggered, that can be handled by a change handler - classic pub-sub mechanism
        1. The handler can be defined as the `onchange` attribute

            ```jsx
            <input className='search-box' type='search' placeholder='search monsters' onChange={
              (event) => { console.log(event.target.value); return null; }
            } />
            ```

        2. The `event` has `[event.target](http://event.target)` that defines the state of the target of the event, which is the element that was modified
        3. The target for a input box has `value`, that shows the complete value of the text box AFTER the event was triggered
        4. The solution to the filtering
            1. Think of the state. The change in the text field changes the “state” of the application, so the `searchString` should be in the state
            2. When the state is changed, the list in the state should be filtered
            3. The original list should not be touched, as we might need to get that back - do not mutate the original list

                ```jsx
                class App extends Component {

                  constructor() {
                    console.log('constructor-begin');
                    super();

                    this.state = {
                      monsters: [],
                      **filterString: ''**
                    };
                  }

                  //
                  componentDidMount() {
                    console.log('componentDidMount-begin');
                    fetch('https://jsonplaceholder.typicode.com/users')
                      .then((response) => response.json())
                      .then((users) => {
                        this.setState(() => {
                          return { monsters: users };
                        },
                          () => {
                          console.log(this.state);
                        })
                      });
                  }

                  render() {
                    console.log('render-begin');
                    return (
                      <div className="App">
	                    <input className='search-box' type='search' placeholder='search monsters' onChange={
                          (event) => {
                            console.log(event.target.value);
                            this.setState(() => {
                              return {
                                filterString: event.target.value
                              };
                            });
                            return null;
                          }
                        } />
                        {
	                        this.state.monsters.filter((monster) => {
                            return monster.name.toString().toLowerCase().includes(this.state.filterString);
                          }).map(
                            (monster) => {
                              return <div key={monster.name}>
                                <h1>{monster.name}</h1>
                              </div>
                            })
                        }
                      </div>
                    );
                  }

                }
                ```

17. **Lesson 40-42:**
    1. Immutability is a good practice - Do not change anything in the state in a way that changes the state. Some useful functions that respect this are
        1. `map`
        2. `filter`
        3. `reduce`
    2. Rest of the lecture is basic and useless
18. **Lesson 43:**
    1. Anonymous functions are created in runtime and then throws away. Re-creating them again and again consumes time.
        1. Therefore, the `render()` should not contain anonymous functions if the functions are not changing themselves
19. **Lesson 44-45: Components**
    1. Theory
        1. Components should be more and more general-purpose
        2. One component should try to have one logically coherent job/role/responsibility
    2. Process
        1. Put components in separate folders in `src`
        2. As convention, each component folder should be named as `<componentName>.component.jsx`
        3. Must import Component from react to inherit/extend
        4. return the JSX from the component file
        5. `default export` is a cool way to set the default class to export from a file
20. **Lesson 46-47:** `props`
    1. Stands for “properties”
    2. Can be used to pass data to child components
    3. React renders on mount and also whenever props change
21. Lesson 47: Component Tree
22. Lesson 48: Using props to pass functions
23. Lesson 49: CSS in React
    1. No matter where you import a CSS file, react will build all the css into one CSS files
        1. So if one CSS in imported into one file, the CSS is applicable to all files
    2. Isolating CSS can be done with some existing libraries that we will learn later
24. Lesson 50: CardList component
25. Lesson 51-52: Separate the Card Component
26. Lesson 53:
27. Lesson 54: LifeCycle Methods - [the diagram is here](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)


    Components go through the three phases

    1. ***Mounting***
    2. ***Updating***
    3. ***Un-mounting***
28. Lesson 55:
    1. Functional components do not have life-cycles, unlike Class components
29. **Lesson 56: Pure and Impure Functions**
    1. A function is considered “pure” if the output is an isolated function of the inputs. If it is not, then it is called “impure” function
    2. Pure function - Returns the same output given the same inputs

        ```jsx
        const func = (a,b) => {return a + b}
        ```

    3. Impure function - Depends on “things” other than the inputs (like a variable outside the function

        ```jsx
        const c = 10;
        const func = (a,b) => {return a + b + c;} // variable outside function impacts the result of the function
        ```

    4. Side effects - If a function has an effect (changes something) that is outside it’s explicit scope, it is called a side effect. Side effects are also considered “impure”.

        ```jsx
        const c = 10;
        const func = (a,b) => {c = a + b + c;} // variable outside the function is being updated
        ```

    5. Hooks are generally impure functions, and they create side effects
30. **Lesson 57-58:** Hooks and functional components
    1. `useState(object)` - returns array with two values - a value and its “`setter()`”. The “value” can be initialised, and the functional component is re-rendered only when the data in value and the argument to the `setter()` are different
31. Lesson 59-60:
    1. If you are stuck in a rendering loop, you need to check if you are changing data during a render, that can trigger another render
    2. Solution is `useEffect(() => {function to run}, [in case these values change])` for functional components
        1. Can be used to run specific logic only if specific values change between subsequent renders
32. Lesson 61-62
33. Lesson 63: Some components are double rendered because of the strict mode. Use a browser extension to “grey those out”.
34. Lesson 64: DOM and Virtual DOM
    1. DOM -
        1. Making changes is expensive computationally (adding and removing nodes cost the most)
    2. Virtual DOM - A duplicate of the real DOM inside JS
        1. Computationally cheaper than the real DOM
    3. Triggering process - Need to understand better
35. Lesson 65-66: React and ReactDOM - Can be used as base libraries as well by importing the libraries into a plain vanilla HTML
36. Lesson 68:


## Section 4: Capstone Project Intro

Where to find code if needed at any time during the project:
[GitHub - ZhangMYihua/crwn-clothing-v2: Version 2 of Crwn-Clothing!](https://github.com/ZhangMYihua/crwn-clothing-v2)

1. Lesson 75: Try to work from outside to inside with boilerplate without styling. Build functionality first. 


## Section 5: React Routing
1. Lesson 81
2. Lesson 82
3. A fragment is useful to group things invisibly. The `<Fragment></Fragment>` is never rendered. 
	1. A react component is supposed to render only one parent component. Fragment can be used to group many into one without adding unnecessary "container" component
4. The routes are hierarchical, and the routes can be nested
5. An `<Outlet/>` can be used to show the components of the "child" route in the parent route
   ```jsx
   const App = () => {
		return (
			<Routes>
				<Route path='/' element={ <NavBar />}>
					<Route path='hello' element={ <Home />} />
				</Route>
			</Routes>
		);
	}
	
	const NavBar = () => {
		return (
			<div className="navbar">
				<div>This is the NavBar</div>
				<Outlet/>
			</div>
		);
	};

   
	```


![[../../../../Pasted image 20220930075320.png|Pasted image 20220930075320]]
This is what is rendered.



## Section 6


## Section 7: React Context 
Used for State Management
Sometimes the same data needs to be accessible by many components in the tree, and at different nesting levels. 
Context lets us “*broadcast*” such data, and changes to it, to all components below. 

**Common examples where using context might be simpler than the alternatives:** managing the current locale, theme, or a data cache.

### prop drilling
`prop drilling` - Passing data via props to components that need it through components that do not need it
React context helps avoid this. 
> [!note] But, if you are looking to just avoid prop drilling, [[React Udemy Course Notes#Component Composition|Component Composition]] can be a better solution. 

### Introduction to Context
React context allows us to store data.
Contexts are actually “glorified” functional components that expose their value and their state setter to the child components.

## Section 8: Observable Listeners
```jsx
// Lesson 109: Observer Pattern
//  onAuthStateChangedListener is a Listener available from "../utils/firebase/firebase.utils" in my project
useEffect(() => {
	const unsubscribe = onAuthStateChangedListener((user) => {
		if (user) {
			createUserDocumentFromAuth(user);
		}
		console.log(user);
		setCurrentUser(user);
	});
	return unsubscribe; // run unsubscribe when the component is unmounted
}, []);
```

## Section 9: React Context - Deep Dive
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

In a typical React application, data is passed top-down (parent to child) via props, but such usage can be cumbersome for certain types of props (e.g. locale preference, UI theme) that are required by many components within an application. **Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree.**

### When to Use Context
Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.

### When NOT to use Context
Context is primarily used when some data needs to be accessible by _many_ components at different nesting levels. 
Apply it sparingly because **it makes component reuse more difficult**.

> [!note] If you only want to avoid passing some props through many levels, [[React Udemy Course Notes#Component Composition|Component Composition]] is often a **simpler solution** than context.

### Context Providers


### Lesson 113: Products Context
When thinking of providers, think about what might need your provider when deciding where to put it.

A provider can access data from it’s parent provider. So, if a provider needs some data from another provider, the first provider needs to be nested inside the second provider.


## Section 10: Firebase Database Storage


## Section 11: Styled Components

### Lesson 135-139: Styling Components
1. We can use JSX files, and use `styled-components` to style a component. 
2. We can style ANY component, be it a standard div or our own components
3. Components styled "below" can extend and style a component defined "above" in the style module/file
4. Be careful while importing the styled library. Note that there are no curly braces `{}` around the import. 
	   `import styled from "styled-components";`

### Lesson 140: Passing CSS Around
To pass CSS around, use a css styled element. 

```jsx
import styled, { css } from "styled-components";

// Define the style
const shrinkLabelStyles = css`
	top: -14px;
	font-size: 12px;
	color: ${mainColor};
`;

// Use the style conditionally, based on a prop, in another component
export const FormInputLabel = styled.label`
	color: ${subColor};
	${({ shrink }) => shrink && shrinkLabelStyles};
`;

```

## Section 12 - Deploying with Netlify
### Setup
Need to update the Build Command to `CI= yarn build` so that the CI environment is used. 

### Redirects with Netlify
Create a file called `_redirects` in the `public` folder, and ask it to redirect all paths to index.html, and return a status code of 200. 
```
/* /index.html 200
```

![[../../../../Pasted image 20220909110114.png|Pasted image 20220909110114]]

## Section 13: Reducers
Reducers are a third party state management solution. 

The reducer is **a pure function that accepts 2 parameters: the current state and an action object**. 
Depending on the action object, the reducer function must update the state in an *immutable manner* (?meaning?), and return the new state.

```jsx
const userReducer = (state, action) => {
	return {
		...build and return the new state based on the action...
		...typically switch case is used...
	}
}
```

### Reducers and business logic
> [!warning] Do NOT write business logic in the reducer. 

The reducer function should only update the state, and not care about "what" to update the state to. **The exact values to be set are to be passed to the reducer in the payload**. 

### When to user Reducers
Use reducers when one event needs to update multiple values in the state/context. 

### Migration Strategies from `useState()` and `setState()` to `useReducer()`
- identify what is important to track
	- check the existing context attributes
	- we do not need the functions, just the values
	- keep the default values from the context
- To keep business logic separate from the reducers [[React Udemy Course Notes#Reducers and business logic|React Udemy Course Notes > Reducers and business logic]], think differently at this step to make the actions more generic. This is one of the greatest powers of reducers - maintaining only the state. 


## Section 14: Reducers
### Context API VS Redux
Accessibility - All the information in the global context can be accessed by all the components in case of redux. But contexts can be used to segregate the components in terms of accessibility to data 
Flow of data - 

#### How it works
We have only one parent reducer, and the state of the entire application is managed by this one reducer in a centralized manner. 
The components fire actions that one or more reducers can choose to either use (to change the global state) or ignore. 
The individual reducers are a way to compartmentalize logic, even though all the state is managed by the parent reducer. 

The individual reducers update the root reducer, which in turn, is used by the components. 
![[React Reducers.excalidraw|React Reducers.excalidraw]]

> [!note] Since all reducers react to all events in redux, it is important to return the original `state` as the `default` in the `switch-case` of every reducer when working with redux. 


#### Middleware
Middle-wares are things that are processed before and after the reducer is hit. 
They generally enhance the store, for things like logging. 
Also see: [[React Udemy Course Notes#Create own Middlewares|Createing own Middlewares]]

#### Redux root reducer 
In redux, conceptually, we have only one reducer, called the root reducer. 
To break it down to manageable parts, we split it into different reducers, and then use `combineReducers()` to combine them. 

```jsx
import { combineReducers } from "redux";
import { userReducer } from "./user/user.reducer";
import { categoriesReducer } from "./categories/category.reducer";

export const rootReducer = combineReducers({
	user: userReducer,
	categories: categoriesReducer
})
```

##### Individual Reducers
Each reducer looks like this:
```jsx
import { CATEGORIES_ACTION_TYPES } from "./category.types";

export const CATEGORIES_INITIAL_STATE = {
	categoriesMap: {}
};

export const categoriesReducer = (state = CATEGORIES_INITIAL_STATE, action) => {
	const { type, payload } = action;
	switch (type) {
		case CATEGORIES_ACTION_TYPES.SET_CATEGORIES_MAP:
			return { ...state, categoriesMap: payload };
		default:
			return state;
	}
}
```

#### The `useSelector` hook
The `useSelector` hook from `react-redux` is used to get the value of something from the global state (generally parameterized as `state`) when a component is rendered. 
It takes a function as a parameter. 
```jsx
const currentUser = useSelector([selectCurrentUser]((state) => state.user.currentUser));
```


> [!Question] Find out
> How does the internal code of React pull this off? 

### General Idea regarding reducers 
The reducers should hold the most basic form of the data (probably the data from the API, or a basic JSON converted to an object).
Then, we use `selector`s to perform different manipulations and get the data in a format that we want.  

### Lesson 157. Business Logic in Selectors

### Lesson 158: What Triggers `useSelector()`
Any changes to the redux store triggers ALL useSelector hooks. All `useSelector()`s are fired when the state of the store is changed. 
Whether the component is re-rendered is a separate thing. 
See [[React Udemy Course Notes#Reselect Library - And how to avoid triggering re-renders in|How to avoid triggering re-renders in]] to know how to avoid this. 

#### Create own Middlewares
[[currying|Currying]] can be used to create our own middlewares. 

```jsx
const loggerMiddleware = (store) => (next) => (action) => {
	if (!action.type){
		// some middlewares share actions where we do not get a type, so we just pass
		return next(action);
	}
	console.log('type: ', action.type);
	console.log('payload: ', action.payload);
	console.log('current state: ', store.getState()); // prints the prv state

	next(action); // this is synchronous, so the current middleware waits until all the reducers and next middlewares finish

	console.log('next state: ', store.getState()); // this prints the updated state
}
```


### Reselect Library - And how to avoid triggering re-renders in 
We use the `reselect` library for this, which used [[memoization|memoization]] under the hood. 
```jsx
import { createSelector } from "reselect";

const selectCategoryReducer = (state) => state.categories;
export const selectCategories = createSelector(
	[selectCategoryReducer], // the output of this array of functions is going to be the input to the next function, in order
	(categoriesSlice) => categoriesSlice.categories
);
```

![[React Course Notes - Migrating the Cart Context Exercise|React Course Notes - Migrating the Cart Context Exercise]]

## Section 15: Redux Extended Tools
### Lesson 167: [[Redux Persist|Redux Persist]]
![[Redux Persist|Redux Persist]]

### Lesson 168: Redux-Devtools
[[202301142044 - filter function|filter functions]] are a great way to filter out middlewares based on condition. 

---
> [!info]  Everything from here is needed only at scale. 

## Section 16: Redux Thunk
A flavor of asynchronous side effects inside redux. 
`yarn add redux-thunk`

I need to spot where in my application codebase I have async behavior that I want to move into an action driven flow. 

When using thunks, we must start tracking errors in the reducers, because now the reducer needs to know. 
> [!question] Why does it need to know now?
> It needs to know because thunk's greatest capability is to be able to parse these states (of processing, success, error, etc) and provide different behavior for different states. 
> For example, it can be used to show a spinner while an async action is loading. 

## Section 17: Redux Saga
[[Redux Saga|Redux Saga]]
![[Redux Saga#^130f39|Redux Saga > ^130f39]]



# Additional Stuff / Appendix
### [[Component Composition|Component Composition]]
