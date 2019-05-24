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

### Tokens

Each element in an expression is called "token" (not a standard name). Tokens can be:

* Numbers, always considered as real numbers (floats)
* Operators (+, -, ...)
* Variables (starting with a $ sign)

### Stack

As I already mentioned, operands (numbers) are pushed into a stack and later operators pop the number of operands from the stack. Let's take a closer look to a simple RPN expression: `4 2 - 5 * 1 +`. The first column shows the next token to process and the third column the status of the stack after processing the token. At the beginning the stack is (usually) empty.

|token|action|stack|
|:-:|---|:-:|
|4|pushes '4' into the stack|4|
|2|pushes '2' into the stack|4<br/>2|
|-|pops 2 values from the stack<br />performs the substraction<br/>and pushes the result to the stack|2|
|5|pushes '5' into the stack|2<br/>5|
|*|pops 2 values from the stack<br />performs the multiplication<br/>and pushes the result to the stack|10|
|1|pushes '1' into the stack|10<br/>1|
|+|pops 2 values from the stack<br />performs the sum<br/>and pushes the result to the stack|11|

### Operators

Of course you need to know the vocabulary, i.e. the available operators. There are different types of operators:

* Mathematical (+, -, *, ...)
* Stack manipulation (dup, swap, ...)
* Comparison (eq, gt, cmp, ...)
* Logical (and, or, ...)
* Time management (now, hour, minute,...)
* ESPurna related (relay, channel)

The RPN Rules module is based on the [RPNLib library](https://github.com/xoseperez/rpnlib), so all operators defined there are also available here. I'm going to explain here only the custom ESPurna operators:

|Token|Description|
|---|---|
|now|Pushes the current epoch time into the stack|
|hour|Gets a timestamp from the stack and returns the hour|
|minute|Gets a timestamp from the stack and returns the minute|
|dow|Gets a timestamp from the stack and returns the day of week|
|debug|Dumps the current stack to the serial debug|
|relay|Gets a value and a relay number from the stack and changes that relay to the given status, status can be 0, 1 or 2 (toggle)|
|black|Turns off all channels (only lights)|
|update|Updates channels|
|channel|Gets a value and a channel number from the stack and changes that chanel to the given value (from 0 to 255). Does not update the light, you must call "update" at the end.|

### Variables

Variables are stored in the module context so they can be used from your expressions. Variables are fed from different sources:

* Relay status ($relay0, $relay1,...)
* Lights channel values ($channel0, $channel1,...)
* Sensors ($temperature0, $humidity0,...)
* MQTT (custom names)

By default they are persistent (meaning that once defined they are available for any rule execution in the future) but they do not persist across reboots. This behavior is called "sticky variables" and can be changed from the UI. Non sticky variables get deleted after the next rule execution. This can be useful to avoid dead locks when used with other features like relay pulses.

### MQTT variables

MQTT variables are a special type of variable that gets 

## Examples



## Terminal commands

The module exposes different terminal commands to test and evaluate expressions and variables.