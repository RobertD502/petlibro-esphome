# plwf105

An esphome firmware for [PLWF105](https://www.amazon.com/dp/B0BSFB2D37) automatic water bowl (also called the Dockstream or the PETLIBRO App Monitoring Cat Water Fountain with Wireless Pump) by Petlibro. 

## About

The default firmware, which is included in this respository requires use of the Petlibro application and must be cloud connected. Internally the firmware uses MQTT to communicate.

The esphome firmware included in this repository implements (almost) feature parity as the stock firmware without the need for the third party cloud, or any WAN connection for that matter.

### Supported Features

- Turn pump on or off
- Red LED
- Yellow LED
- Scale (used to determine water level)
- Pump error indicator

## Flashing prereqs

If you carefully open the water bowl "base" you will see a PCB holding a `ESP32-C3-WROOM-03`, a `HX7111` and a voltage regulator. There is also one more chip on the board but I am unable to identify it.

The PCB very conveniently contains 4 pins that we can use to flash our firmware. `GND`, `TX`, `RX`, and `VCC`. The PCB also has two pads on the lower right corner labled `B` and `G`. These pads can be shorted to put the ESP chip in programmer mode.

## Flashing

1) Plug the USB to serial converter into your computer and hook up to the pin holes as described below. Do NOT plugin the board yet.


`GND` -> `GND`

`TX`  -> `RX`

`RX`  -> `TX`

You don't even need to solder anything most likely. I was able to hold the pins in place with just tension.

2) Take a small wire and hold it on the `B` and `G` pads described above.
3) While still holding the wire in place, plug in the board.
4) At this point the board should be in programming mode.
5) Flash the firmware in this repo.

## Result

Here is how it looks in HomeAssistant:

![image](https://github.com/RobertD502/petlibro-esphome/assets/52541649/c34f495e-b0ef-4df2-bb2d-ef614b902c97)


## Setting Water Level

**First time setup:**

1) With the device powered on and the pump `switch` set to off, fill the water level to the `Min` marker.
2) Place the upper-assembly back on the water fountain.
3) Press the `Set Min Water Level` button to record the minimum water level.
4) Remove the upper-assembly and fill the water to the `Max` line.
5) Secure the upper-assembly to the water fountain and set the pump `switch` to on.
6) Press the `Set Max Water Level` button to record the maximum water level.

> [!Tip]
> When it is time to refill the water fountain, if you don't intend to fill the water fountain to precisely the `Max` fill line, simply press the `Set Max Water Level` button after you have added the desired amount of water.

> [!Tip]
> If you don't want to use the Max and Min buttons to set the max and min water levels, you may manually enter the desired water level values using the `Max Water level` and `Min Water level` `number` entities (use the `Internal Water Level` sensor for reference).
