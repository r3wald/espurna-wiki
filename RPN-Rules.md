# RPN Rules

The "RPN Rules" module is an advanced feature that let's you define pretty flexible custom rules to execute actions (mostly changing relay and light statuses) based on different inputs. Rules are defined as a series of commands using [Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation), also called "postfix" notation, where operators come after the operands.

This might look somewhat complicated but it actually has major benefits over the usual "infix" notation:

* Commands (rules) are faster to process
* Rules are simple to understand
* It's easier to implement

## Main concepts

### Postfix notation

First you should familiarize yourself with RPN calculation. Reverse Polish notation (RPN) is a mathematical notation in which operators follow their operands. It does not need any parentheses as long as each operator has a fixed number of operands.

A simple calculation in infix notation might look like this:

```
( 4 - 2 ) * 5 + 1 =
```

The same calculation in RPN (postfix) will look like this:

```
4 2 - 5 * 1 +
```

It results in a shorter expression since parenthesis are unnecessary. Also the equals sign is not needed since all results are stored in the stack. From the computer point of view is much simpler to evaluate since it doesn't have to look forward for the operands.

### Stack

As I already mentioned, operands (numbers) are pushed into a stack and later operators pop the number of operands from the stack. Let's take a closer look to a simple RPN expression: `4 2 - 5 * 1 +`. Each element in the expression is called "token" (not a standard name). The first column shows the next token to process and the third column the status of the stack after processing the token. At the beginning the stack is (usually) empty.

|token|action|stack|
|:-:|---|:-:|
|4|pushes '4' into the stack|4|
|2|pushes '2' into the stack|4<br/>2|
|-|pops 2 values from the stack<br />performs the substraction<br/>and pushes the result to the stack|2|
|5|pushes '5' into the stack|2<br/>5|
|*|pops 2 values from the stack<br />performs the multiplication<br/>and pushes the result to the stack|10|
|1|pushes '1' into the stack|10<br/>1|
|+|pops 2 values from the stack<br />performs the sum<br/>and pushes the result to the stack|11|