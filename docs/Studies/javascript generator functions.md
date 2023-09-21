---
share: "true"
---

Example Declaration of [[generator functions|generator functions]] in [[Javascript|Javascript]]:
```js
function* gen(i){
	yeild i;
	yeild i + 10;
}

const g = gen(5); 

const gObj1 = g.next(); // gObj1 gets: {value: 5, done: false}
const gObj2 = g.next(); // gObj2 gets: {value: 15, done: false}
const gObj3 = g.next(); // gObj3 gets: {value: undefined, done: true}
```

returns `{value: <returnvalue>, done: <boolean>}` 

If we use a `return`, then during this return, the `done` will be set to `true`.

```js
function* gen(i){
	yeild i;
	yeild i + 10;
	return 105;
}

const g = gen(5); 

const gObj1 = g.next(); // gObj1 gets: {value: 5, done: false}
const gObj2 = g.next(); // gObj2 gets: {value: 15, done: false}
const gObj3 = g.next(); // gObj3 gets: {value: 105, done: true}
```