## 4.1 Reflection 

### Simplicity
- Self explanitory: writing a solution as simple as possible. It needs to be short, clean, not have any extra logic, unnecessary variables or complicated structures. 

### Readability
- It needs to be easy for someone else to read and understand. Good practise would be keeping the variable names clear, have meaningful function names, proper spacing and a clean structure. 

### Maintainability 
- Code needs to be easy to update, improve, fix or add to in the future. clean code will also help to make chanegs without breaking anything 

### Consistency 
- Following the same structure, style and format throughout the whole project! Makes it easier to read and understand. Stick to the same naming style, indentation, file structure and coding conventions

### Efficiency 
- dont make the code complex unnecessarily; overengineering code for small or no performace gain when not needed. clean code needs to balance performance and clarity.

## Example of Messy Code
- The messy code checks if there are duplicate numbers in a list by comparing every number with every other number. It works, but it uses nested loops, unclear variable names, and is slower than needed.

```python
def t(n):
    x = 0
    for i in range(len(n)):
        for j in range(i + 1, len(n)):
            if n[i] == n[j]:
                x += 1
    if x > 0:
        return True
    return False

```

## Cleaner Version 
- The cleaner code also checks for duplicates, but it uses a set to keep track of numbers that have already been seen. This makes the code shorter, easier to read, and much faster.

```python 
def contains_duplicate(numbers):
    seen_numbers = set()

    for number in numbers:
        if number in seen_numbers:
            return True
        seen_numbers.add(number)

    return False
```