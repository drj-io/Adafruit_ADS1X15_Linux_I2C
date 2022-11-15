# Adafruit_ADS1015_Linux_I2C

Driver for TI's ADS1X15: 12 and 16-bit Differential or Single-Ended ADC with PGA and Comparator

# Fork
This repository has been forked from 
## Info
Forked and modified for use directly on linux systems. The following changes have been made: 

- Removed Arduino specific headers and methods
- Replaced i2c communication methods using `i2c-dev` hand `ioctl` kernel headers.
- Specifically avoid using deprecated libraries (like WiringPI)
- Removed Arduino specific library information
- TODO: Update examples

This library and examples should operate on most Linux systems with i2c kernel drivers enabled including the Raspberry PI.  

Thanks to Adafruit for providing most of the code shown here.

## Usage

main.cpp
```cpp
#include <iostream>
#include "Adafruit_ADS1X15.h"

Adafruit_ADS1015 ads;

int main(){
  int16_t read;
  
  ads.begin();
  ads.setDataRate(RATE_ADS1015_3300SPS);
  read = ads.readADC_SingleEnded(0);
  std::cout << read << std::endl;
}

```

build.sh
```bash
g++ -c -o main.o main.cpp
g++ -c -o ads.o Adafruit_ADS1X15.cpp 
g++ -o a.out main.o ads.o
```

## Info

This family of ADCs provide 4 single-ended or 2 differential channels.
Each has a programmable gain amplifier from 2/3 up to 16x. Available
in 12 or 16 bit versions:

* [ADS1015 12-bit ADC](https://www.adafruit.com/product/1083)
* [ADS1115 16-bit ADC](https://www.adafruit.com/product/1085)

The chip's fairly small so it comes on a breakout board with ferrites to keep the AVDD and AGND quiet. Interfacing is done via I2C. The address can be changed to one of four options (see the datasheet table 5) so you can have up to 4 ADS1x15's connected on a single 2-wire I2C bus for 16 single ended inputs.

Adafruit invests time and resources providing this open source code, please
support Adafruit and open-source hardware by purchasing products from
[Adafruit](https://www.adafruit.com)!

## License

 BSD license, all text above must be included in any redistribution.
