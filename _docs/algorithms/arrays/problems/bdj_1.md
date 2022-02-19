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
Order of operations is important here. We can compute our answer in two iterations - the first iteration will compute all of the multiplication and division, and the second iteration will compute the addition and subtraction. The data structure we will use is a stack.

As we iterate through the string, we will keep track of the last seen operator. When we reach the end of a number, we can update the stack. If the element is added, we push the number onto the stack. If the element is multiplied, we will pop the last element off the stack, perform the multiplication, and then push the combined value back onto the stack.

Finally, we can sum the stack to finish the computation.

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