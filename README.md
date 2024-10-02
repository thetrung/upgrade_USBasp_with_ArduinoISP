# UPGRADE USBASP WITH ARDUINO UNO (AS ISP).
Upgrade the old USBasp with Arduino Uno R3 in 2024 on Ubuntu 24.04.1.

# WIRING & JUMPER CONFIG
```
___________________
Arduino | USBASP

5V      | 2 (VCC)

GND     | 10(GND)

13      | 7 (SCK)

12      | 9 (MISO)

11      | 1 (MOSI)

10      | 5 (RESET)
___________________
```
USBasp also need to have 2 jumpers :
* JP1 : to enable upgrade firmware mode
* JP2 : to use 5V instead 3V3

# ARDUINO AS ISP
* Use Arduino-IDE to upload `Examples/ArduinoISP` sketch into your Uno (As our ISP Programmer to program USBasp/ATMega8 ).
* Make sure your USB/COM port aren't denying Arduino from I/O by checking on `udev/rules.d` to see if you already have arduino rules or not.

# DOWNLOAD USBASP FIRMWARE
* Get it from [fischl.de](https://www.fischl.de/usbasp/) & extract to where you can use it.
* I will also include it [here](https://github.com/thetrung/upgrade_USBasp_with_ArduinoISP/tree/main/firmwares) for convenient usage.

# UPLOAD COMMAND
* Locate your `avrdude.conf` but for `Ubuntu/Linux`, it's usually at `/etc/avrdude.conf`.
* Now Plug your Arduino -> USB port, with `wired USBasp`.
* Execute this command :
```  
avrdude -C /etc/avrdude.conf -p m8 -c arduino -P /dev/ttyACM0 -b 19200  -U flash:w:usbasp.atmega8.2011-05-28.hex:i
```

# RESULT (IF success)
```
avrdude: AVR device initialized and ready to accept instructions
avrdude: device signature = 0x1e9307 (probably m8)
avrdude: Note: flash memory has been specified, an erase cycle will be performed.
         To disable this feature, specify the -D option.
avrdude: erasing chip
avrdude: reading input file usbasp.atmega8.2011-05-28.hex for flash
         with 4700 bytes in 1 section within [0, 0x125b]
         using 74 pages and 36 pad bytes
avrdude: writing 4700 bytes flash ...

Writing | ################################################## | 100% 6.87 s 

avrdude: 4700 bytes of flash written
avrdude: verifying flash memory against usbasp.atmega8.2011-05-28.hex

Reading | ################################################## | 100% 3.37 s 

avrdude: 4700 bytes of flash verified

avrdude done.  Thank you.
```
