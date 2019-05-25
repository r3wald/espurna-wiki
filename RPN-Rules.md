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
|now|Pushes the current local epoch time into the stack|
|utc|Pushes the current UTC epoch time into the stack|
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

MQTT variables are a special type of variable that gets its content from MQTT topics. You can define an MQTT and a variable name and every time the topic receives a message the variables will get updated and the rules will be executed. Remember than variable names in the RPN expressions begin with the $ sign.

### Rule execution

Rules get executed X milliseconds after the last variable update. The execution delay is 100ms by default but it can be changed from the web UI. This allows for a buffer time so all variables coming from sensors get updated before rules are executed. 

All variables changes trigger the rule execution after the delay time. So every time a relay is toggled, every time a sensor reports values or every time one of the MQTT topic gets updated the rules will be executed.

## Examples

### Toggle a heater depending on a temperature sensor

Imagine you have a device with a relay controlling a heater and a temperature sensor. You can implement a simple thermostat with hysteresis using the input variables of the sensor (`$temperature0`) and the relay (`$relay0`):

```
$temperature0 18 24 cmp3 1 + 1 $relay0 0 3 index 0 relay
```
Let's split the expression in parts:

|sub-expression|description|output|
|---|---|---|
|$temperature0 18 24 cmp3|Compares the temperature to the 18-24 range, it will output -1 if temperature is below 18, +1 if it is above 24 and 0 in the middle|-1 to 1|
|1 +|We need to shift the cmp3 result to use the index operator|0 to 2|
|1 $relay0 0 3 index|We define an index of 3 different values (that's the `3` in the expression) that will be 1, the current status of the relay (0 or 1) and 0, the sub-expression will return one of them depending on the value in the stack|0 or 1|
|0 relay|It will set the relay number 0 to the status in the stack|(empty)|

This expression will ensure the relay in ON if the temperature is below 18C and OFF if it's above 24C. If the reported temperature is in between 18 and 24 the relay status will not change.

### Open light at night if there is presence

In this case image we have a simple WiFi relay device and a PIR in the same room that reports presence via MQTT to the `/livingroom/motion` topic. We first define an MQTT topic for it using `motion` as the variable name. Then we can trigger the light if there is motion between 22h and 8h in the morning.

```
now hour 8 23 cmp3 abs $motion and 0 relay
```

Again, let's analyze it step by step

|sub-expression|description|output|
|---|---|---|
|now hour|Will return the current hour|0 to 23|
|8 23 cmp3 abs|Compare the hour in the stack to the 8-23 range and get the absolute value, will output 1 if it's below 8 or above 23, 0 otherwise|0 or 1|
|$motion and|We do an AND with the motion value, so we will now have a 1 if it's nighttime AND there is motion|0 or 1|
|0 relay|We use the result value to turn on or off the relay #0|(empty)|

Since our device will only have a relay, this rule will be executed every minute (triggered by the NTP module) and when there is a new value in the motion topic. Alternatively, if you disable the "stickyness" of the variables, the expression will fail except when the `$motion` is defined which will only happen after we receive a message to the motion topic. 

Keep in mind that if the result changed the relay status, the relay change will trigger the rule execution again! Try to avoid loops in the rules like, for instance: `1 $relay0 - 0 relay`. This simple expression will turn the relay ON and OFF and ON again and OFF again forever!!

### Emulate the schedule

The schedule is different to the previous examples since it will only perform an action at a given time, not every time there is a time or status update like the RPN Rules module. But we can easily emulate this behaviour here:

```
now minute 0 ne end now hour 8 ne end 1 0 relay
```
The `end` operator takes and argument from the stack and ends the execution if the argument resolves to true. Hence:

|sub-expression|description|output|
|---|---|---|
|now minute 0 ne end|Will end the execution if the current minute is not 0|(empty)|
|now hour 8 ne end|Will end the execution if the current hour is not 8|(empty)|
|1 0 relay|Turn relay 0 to ON, this will only happen at 8:00!|

There is a small glitch here. If you turn the relay OFF while it's still 8:00 the rule will run and turn it ON again. But if it's not 8:00 the rule will not change the relay status.

### Light color following power consumption

Some devices, like the Smartlife Mini Smart Socket, have an LED light (sometime RGB) and a power consumption monitor. Wouldn't it be cool that the light would turn more and more red as the power consumption rises?

```
black $power0 0 1000 0 255 map 0 channel update
```
This expression maps a power value between 0 and 1000W to a number between 0 and 255 and then it feeds it to channel 0 (usually red). Previously it sets all channels to 0 (`black`) and at the end forces the light driver to `update` the color. Nice.

### Individually synchronize relays

ESPurna has a relay synchronization feature that offers different ways to synchronize relays when there is more than one available, but all of these options perform actions of all the relays, turning them ON or OFF to match the required pattern. What if you have 4 different relays and you want to synchronize relays 0 and 1 together but leave 2 and 3 untied? Easy.

```
$relay0 1 relay
```  

What if you want them to have opposite value?

```
1 $relay0 - 1 relay
```  

Now you can control relays 0 and 1 by just changing relay 0.

## Terminal commands

The module exposes different terminal commands to test and evaluate expressions and variables.

* **RPN.OPS** will output the list of available operators and the number of required arguments for each of them
* **RPN.TEST "&lt;expression&gt;"** will execute the expression and output the stack at the end, useful to do partial tests of sub-expressions
* **RPN.VARS** will output the current defined variables and their values
