---
title: "Four Function Calculator"
layout: blog
order: 5
topic: Arrays
topic_path: /docs/algorithms/arrays/index.html
---
Build a four function calculator. Your algorithm should accept a string, which will represent an arithmetic calculation with the four basic arithmetic operators (addition, subtraction, multiplication, division). The algorithm should return the evaluated expression.

For example, given the string `"10+5*2"`, the function should return `20`.

#### Solution
Order of operations is important here. We can compute our answer in two iterations - the first iteration will compute all of the multiplication and division, and the second iteration will compute the addition and subtraction. The data structure we will use is a stack - the utility of the stack will become apparent when we talk about multiplication.

We will iterate through the string, building numbers out of substrings and also keeping track of the last seen operator. When we encounter a new operator, we can update the stack using the previous operator. If the previous operator was addition or subtraction, we will simply push the number onto the stack. If the previous operator was multiplication or division, we will pop the last element off the stack, perform the multiplication, and then push the combined value back onto the stack.

Note this solutions is much simpler than keeping track of two pointers as you iterate through the array - the stack allows us to interact with the information we have gathered in two ways, by either pushing a new element or popping the top element from the stack.

```python
def update(stack, operator, value):
  if(operator == "+"):
    stack.append(value)
  if(operator == "-"):
    stack.append(-value)
  if(operator == "*"):
    stack.append(stack.pop() * value)
  if(operator == "/"):
    stack.append(stack.pop() / value)


def compute(s):
  i = 0
  stack = []
  operator = "+"
  numstr = ""

  while(i < len(s)):
    if(s[i].isnumeric()):
      numstr += s[i]
    elif(s[i] in "+-/*"):
      num = int(numstr)
      update(stack, operator, num)

      numstr = ""
      operator = s[i]

    i += 1

  num = int(numstr)
  update(stack, operator, num)
  return(sum(stack))
```