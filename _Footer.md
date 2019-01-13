Hi.

I got the NEO and tried to flash. Connection GPIO0 to GND did not help - flashing did not work.
I had also to connect RST pad to 3.3V. After that - flashing worked perfectly even without RST connected to 3.3 V (from second flash)

Important build flags.
1. in Platformio for tasmota flag change from 1MB to 8MB is needed, otherwise flash fails.
build_flags               = ${esp82xx_defaults.build_flags}
                            -Wl,-Teagle.flash.8m.ld

2. in Arduino IDE, board selected - "Node MCU 1.0", standard

I've discovered how NEO device is connected:
// LED = GPIO4 (D2 NodeMCU)
// RELAIS = GPIO12 (D6 ModeMCU)
// BUTTON = GPIO13 (D7 NodeMCU)

