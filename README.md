# Reverse Polish Notation Caclculator

Let's use one of our favorite data structures to make a reverse polish notation calculator.

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
1. Save the result of `2 + 3`, `5`, for later!
1. We see the number `4`. Save for later!
1. We see the operator `*`
1. Fetch the last two numbers and solve `5 * 4`
1. Save the result of `5 * 4`, `20`, for later!
1. We see the operator `+`
1. Fetch the last two numbers and solve `1 + 20`
1. Save the result of `1 + 20`, `21`, for later!
1. We are out of items to iterate through, so we are done! There should be one item saved which is the answer to the problem
1. Return the answer, which is `21`. Blackjack!

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
      # If operator: Solve for the operator with the last two numbers (Two pops, then a push) 
      # If number: Save for later (Push to stack)
  # return the one item remaining on the stack
  
calculate('9 2 +')
```

### Some Assumptions

You can assume that you will be given a valid input - you don't need to solve for mismatched operators or empty input.

### Some Hints

Having trouble getting started? Keep in mind that your first solution doesn't have to be the *best* solution. You can always go back and make it pretty later. Use big ugly if statements, don't get tripped up on making an elegant solution. Additionally, solve for the simple cases before worrying about how to do the more complex cases!

Once you've solved for the simple case run through the test cases and then, if any are failing, visit the "gotchas" section below. 

### Some Gotchas...

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

*This is valid! Expected Value: 282*

#### 3. Order matters... sometimes!

You may find that your code works for `+` and `*` but not for `-`, `/`, and `%`. This is known in math as the commutative property. For example, `4 + 2` and `2 + 4` are always going to return the same thing. Addition and multiplication are commutative, but division and subtraction are not! When grabbing the "last two" numbers to solve for your operator, order matters! 

#### 4. Your return value should be a number, not a string

Does your function work for a length of 1 number? For example, if I just passed in the string `'2'`, will your function give me back the number `2`?

## Test Cases

Think you're ready to roll? Try these out by copying and pasting them at the bottom of your file!

```py
# Basic Test
if calculate_rpn('2 4 +') == 6: print('✅ Passing for "2 4 +"')
else: print('🚫 Not passing for "2 4 +"')

# Test for single number as input
if calculate_rpn('2') == 2: print('✅ Passing for "2"')
else: print('🚫 Not passing for "2"')

# Test for subtraction
if calculate_rpn('2 1 -') == 1: print('✅ Passing for "2 1 -"')
else: print('🚫 Not passing for "2 1 -"')

# Test for 2-digit numbers
if calculate_rpn('12 4 *') == 48: print('✅ Passing for "12 4 *"')
else: print('🚫 Not passing for "12 4 *"')

# Test multiple calculations
if calculate_rpn('12 381 + 111 -') == 282: print('✅ Passing for "12 381 + 111 -"')
else: print('🚫 Not passing for "12 381 + 111 -"')

# Test multiple calculations
if calculate_rpn('1 2 3 + 4 * +') == 21: print('✅ Passing for "1 2 3 + 4 * +"')
else: print('🚫 Not passing for "1 2 3 + 4 * +"')
```

## Bonus

All done with time to spare? Already DRYed out your code too? Try out one of the following challenges:

1. Implement your solution to include floating point numbers. Use test cases like `1.5 3.5 +`, which should equal `5.0`.
1. Implement your solution to check for a valid input length before solving. What ratio of operators to numbers is "valid"?
1. Implement a solution for exponents
