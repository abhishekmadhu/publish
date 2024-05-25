---
type: note
tags:
  - permanent
  - zettelkasten
share: "true"
---

#permanent #programming 

- class variables in [[./Python Programming Language|Python Programming Language]] are shared across all instances. 

If we try to set the class variables with the instances (objects), then a new instance variable is created with the same name, that shadows the class variable. 
```python
class Item():
    # Defining a class variable
    parsed = 0

    def __init__(self, name):
        self.name = name


if __name__ == "__main__":
    first_item = Item(name='first')
    
    # This creates a new instance variable with the same name
    # The new instance variable "overshadows" the class variable
    first_item.parsed = 1  
    
    second_item = Item(name="second")
    print(first_item.parsed)  # prints 1 
    print(second_item.parsed) # prints 0

    Item.parsed = 3

    print(first_item.parsed)  # prints 1
    print(second_item.parsed) # prints 3

	# If we look into the class of the first item, 
	# it shows the new value of the class variable as expected
	print(first_item.__class__.parsed) # prints 3
```

This prints:
```text
1
0
1
3
3
```