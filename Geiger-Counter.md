# ESPurna based Geiger Counter

The wiring of this project is straight forward. I used a NodeMCU board to host ESPurna.  
The Geiger counter itself is based on aa Arduino-ready Kit from [RH Electronics](http://www.rhelectronics.net/store/radiation-detector-geiger-counter-diy-kit-second-edition.html).
![Wiring Diagram](https://github.com/Trickx/espurna/blob/dev/images/devices//geiger_wiring_diagram.png)
The Geiger board is prepared for two variants of interrupt outputs. I soldered the C-Int type, consisting of 10nF capacitor in front of the output. The corresponding impulse looks like this.

![Scope screenshot of Geiger impulse](https://github.com/Trickx/espurna/blob/dev/images/devices/geiger_scope_single_pulse.png)

Yes, I know the NodeMCU is a 3V3 powered device, while the Geiger board runs at 5V. Well, the interrupt impuls shows a peak of below 4V and it did not kill my NodeMCU, yet. Use this wiring at your own risk :-) However the impuls shows a width of 20ms, so I decided to go with a debounce time of 25ms, just to be sure. Debouncing does not seem to be required here, but I wanted to be on the safe side. I will test the system with different settings but for the moment rising edge detection is configured. The closest time between two impulses I could fetch while playing with the scope was about 50ms. This would result in a quiet high radiation level.

![Scope screenshot of 2 folowing Geiger impulses](https://github.com/Trickx/espurna/blob/dev/images/devices/geiger_scope_following_pulses.png)

## Calibration
The Geiger counter board generates an interrupt per detection.
One way to measure the local (Gamma) dose rate is therefore to count the impulses per minute [CPM].
CPMs depend on the used geiger tube. Im my case an russian SBM-20.
In other words CPMs are not comparable with other geiger tubes.

The Sievert [Sv] is the unit of ionizing radiation dose in the International System of Units (SI).
We need a dose rate (per time interval). The most common one is micro Sievert per hour [µSv/h].

But how to convert from CPM to µSv/h?

A web search will end up an large list of conversion factors.
For example [here](https://sapporohibaku.wordpress.com/2011/10/15/conversion-factor/) or [here](https://sites.google.com/site/diygeigercounter/gm-tubes-supported). They are all wrong.
Actually I gave up to calculate the conversion factor.

This is the way I derived my own version of a wrong conversion factor:

I'm located in Lehrte, Germany and see about 18 ticks in average with my SBM20 tube.
The German "Bundesamt für Strahlenschutz" (Federal Office for Radiation Protection - BfS) operates some monitoring stations acros Germany. Luckily there is one located in [Lehrte](https://odlinfo.bfs.de/DE/aktuelles/messstelle/032530101.html).
The average of this station is around ~0,075 Sv/h.

This leads to a conversion factor of ~ 0,0041666 (inverse= 240), which is my default conversion factor for now for my instance of the SBM-20 tube.

I recommend to configure a read/counti interval of at least a minute to get stable results.
Averaging does not makes sense for impulse counting, since the longer the count interval, the more stable are the results anyway.

![ESPurna Configuration Page](https://github.com/Trickx/espurna/blob/dev/images/devices/geiger_espurna_configuration.png)

## Result Visualisation
I'm using an InfluxDB and Grafana stack to visualise my sensor data. The screenshot below illustrates a typical result from the sensor. On the left hand side the values are dispalyed in the unit "µSv/h", while on the right hand side "counts per minute" are given. 

![Grafana dashboard for the Geiger Counter](https://github.com/Trickx/espurna/blob/dev/images/devices/geiger_grafana_dashboard.png)

The last values are mentioned on the status page of the device's webpage.
![ESPurna Status Page](https://github.com/Trickx/espurna/blob/dev/images/devices/geiger_espurna_status.png)



