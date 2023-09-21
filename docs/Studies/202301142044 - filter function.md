---
aliases:
  - filter function
  - filter functions
sticker: 1f4bb
share: "true"
---
A filter function can be used to filter things out of a list. 

> [!warning] Be careful of the return values
>Be careful that in some languages, the filter function filters out elements, and on some other cases returns the list of valid values. 
>
>Example:
>`myList = [1,2,3,4,5,6]`
>
>Assume that function `isEven` returns true if a number is even. 
>`const isEven = (num) => num % 2 == 0;`
>
>Now, [[202301142050 - Python List Filter Function|Python List Filter Function]] will return `[2,4,6]` whereas the the [[202301142052 - JS List Filter Function|JS List Filter Function]] will return `[1,3,5]`



