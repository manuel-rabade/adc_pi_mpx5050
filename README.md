ADC Pi MPX5050
==============

This an example to messure pressure (that equals water depth) using a
[Raspberry Pi](http://www.raspberrypi.org/), an [ADC
Pi](https://www.abelectronics.co.uk/products/3/Raspberry-Pi/17/ADCPIV2)
shield and a couple of
[MPX5050](http://www.freescale.com/webapp/sps/site/prod_summary.jsp?code=MPXx5050)
pressure sensors.

Wiring
------

- Wire pin 1 of the first MPX5050 to `A1` on the ADC Pi.
- Wire pin 1 of the second MPX5050 to `A2` on the ADC Pi.
- Wire pin 2 of both MPX5050 sensors to `GND` on the ADC Pi.
- Wire pin 3 of both MPX5050 sensors to `5V` on the ADC Pi.
- Wire pin `A8` on the ADC Pi to a 5V source (i used a 5V address
  selection pin on the ADC Pi).

![Prototype](rpi_adc_pi_mpx5050.jpg "Prototype")

Software
--------

Just run [bin/mpx5050](bin/mpx5050), the expected output is:

```
# ./mpx5050
channel          v               pa              m
----------------------------------------------------------------
1               0.855210        7.167939        0.730930
2               0.351403        1.636162        0.166843
vcc             5.059726
```

Calibration
-----------

Since the MPX5050 sensors have a small offset error and linear output
from Vcc to Vss that isn't exactly 5 V, the `mpx5050` script can take
that into account to give more precise output.

To calibrate your sensors follow this steps:

1. Without applying pressure run `mpx5050` and write down channel 1, 2
   and vcc volts values.

2. On the `mpx5050` script set `cal_on` to 1 and fill `vcc_cal`,
   `mpx_cal1` and `mpx_cal2` with the values from step 1.

See the _transfer function_ on the [MPX5050
datasheet](http://cache.freescale.com/files/sensors/doc/data_sheet/MPX5050.pdf)
for more information.

Resources
---------

- [ADC Pi v2 datasheet](https://www.abelectronics.co.uk/docs/stock/raspberrypi/adcpi2/Datasheet-ADCPiV2.pdf)
- [MCP3424 datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/22088b.pdf)
- [Quick2Wire Python API](https://github.com/quick2wire/quick2wire-python-api)

Author
------

Manuel Rábade <[manuel@rabade.net](mailto:manuel@rabade.net)>

Based on adcpiv2.py demo by [ABE Electronics
UK](http://www.abelectronics.co.uk).

License
-------

This work is published under a [Creative Commons Attribution 4.0
International License](http://creativecommons.org/licenses/by/4.0/).
