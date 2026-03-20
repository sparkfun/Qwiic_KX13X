---
slug: /
---
# Introduction

The SparkFun [Triple Axis Accelerometer Breakout - KX134 (Qwiic)](https://www.sparkfun.com/products/17589) and [Triple Axis Accelerometer Breakout - KX132 (Qwiic)](https://www.sparkfun.com/products/17871) offer two high-speed additions to SparkFun's accelerometer selection featuring the KX134-1211 and KX132-1211 3-axis digital accelerometers from Kionix. The KX134 and KX132 both include a host of accelerometer features including Freefall detection, Directional Tap™ and Double-Tap™ detection, tilt orientation detection and more. The breakouts can interface with controllers using both I²C and SPI at high speeds so you can use it in either an existing Qwiic/I²C chain or SPI bus.

The KX134 is a low-power, 16-bit resolution 3-axis accelerometer capable of measuring ±8g/16g/32g/64g (user selectable) and has up to a 10kHz (max) output data rate making it ideal for high-g measurements as well as high-speed applications such as vibration sensing. The KX132 offers nearly the same data specifications at smaller acceleration (±2g/4g/8g/16g) ranges. At lower ranges the sensitivity can be set as high as 17367 counts/g (@±2g), so it's a great for applications looking for both high-speed data rates and high-sensitivity measurements at lower acceleration ranges.

**Note:** Any reference in this guide specific to either version of these breakouts will denote the version (KX132 or KX134) discussed. We'll use the terms "KX13x Breakout(s)" or "KX13x" when discussing subjects or specifications pertaining to both boards or both accelerometers.

## Required Materials

In order to follow along with this tutorial you'll need a few items along with your KX13x Breakout.

* A microcontroller or single-board computer (SBC) like a Raspberry Pi to communicate with the board.
* At least one Qwiic cable is recommended to connect your KX13x Breakout to your microcontroller/SBC:

For users who wish to communicate with the KX13x Breakout using SPI, some through-hole soldering will be necessary. You may already have a few of these items but if not the tools and products below will help with that assembly:

## Suggested Reading

If you aren't familiar with the Qwiic system, we recommend reading [here for an overview](https://www.sparkfun.com/qwiic):
