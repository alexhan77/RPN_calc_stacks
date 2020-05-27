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
1 2 3 + 4 *
```

The expected result due to order of operations is `21`.

