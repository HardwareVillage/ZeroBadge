# ZeroBadge
Info and soft for ZeroNights 0x7E0 badge.

## Hardware
Board is exactly the same as Teensy 2.0 and uses atmega32u4 MCU.

## USB device info

Initial state - led slowly blinks
```
Bus 250 Device 006: ID 16c0:0486 16c0 Teensyduino RawHID Device
```

DFU mode after reset button pressed
```
Bus 250 Device 006: ID 03eb:2ff4 Atmel Corporation ATm32U4DFU  Serial: 1.0.0
```

## Pinout

Pinout for the board (NEEDS checking)

|PIN|   |   |   |XX1|XX2|   |   |   |PIN|
|---|---|---|---|---|---|---|---|---|---|
|   |   |   |   |VCC | PF0|ADC0|  |   | 41|
|   |   |   |   |GND | PF1|ADC1|  |   | 40|
|42 |   |   |   |AREF| PF4|TCK|ADC4| | 39|
|01 |   |   |   |PE6 | PF5|TMS|ADC5| | 38|
|08 |   |PCINT0|SS |PB0 | PF6|TDO|ADC6| | 37|
|09 |   |PCINT1|SCLK|PB1| PF7|TDI|ADC7| | 36|
|10 |PCINT2|PDI|MOSI|PB2|PC7|ICP3|CLK0|OC4A|13|
|11 |   |PDO|MISO|PB3|PC6|OC3A|OC4A||05|
|12 |RTS|OC1C|OC0A|PB7|PB6|ADC13|OC1B|OC4B| 30|
|18 |OC0B|SCL|INT0|PD0|PB5|ADC12|OC1A|OC4B| 29
|19 |   |SDA|INT1|PD1|PB4|ADC11|   |   | 28|
|20 |   |RXD1|INT2|PD2|PD7|ADC10|T0|OC4D| 27|
|21 |   |TXD1|INT3|PD3|PD6|ADC9|T1|OC4D| 26|
|22 |   |CTS|XCK1|PD5|PD4|ADC8|ICP1|   | 25|

## Flash bootloader

Device doesn't support Arduino IDE by default because of default bootloader. First of all you should check fuses and flash correct version of bootloader. Use Bus Pirate or USBASP for flashing.
We have used BusPirate 3.6 for this.

Connection scheme:

|BusPirate|ZeroNights badge|
|---|---|
|GND|GND|
|5/3.3V|VCC|
|CS|RESET (RESET button)|
|MOSI|MOSI (PB2)|
|MISO|MISO (PB3)|
|SCLK/CLK|SCK (PB1)|

Checking fuses
```
avrdude -C/Arduino.app/Contents/Java/hardware/tools/avr/etc/avrdude.conf -v -patmega32u4 -cbuspirate -P/dev/cu.usbserial-A603PKTL -e -Ulock:w:0x3F:m -Uefuse:w:0xcb:m -Uhfuse:w:0xd8:m -Ulfuse:w:0xff:m
```

After that choose "Arduino Leonardo" board in Arduino IDE settings and flash bootloader via ICSP programming.

USB VID:PID after bootloader updating
```
Bus 250 Device 006: ID 2341:8036 2341 Arduino Leonardo
```

## NRF24L01+ SPI connection

Connect NRF24L01+ to ZeroNights badge via SPI.

|ZeroNights badge|NRF24L01|
|---|---|
|GND|GND|
|VCC|VCC|
|SS(PB0)|CSN|
|MOSI(PB2)|MOSI|
|MISO(PB3)|MISO|
|SCLK(PB1)|SCK|
|CE(PD5)|CE|

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
