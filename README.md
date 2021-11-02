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

#### [GPS](https://www.sparkfun.com/products/15210)

The GPS module is necessary so that GPS positioning info can be used to discern the closest ARGOS Stellite to connect to for the best connection. This module uses a Qwiic connection to connect to the SparkFun board. If the Nano is used instead of the Artemis, then a qwiic connection shield needs to be used so to connect the GPS module. That, or a seperate GPS module may be used.

#### [ARGOS Transceiver Shield](https://www.sparkfun.com/products/17236)

(pending write-up)

#### [SparkFun Qwiic Shield for Arduino Nano](https://www.sparkfun.com/products/16789)

The Arduino Nano has no Qwiic connections so a shield will be necessary if the SparkFun GPS module is to be used.

#### Miscellaneous

* [SparkFun Qwiic Cable Kit](https://www.sparkfun.com/products/15081)
  - Qwiic connect cables are neccessary for connecting the GPS module to the Artemis
* [ARGOS Omnidirectional Antenna - 401MHz](https://www.sparkfun.com/products/17523)
  - The antenna is neccessary for the ARGOS transceiver to work properly. Per the device's documentation, it is possible that without the antenna, the reciever component of the transceiver shield can become damaged during operation.

## Development Approach

#### Physical Assembly

Goal: Assemble all modules together.

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

