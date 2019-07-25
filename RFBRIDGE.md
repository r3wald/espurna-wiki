# RFBRIDGE

RFBRIDGE module ([rfbridge.ino](https://github.com/xoseperez/espurna/blob/dev/code/espurna/rfbridge.ino)), originally created for the [Itead Sonoff RF Bridge](Hardware-Itead-Sonoff-RF-Bridge). 

Since version **1.13.6**, [combined with RF module and now allows to use standalone ESP8266 board with an external RF receiver / transmitter](https://github.com/xoseperez/espurna/pull/1693)

## MQTT

`rfin` and `rfout` topics are used to receive and send messages.
`rfraw` topic allows to send raw binary messages to the EFM8 chip <a href="#note2"><sup>(2)</sup></a>

State topic         | Example payload      | Notes
--------------------| -------------------- | -----------------
`{root topic}/rfin` | `26C0013603CA511451` | received code

Command topic                | Example payload        | Notes
---------------------------- | ---------------------- | -----------------
`{root topic}/rflearn/0/set` | `1`                    | see <a href="#note1">note 1</a> below
`{root topic}/rfout/set`     | `26C0013603CA511451`   | send code
`{root topic}/rfout/set`     | `26C0013603CA511451,3` | send code N times
`{root topic}/rfraw/set`     |                        | see <a href="#note2">note 2</a> below

## Terminal

| Command | description |
| --- | --- |
|**learn** &lt;id&gt;|Learn RF code for relay ID|
|**forget** &lt;id&gt;|Forget previously learned RF code|

## Settings

|Key|Description|Possible values|Default value|
| --- | --- | --- | --- |
|rfbOFF#|Code to turn OFF the n-th device|A string||
|rfbON#|Code to turn ON the n-th device|A string||
|rfbRX|(DIRECT) RX GPIO|0-15|-|
|rfbTX|(DIRECT) TX GPIO|0-15|-|

## RF / RFBRIDGE-DIRECT

The RF codes produced by the firmware for the "direct" modified board are different from the ones produced by the "vanilla" bridge for same remote. This was a design choice, due to the different kind of information passed by the EFM8 hardware and the [software library](https://github.com/sui77/rc-switch).

For example, running `mosquitto_sub -v -t "+/rfin"`:
```
rfbridge-vanilla/rfin 2F260186046ACE9778
rfbridge-direct/rfin C00101841800CE9778
```

Thanks to [**@pelson**](https://github.com/pelson), here is an example of how to port basic Arduino sketch code that uses RCSwitch to send messages using MQTT <a href="note3"><sup>3</sup></a>:

```
mySwitch.setProtocol(4);
mySwitch.send(2175276, 24);
```

Equivalent message for the `rfout` would be:
```
mosquitto_pub -t "rfbridge-direct/rfout/set" -m "C0040000180021312C"
```

- `C0`: The initial byte (always the same)
- `04`: Protocol 4.
- `0000`: 2 timing bytes (16 bit int?) - I wanted the timing to be defined by the protocol, not overridden.
- `18`: Bit length (24 in decimal)
- `0021312C`: The code to send (2175276 in decimal). This code is limited to 4 bytes.

### Notes
<sup name="note1">(1)</sup> Triggers a learn action. The index after the "learn" magnitude indicates the relay the code will be linked to. The payload of the message indicates the action (`0` for off, `1` for on).  

<sup name="note2">(2)</sup> Raw codes requires a special firmware in the EFM8BB1. See [Portisch/RF-Bridge-EFM8BB1](https://github.com/Portisch/RF-Bridge-EFM8BB1/) and issue #386 for more information. Full list of commands: https://github.com/Portisch/RF-Bridge-EFM8BB1/wiki/Commands

<sup name="note3">(3)</sup> https://gitter.im/tinkerman-cat/espurna?at=5d39a15be16c666d8967d6c9
