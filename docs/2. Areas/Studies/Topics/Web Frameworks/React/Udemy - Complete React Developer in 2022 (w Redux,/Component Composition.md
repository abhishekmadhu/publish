---
share: "true"
---


Component composition is the name for **passing components as props to other components**, thus creating new components with other components.
```jsx
const Button = ({ onClick, children }) => (   // The {children} is a prop
 <button onClick={onClick}>{children}</button>
);

const App = () => {
  const onClick = () => alert('Hey 👋');

  return (
    <Button onClick={onClick}>Click me!</Button>
  );
};
```

```jsx
const App = () => {
	const onClick = () => alert('Hey 👋');
	return (
		<Button onClick={onClick}>
			<img src="/logos/logo.svg" />      Click me!     // Only one child is sent here, but we can send more
		</Button>
	);
};
```

### Composition Prevents Prop Drilling 
[[./React Udemy Course Notes#prop drilling|Prop drilling]] is undesirable and bad. 

Instead of passing `anyProp` through many different layers, we can try to compose the components at a higher level, like the `App` component.

```jsx
const App = () => {
  const userName = 'Joe';

  return (
    <WelcomePage title={<WelcomeMessage userName={userName} />} />
  );
}

const WelcomePage = ({ title }) => {
  return (
    <>
      {title}
      {/** Some other welcome page code */}
    </>
  );
}

const WelcomeMessage = ({ userName }) => {
  return (
    <h1>Hey, {userName}!</h1>
  );
}
```

*Source: https://felixgerschau.com/react-component-composition/#how-can-composition-help-prop-drilling*
