# Two-Step updates

As more and more features get packed into the firmware the binary image grows bigger. Until a few weeks ago it was one of my requirements to build images below the 512000 bytes size. That's the maximum size of an image so two of them would fit in a 1MB flash memory using the '1M (no SPIFFS)' memory layout.

The flash memory is split into 4096 bytes sectors, so a 1MB flash memory has 256 sectors. One of those sectors is used for EEPROM and 4 more are reserved space at the end of the flash. That leaves us with 251 sectors for code (assuming no SPIFFS partition). And that means the code must not be larger than 125 sectors to be able to do OTA. That's 512000 bytes or 500Kb.

ESPurna is close to that limit and I have sacrificed some features that are disabled by default so the limit is not met. But with the release of Arduino Core 2.4.0 things have gone worst on the size battle, albeit much better on other aspects.

That's why I'm starting to use another approach: **the two-steps updates**. The idea behind it is to flash a stripped-down version of the firmware first, lighter and with the minimum features required to flash it again with the real, full-featured image. This lighter version is the ESPurna Core binary and right now it's 290Kb. This means that using this method you can now flash an image of up to ~712Kb.

Of course, it's not as easy as it is doing a single flash, but I think it's worth it.

