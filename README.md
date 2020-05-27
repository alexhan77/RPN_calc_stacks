# Reverse Polish Notation Caclculator

Stacks can be more useful than they seem at first! We've seen how they can make a simple bracket matcher, now let's use it to make a reverse polish notation calculator.

## What is RPN?

Reverse Polish Notation uses postfix operators instead of the typical infix operators. For example, your normal `2 + 3` becomes `2 3 +`. Pretty simple, right? But it can get more complex quickly... take this for example:

**infix version**
```py
1 + (2 + 3) * 4
```

**postfix version**
```py
1 2 3 + 4 * +
```

The expected result due to order of operations is `21`.

### How do we translate postfix to infix?

For postfix operators, such as the above `1 2 3 + 4 * +`, we can iterate through one at a time. We skip over numbers until we find an operator. Then, once we find an operator, we solve it for the *last two numbers we saw*. So, think of it this way:

1. We see the number `1`. Save for later!
1. We see the number `2`. Save for later!
1. We see the number `3`. Save for later!
1. We see the operator `+`
1. Fetch the last two numbers and solve `2 + 3`
1. Save the result of `2 + 3`, `5` for later!
1. We see the number `4`. Save for later!
1. We see the operator `*`
1. Fetch the last two numbers and solve `5 + 4`
1. Save the result of `5 + 4`, `9`, for later!
1. We see the operator `+`
1. Fetch the last two numbers and solve `1 + 9`
1. Save the result of `1 + 9`, `10`, for later!
1. We are out of items to iterate through, so we are done! There should be one item saved which is the answer to the problem
1. Return the answer, which is `10`

## Starter Code

You may have guessed from the above example that we will need a structure of some sort to "save" numbers for later. You may have inferred that the structure should be a stack because we need to access the *last* numbers put in *first* (LIFO structure!) or perhaps you guessed it because the name of this repository includes the word "stacks". Either way, astute observation!

We can start with some Python code that has a Stack class.

**Simple Stack Class in Python**

```py
class Stack:
  def __init__(self):
    self.list = []

  def pop(self):
    return self.list.pop()

  def push(self, data):
    self.list.append(data)

  def length(self):
    return len(self.list)

  def print_stack(self):
    print([str(x) for x in self.list])
```

**Stub Function**

```py
def calculate_rpn(input):
  # Declare an empty stack
  # Split the string input on spaces
  # Iterate through the input
    # Check if the item is an operator or not
      # If operator: Solve for the operator with the last two numbers
      # If number: Save for later
  # return the one item remaining on the stack
  
calculate('9 2 +')
```

### Some Assumptions

You can assume that you will be given a valid input - you don't need to solve for mismatched operators or empty input.

### Some Hints

#### 1. Remember that you will need to deal with numbers when doing math, not strings.

```py
9 + 2 == 11
```

```py
'9' + '2' == '92'
```

You can cast strings to integers using the `int()` function.

#### 2. Your solution should work for numbers with multiple digits!

Your input may contain 2 or 3 digit numbers, such as `12` or `381`. To capture these values properly, you can split your string on the space character.

```py
12 381 + 111 -
```

**This is valid! Expected Value: 282**
