---
share: "true"
---
**Definition: Generator Functions**
A generator-function is defined like a normal function, but whenever it needs to generate a value, it does so with the yield keyword rather than return. The yield statement suspends the function’s execution and sends a value back to the caller, but retains enough state to enable the function to resume where it is left off. When resumed, the function continues execution immediately after the last yield run. ^7b11b9

When a generator sees a `yeild`, it pauses execution and returns the current value as well as the flow control to the caller. 

**Generators in different languages:**
- [[javascript generator functions|javascript generator functions]]
- [[python generator functions|python generator functions]]


