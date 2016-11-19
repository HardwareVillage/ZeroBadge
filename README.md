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
