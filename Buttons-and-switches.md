This page is about general options you can compile-in into your ESPurna. The hardware defining settings can be found in header file ``hardware.h``

# Buttons and switches 

ESPurna supports up to 8 buttons connected to various GPIO pins. These buttons are defined using C preprocessor flag `BUTTONx_PIN` (x being a number from 1 to 8). Some buttons might be onboard, and you might have the option of connecting some additional, depending on the board you are using.

Each button can operate in number of different modes, configured using `BUTTONx_MODE` flag:
- `BUTTON_PUSHBUTTON` - connected button is of push-button type, possible events are: `pressed`, `released`, `double clicked`, `long clicked` and `long-long clicked`).
- `BUTTON_SWITCH` - connected button is actually a flip-switch, only reports the `click` event on both transitions.

In addition, each button can have additional options that are logically `ORed` with type of button:
- `BUTTON_DEFAULT_HIGH` - what should be default state of a button.
- `BUTTON_SET_PULLUP` - should internal pull-up be enabled for a given GPIO (note that not all GPIOs support pullup)

For example `-DBUTTON3_PIN=2 -DBUTTON3_MODE=4` (4 is the sum of BUTTON_PUSHBUTTON + BUTTON_SET_PULLUP) will configure Button3 on a GPIO02, will treat it as Push-button and will set the internal pull-up.

Event codes (as reported via MQTT) are (note that `released` and `click` have the same code but are generated by different types of buttons):

```
#define BUTTON_EVENT_NONE           0
#define BUTTON_EVENT_PRESSED        1
#define BUTTON_EVENT_RELEASED       2
#define BUTTON_EVENT_CLICK          2
#define BUTTON_EVENT_DBLCLICK       3
#define BUTTON_EVENT_LNGCLICK       4
#define BUTTON_EVENT_LNGLNGCLICK    5
```
To every button event an action can be assigned by setting the corresponding value to the button event define. The following button events are available
```
#define BUTTONx_PRESS
#define BUTTONx_CLICK     (what is the also used for _released_ event)
#define BUTTONx_DBLCLICK
#define BUTTONx_LNGCLICK
#define BUTTONx_LNGLNGCLICK
```
To every event, one of the following actions can be assigned:
```
BUTTON_MODE_NONE
BUTTON_MODE_ON
BUTTON_MODE_OFF
BUTTON_MODE_TOGGLE
BUTTON_MODE_AP (-> Access point mode)
BUTTON_MODE_RESET
BUTTON_MODE_FACTORY
```

> NOTE: For button mode `BUTTON_SWITCH`. only the click event is available currently, therefore configuration of other events make no sense.

By default button 2-8 are set to ``BUTTON_MODE_NONE``, while button 1 has the following defaults:
```
#define BUTTONx_PRESS           BUTTON_MODE_NONE
#define BUTTONx_CLICK           BUTTON_MODE_TOGGLE    
#define BUTTONx_DBLCLICK        BUTTON_MODE_AP
#define BUTTONx_LNGCLICK        BUTTON_MODE_RESET
#define BUTTONx_LNGLNGCLICK     BUTTON_MODE_FACTORY
```
> NOTE: If you plan using button1, please make sure you override these settings. 

# LEDs 

ESPurna supports up to 8 connected LEDs to various GPIO pins. These LEDs are defined using C preprocessor flag `LEDx_PIN` (x being a number from 1 to 8). Some LEDs might be onboard, and you might have the option of connecting some additional, depending on the board you are using.

Each LED can be bound to a relay state (see below), or operate in one of following modes, defined by `LED_MODE`:
- `LED_MODE_MQTT`: LED will be managed from MQTT (OFF by default)
- `LED_MODE_WIFI`: LED will blink according to the WIFI status
- `LED_MODE_FOLLOW`: LED will follow the state of the linked relay (check `RELAY#_LED`)
- `LED_MODE_FOLLOW_INVERSE`: LED will follow the opposite state of the linked relay (check `RELAY#_LED`)
- `LED_MODE_FINDME`: LED will be ON if all relays are OFF
- `LED_MODE_FINDME_WIFI`: A mixture of WIFI and FINDME
- `LED_MODE_ON`: LED always ON
- `LED_MODE_OFF`: LED always OFF
- `LED_MODE_RELAY`: If any relay is ON, LED will be ON, otherwise OFF
- `LED_MODE_RELAY_WIFI`: A mixture of WIFI and RELAY, the reverse of FINDME_WIFI

You can invert the LED status by set `LEDx_PIN_INVERSE` to `1`

# Relays 

ESPurna supports up to 8 connected relays to various GPIO pins. These relays are defined using C preprocessor flag `RELAYx_PIN` (x being a number from 1 to 8).

Example:

``#define RELAY1_PIN        4`` defines that relay 1 is connected to GPIO4

Each relay can operate in one of the following modes: 
- `RELAY_TYPE_NORMAL` - High-level-trigger, normally open relay.
- `RELAY_TYPE_INVERSE` - Either low-level-trigger, or normally closed relay. 
- `RELAY_TYPE_LATCHED`- Relay is controlled with two normally-low GPIOs, if `set` GPIO goes up the relay will turn on, if `reset` GPIO goes up the relay will turn off
- `RELAY_TYPE_LATCHED_INVERSE`- Relay is controlled with two normally-high GPIOs, if `set` GPIO goes down the relay will turn on, if `reset` GPIO goes down the relay will turn off

## Binding buttons, relays and LEDs

ESPurna has ability to change relay state based on the event coming from a button and set a LED status accordingly.

To do that, one should define `BUTTONx_RELAY` with a relay number that's "bound" to a switch. 
So, for example `-DBUTTON1_PIN=10 -DRELAY2_PIN=11  -DBUTTON1_RELAY=2` will configure Button1 on GPIO10, Relay2 on GPIO11, and will connect Button1 to Relay2.

To also reflect Relay2 state (as defined above) on a LED1 connected to GPIO02, one should configure: `-DLED1_PIN=2 -DLED1_RELAY=2` in addition to the above line. 


