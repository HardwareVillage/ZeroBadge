# ZeroBadge
Info and soft for ZeroNights 0x7E0 badge.

## Hardware
Board is exactly the same as Teensy 2.0 and uses atmega32u4 MCU.

## USB device

Initial state - led slowly blinks
```
Bus 250 Device 006: ID 16c0:0486 16c0 Teensyduino RawHID Device
```

DFU mode after reset button pressed
```
Bus 250 Device 006: ID 03eb:2ff4 Atmel Corporation ATm32U4DFU  Serial: 1.0.0
```


## Pinout

Pinout for from front view

|   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|
|   |   |   |VCC|PF0|   |   |   |
|   |   |   |GND|PF1|   |   |   |
|   |   |   |AREF|PF4|   |   |   |
|   |   |   |PE6|PF5|   |   |   |
|   |   |   |PB0|PF6|   |   |   |
|   |   |   |PB1|PF7|   |   |   |
|   |   |   |PB2|PC7|   |   |   |
|   |   |   |PB3|PC6|   |   |   |
|   |   |   |PB7|PB6|   |   |   |
|   |   |   |PD0|PB5|   |   |   |
|   |   |   |PD1|PB4|   |   |   |
|   |   |   |PD2|PD7|   |   |   |
|   |   |   |PD3|PD6|   |   |   |
|   |   |   |PD5|PD4|   |   |   |

## Checking HlfKay

The HalfKay is shown as "Composite Device". When it is selected, the lower right panel will show its properites. You should see 0x0478 and 0x16c0 as the Product and Vendor ID.


## MAC OS X

First of all install Teensyduino from pjrc.com

Optionaly install gcc-avr:
```
$ brew tap osx-cross/avr
$ brew install avr-libc
```

Install dependencies:
```
brew install dfu-programmer avrdude
```

Flash board with blink [led example](https://www.pjrc.com/teensy/blink_both.zip)
```
sudo dfu-programmer atmega32u4 erase --debug 5
sudo dfu-programmer atmega32u4 flash --debug 5 ~/Downloads/blink_both/blink_fast_Teensy2.hex
```
