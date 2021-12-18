# Sattelite Communication of North Carolina Environmental Data via ARGOS Satellite Network

## Index

* [Intent](#intent)
* [Hardware](#hardware)
  - [External Controller](#external-controller)
  - [Modules](#modules)
* [Development Approach](#development-approach)
  - [Physical Assembly](#physical-assembly)
  - ["Hello Artemis"](#hello-artemis)
  - ["Hello GPS"](#hello-gps)
  - ["Hello ARGOS"](#hello-argos)
  - ["Artemis/Nano Swap](#artemisnano-swap)
  - ["Data What?](#data-what)
  - [Let Them Eat PI](#let-them-eat-pi)
* [Resources](#resources)

## Intent

The health of North Carolina beaches is an important ecological issue and as such it is necessary to track the state of erosion of said beaches. This project serves to knock out two birds with one stone :

1. Provide data transfer capabilities for the [beach rover](https://github.com/UNCG-DAISY/BeachRover) being developed under UNCG research. 
2. Provide a future library for environmental UNCG Research projects that allows ARGOS transmission of arbitrary data.

## Hardware

For this specific research instance the idea is to have a Raspberry PI installed on the rover that then would communicate evnironmental data (such as geolocation, sensor readings, etc.) to an external embedded controller that would then send the information to a connected ARGOS shield, as shown below in Fig.1. A GPS Module would also be connected to the embedded controller for the sake of ensuring correct satellite connection given the rover's current positional data.

<p align="center"><img width="600" src="/Media/physical_diagram.jpg"></br><em>Fig.1 - Rudimentary device connection diagram.</em></p>


### External Controller

There are two controllers that will be tested throughout this research for this task:

* [SparkFun Thing Plus - Artemis](https://www.sparkfun.com/products/15574)
* [Arduino Nano Every](https://www.sparkfun.com/products/15590)

<p align="center"><img width="800" src="/Media/controllers.jpg"></br><em>Fig.2 - Both embedded controllers shown in scale relative to each other.</em></p>

The Arduino Nano is optimal given the familiarity and availability of the family of Arduino devices. In the documentation for the ARGOS transceiver shield however, only the SparkFun family of devices are listed as being compatible with the shield, so some of this research serves to find whether the transceiver shield is compatible with the Arduino Nano at all.

### Modules

#### [SparkFun GPS Breakout - Chip Antenna, SAM-M8Q](https://www.sparkfun.com/products/15210)

The GPS module is necessary so that GPS positioning info can be used to discern the closest ARGOS Stellite to connect to for the best connection. This module uses a Qwiic connection to connect to the SparkFun board. If the Nano is used instead of the Artemis, then a Qwiic connection shield needs to be used to connect the GPS module. That, or a seperate GPS module may be used.

#### [ARGOS Satellite Transceiver Shield - ARTIC R2](https://www.sparkfun.com/products/17236)

The ARGOS sattelite transceiver shield is responsible for connecting to the ARGOS satellite network.

#### [SparkFun Qwiic Shield for Arduino Nano](https://www.sparkfun.com/products/16789)

The Arduino Nano has no Qwiic connections so a shield will be necessary if the SparkFun GPS module is to be used.

#### Miscellaneous

* [SparkFun Qwiic Cable Kit](https://www.sparkfun.com/products/15081)
  - Qwiic connect cables are neccessary for connecting the GPS module to the Artemis
* [ARGOS Omnidirectional Antenna - 401MHz](https://www.sparkfun.com/products/17523)
  - The antenna is neccessary for the ARGOS transceiver to work properly. Per the device's documentation, it is possible that without the antenna, the reciever component of the transceiver shield can become damaged during operation.

### Accessories/Consumables

* [4PCS Breadboards Kit](https://www.amazon.com/dp/B07DL13RZH/ref=cm_sw_r_apan_glt_fabc_0WP1FVKA3A0C24NCWBNY?_encoding=UTF8&psc=1)
* [22 Guage Wire](https://www.amazon.com/dp/B00DRGAQ0I/ref=cm_sw_r_apan_glt_fabc_9SQN1RBHWD7QPP8KB1K8?_encoding=UTF8&psc=1)
* [Dupont Cable Pack](https://www.amazon.com/dp/B01EV70C78/ref=cm_sw_r_apan_glt_fabc_NQ8A65M8068WQ4MAK1M0)
* [Leaded Solder](https://www.amazon.com/dp/B076QF1Y85/ref=cm_sw_r_apan_glt_fabc_EG9E51PZEE3Z2TRBPY2K)

### Tools

* Variable Temperatrure Soldering Iron

## Development Approach

#### Physical Assembly

Goal: Assemble all modules together.

The Artemis Sparkfun board will be connected to the GPS breakout module via qwiic cable, using I2C protocol, while the transceiver shield uses the SPI protocol. Given that they differ, the table below shows the equivalent SPI pins labeled on both the board and shield.

|SPI Equivalent|Artemis Board|ARGOS Shield|
|---|----|----|
|MISO|MISO|CIPO|
|MOSI|MOSI|COPI|
|SCK|SCK|SCLK|
|NSS|(unknown)|CS|

Thus, the connections are as follows:

|Artemis Board|ARGOS Shield|
|---|----|
|MISO|COPI|
|MOSI|CIPO|
|SCK|SCLK|
|(unknown)|CS|

Currently I cannot determine the NSS equivalent pin on the Artemis board. This pin is necessary to let peripheral devices know that they are being selected. It is possible that the intent here is for the user to define their own NSS pins via the available digital pins. For example, one might assign digital pin 4 as the NSS pin for one device, and digital pin 5 as the NSS pin for another device.

(pending write-up)

#### "Hello Artemis"

Goal: Get artemis board connected and printing "Hello World" over Serial.

(pending write-up)

#### "Hello GPS"

Goal: Get positional data from GPS module and print the GPS coordinates over Serial.

(pending write-up)

#### "Hello ARGOS"

Goal: Using GPS data, send an initial test message "Hello Argos" to ARGOS satellite network using the satellite transceiver module.

(pending write-up)

#### Artemis/Nano Swap

Goal: Now understanding the process of using the transceiver shield properly, connect the transceiver shield to the Arduino Nano and try to relay data from the Nano.

(pending write-up)

#### Data what?

Goal: Define a C library for UNCG research needs that allows an abstract data blob to be sent from the embedded device to the ARGOS network via a single function call.

(pending write-up)

#### Let Them Eat PI

Goal: Define functionality on the embedded controller so that it listens for serial input coming in from the Raspberry PI and upon receiveing properly formatted input data, the embedded device sends the data to the ARGOS network.

(pending write-up)

## Resources

### Artemis

- [Artemis Product Page](https://www.sparkfun.com/products/15574)
- [Artemis Hookup Guide](https://learn.sparkfun.com/tutorials/hookup-guide-for-the-sparkfun-artemis-thing-plus)
- [Artemis Resource Guide](https://cdn.sparkfun.com/assets/8/7/5/3/f/Artemis_Integration_Guide.pdf)
- [Artemis Development with Arduino](https://learn.sparkfun.com/tutorials/artemis-development-with-arduino)
- [Artemis Schematic](https://cdn.sparkfun.com/assets/6/f/0/5/9/ArtemisThingPlusSchematic.pdf)

### GPS

- [SparkFun GPS Breakout Hookup Guide](https://learn.sparkfun.com/tutorials/sparkfun-gps-breakout-zoe-m8q-and-sam-m8q-hookup-guide?_ga=2.165370751.1191664431.1635884012-636933122.1635884012)
- [SAM-M8Q Datasheet](https://cdn.sparkfun.com/assets/4/e/b/9/f/SAM-M8Q_DataSheet__UBX-16012619_.pdf)
- [SAM-M8Q Hardware Integration Manual](https://cdn.sparkfun.com/assets/5/d/d/2/3/SAM-M8Q_HardwareIntegrationManual__UBX-16018358_.pdf)
- [u-blox GNSS Arduino Library](https://github.com/sparkfun/SparkFun_u-blox_GNSS_Arduino_Library)
- [SparkFun GPS Breakout Hardware Git Repo](https://github.com/sparkfun/SparkFun_u-blox_SAM-M8Q)

### ARGOS Transceiver Shield

- [ARGOS Arduino Library](https://github.com/sparkfun/SparkFun_ARGOS_ARTIC_R2_Arduino_Library)
- [ARGOS Hookup Guide](https://learn.sparkfun.com/tutorials/argos-artic-r2-satellite-transceiver-shield-hookup-guide)
- [ARGOS Communication Guide](https://learn.sparkfun.com/tutorials/argos-artic-r2-satellite-communication-guide)
- [ARGOS Transceiver Schematic](https://cdn.sparkfun.com/assets/6/9/0/f/9/SparkFun_ARGOS_ARTIC_R2_Shield.pdf)
- [ARGOS Chipset Info Sheet](https://cdn.sparkfun.com/assets/6/9/0/f/9/SparkFun_ARGOS_ARTIC_R2_Shield.pdf)
- [ARTIC R2 User Datasheet v1.1](https://cdn.sparkfun.com/assets/c/0/8/d/4/ENA303_ARTIC_R2_User_Datasheet_1v10.pdf)
- [ARGOS Hardware Git Repo](https://github.com/sparkfunX/ARGOS-ARTIC-R2-Shield)
