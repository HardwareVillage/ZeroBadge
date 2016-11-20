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

Pinout differs from original Teensy 2.0:

|   |   |   |PIN|PIN|   |   |   |
|---|---|---|---|---|---|---|---|
|   |   |   |VCC|PF0|ADC0|   |   |
|   |   |   |GND|PF1|ADC1|   |   |
|   |   |   |AREF|PF4|ADC4|   |   |
|   |   |   |PE6|PF5|ADC5|   |   |
|   |   |SS|PB0|PF6|ADC6|   |   |
|   |   |SCLK|PB1|PF7|ADC7|   |   |
|   |   |MOSI|PB2|PC7|ICP3|OC4A|   |
|   |   |MISO|PB3|PC6|OC3A|OC4A|   |
|RTS|OC1C|OC0A|PB7|PB6|ADC13|OC1B|OC4B|
|OC0B|SCL|INT0|PD0|PB5|ADC12|OC1A|OC4B|
|   |SDA|INT1|PD1|PB4|ADC11|   |   |
|   |RXD1|INT2|PD2|PD7|ADC10|T0|OC4D|
|   |TXD1|INT3|PD3|PD6|ADC9|T1|OC4D|
|   |CTS|XCK1|PD5|PD4|ADC8|ICP1|   |

## Flash correct bootloader

Device doesn't support Arduino IDE by default because of default bootloader. First of all you should check fuses and flash correct version of bootloader. Use Bus Pirate or USBASP for flashing.
```
avrdude -C/Arduino.app/Contents/Java/hardware/tools/avr/etc/avrdude.conf -v -patmega32u4 -cbuspirate -P/dev/cu.usbserial-A603PKTL -e -Ulock:w:0x3F:m -Uefuse:w:0xcb:m -Uhfuse:w:0xd8:m -Ulfuse:w:0xff:m
```


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
