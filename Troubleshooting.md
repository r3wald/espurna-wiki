## Problems resetting the board

After flashing the firmware via serial do a hard reset of the device (unplug & plug).<br>
There is an issue with the ESP.reset() method. Check [https://github.com/esp8266/Arduino/issues/1017](https://github.com/esp8266/Arduino/issues/1017) for more info.

## Undefined reference to `__ieee754_sqrt'

**FIX: You are using an old ESP8266 Core for Arduino**

```
/home/odroid/.platformio/packages/toolchain-xtensa/bin/../lib/gcc/xtensa-lx106-elf/4.8.2/../../../../xtensa-lx106-elf/lib/libm.a(lib_a-w_sqrt.o):(.literal+0x8): undefined reference to `__ieee754_sqrt'
/home/odroid/.platformio/packages/toolchain-xtensa/bin/../lib/gcc/xtensa-lx106-elf/4.8.2/../../../../xtensa-lx106-elf/lib/libm.a(lib_a-w_sqrt.o): In function `sqrt':
/home/pi/xtensa/esp-open-sdk/crosstool-NG/.build/src/newlib-2.0.0/newlib/libm/math/w_sqrt.c:69: undefined reference to `__ieee754_sqrt'
collect2: error: ld returned 1 exit status
*** [.pioenvs/sonoff-pow-debug/firmware.elf] Error 1
```

This is due to a missing function in a core library (https://github.com/esp8266/Arduino/issues/612, not related to ESPurna). It will be probably solved with 2.4.0 version of ESP8266 Core for Arduino. In the meantime a quick fix is to replace the "(...toolchain-xtensa...)/xtensa-lx106-elf/sysroot/lib/libm.a" with the file one: [https://files.gitter.im/esp8266/Arduino/Abqa/libm.a.tbz](https://files.gitter.im/esp8266/Arduino/Abqa/libm.a.tbz).

## Wifi Stops

* First check you supply enough voltage to ESP8266. Not all power supplies are the same.