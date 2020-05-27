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
