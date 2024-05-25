---
share: "true"
---


There is no precedence when the external CSS is compared to CSS in `<style>` tag in the `header`.
Inline styling is horrible idea. Never do this if possible. 
code sandbox: [stoic-cdn-r5t4q7 - CodeSandbox](https://codesandbox.io/s/stoic-cdn-r5t4q7?file=/css/style.css)
## CSS Selectors
`#id {}` - Try not to use ID when working with CSS. 
`.class {}`
`element {}`
`div, p {}` - `div` and `p`
`div p {}` - all `p` in a `div` - prefer classes when we have things like this. 
`*` - selects everything on the page - css reset 

### Cascade from [[css|css]] 
The last rule read will be used. This is why is it "cascading". 
This can be overwritten by [[css basics#Specificity in CSS|specificity]]. 
Use developer console to understand this. 

### Specificity in CSS

### Inheritance
Elements inherit things related to font and typography. 
Other things (like border and background and stuff) are not inherited. 
Font elements do not inherit things as well from their parents. 
We can make them inherit using 
`font: inherit;`

> [!note] Need to get used to this. 
> This is crazy at times. 

`!important` actually means `important`. This is something that should **never** be used. Using this means you agree that you are an idiot, and you give up. 


Color palette picking: [Coolors - The super fast color palettes generator!](https://coolors.co/)

`rem` looks at the root element. 2 rem = twice the root element. root element font size is set by the browser. `em` looks at the immediate parent. 
Since `em` is relative to parent, it it can mess up the entire tree of elements. Therefore, we generally use `em` only for padding and borders. 

`ch` - use a multiple of the character `0` of the current font. 

### Default styles set by the browser 

Can be overridden by using a css reset. 
`* {}`

`box-sizing: [border-box, content-box]`


## Pseudoclass
A pseudoclass represents the state of an element. 
`a:visited {}` will style a link that was visited earlier. 


