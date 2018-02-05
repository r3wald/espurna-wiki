> This method is experimental. If it doesn't work, you will have to use [standard flashing method](Binaries)

# Introduction 

You just got your Sonoff device and would like to flash it using ESPurna, but would like to avoid opening device, and even soldering?

Clever folks at [SonOTA](https://github.com/mirko/SonOTA) and [Espressif2Arduino](https://github.com/khcnz/Espressif2Arduino) have found a way to intercept iTead Sonoff OTA protocol and allow us to load any firmware built using Arduino framework, which includes ESPurna.
 
# Tested devices and firmware

This method is compatible _only_ to Itead Sonoff devices, and only those running firmware _up until 1.60_. If your device arrived with newer firmware, process will not work, so you might need to downgrade using eWeLink. This method will also not (and never) work on non Itead Sonoff devices or Itead Sonoff devices that don't have "pairing" mode.

Tested devices:

| Device | Reported by | Reported on | 
| --- | --- | --- | 
| Itead Sonoff Dual | lobradov | 2018-Feb-05 |  
| Itead Sonoff 4CH  | lobradov | 2018-Feb-05 | 

If you test/verify any other device, please update the table above.

# Needed tools 

You'd need `python3` and `pip` installed. If you don't have them, google is your best friend.

## SonOTA 

```console
$ mkdir -p ~/src/
$ cd ~/src/
$ git clone https://github.com/mirko/SonOTA.git
Cloning into 'SonOTA'...
remote: Counting objects: 284, done.
remote: Compressing objects: 100% (6/6), done.
remote: Total 284 (delta 2), reused 0 (delta 0), pack-reused 278
Receiving objects: 100% (284/284), 1.29 MiB | 1.63 MiB/s, done.
Resolving deltas: 100% (160/160), done.
$ cd SonOTA
$ pip3 install -r requirements.txt
  Downloading httplib2-0.10.3.tar.gz (204kB)
    100% |████████████████████████████████| 204kB 2.4MB/s 
Collecting netifaces>=0.10.6 (from -r requirements.txt (line 2))
  Downloading netifaces-0.10.6.tar.gz
Collecting tornado>=4.5.1 (from -r requirements.txt (line 3))
  Downloading tornado-4.5.3.tar.gz (484kB)
    100% |████████████████████████████████| 491kB 1.8MB/s 
Building wheels for collected packages: httplib2, netifaces, tornado
  Running setup.py bdist_wheel for httplib2 ... done
[...]
```
This will get you SonOTA, fake SSL certificates and stage 1 and 2 Espressif2Arduino images. 

## ESPurna image

```bash
$ cd ~/src/SonOTA/static
$ curl -fsSL https://github.com/xoseperez/espurna/releases/download/1.12.3/espurna-1.12.3-espurna-core.bin -o image_arduino.bin
```

# Steps

## 1. Starting a script

```console
$ cd ~/src/SonOTA/
$ ./sonota.py --wifi-ssid my-home-wifi-ssid --wifi-password super-secret-password --serving-host your-IP-on-home-network
Current IPs: ['10.0.2.15']

Using the following configuration:
	Server IP Address: 10.0.2.15
	WiFi SSID: my-home-wifi-ssid
	WiFi Password: *********************
Platform: linux
** Now connect via WiFi to your Sonoff device.
** Please change into the ITEAD WiFi network (ITEAD-100001XXXX). The default password is 12345678.
To reset the Sonoff to defaults, press the button for 7 seconds and the light will start flashing rapidly.
** This application should be kept running and will wait until connected to the Sonoff...

.......
[...]
```

Of course, replace "my-home-wifi-ssid", "super-secret-password" and "your-IP-on-home-network" with your actual parameters.

## 2. Booting device in "pairing mode"

At this stage, script is ready to intercept Itead OTA requests, which happen in the first few seconds of powering up Sonoff devices. 

You should power-on a Sonoff device, and press the first button for around 5s (this is the button documented in original Sonoff firmware as "pairing" button). This will create `ITEAD-100001XXXX` Wifi network.

## 3. Switching to `ITEAD-100001xxxx` network

While keeping the script running, you should switch to newly created `ITEAD-100001XXXX` network, so that script can continue:

```console
[...]
<< {
    "error": 0
}
~~ Provisioning completed
** The IP address of <serve_host> (192.168.1.10) is not  assigned to any interface on this machine.
** Please change WiFi network to $ESSID and make  sure %s is being assigned to your WiFi interface.
** This application can be kept running.
................
[...]
```

That's it :) You are just running ESPurna on your new device. Note that device will use ESPURNA-xxxxxx network for initial provisioning, but that's "business as usual". After this, you can use normal OTA to upgrade to any image you actually need, including newer versions.

You can let the script running, switch back to your home Wifi and flash another device.

