# Easyduino Arduino

The Microcontroller that propelled the Maker and Hobbyst movements

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Uno/ProductionFiles/Photos/Easyduino%20UNO%20Iso.jpg" width="60%">
</p>


## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Uno/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Uno/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>

## Specs

- Input Voltage: 6.5V-15V(External Source Vin) 5V (USB). Both can be used at the same time.
- 5V Output Current: 1A (External Source) 500mA (USB)
- 3.3V Output Current: 500mA (External Source) 250 mA (USB)
- Polarity Protection (External Source) diode D2
- Overcurrent Protection: None (External Source) 1A (USB)
- 5V Autoselector: can take both USB and external source. A diode will avoid short circuit
- External Input Polarity protection: A diode will protect the circuit from a wrongly inserted battery. 

## References 

### Atmega 328p

#### Reset 

- Atmega Hardware Design Considerations p7,p8 -> 10kR, 100nF cap and 330R for switch. The 100nF is not used in Arduino (produces erors with DTR)
- The 100nF capacitor on DTR (CH340C) is used for tricking Arduino into Bootloader mode, it produces a voltage spike.

#### Crystal

- Atmega Hardware Design Considerations p16 -> 22pf

#### AVCC

- Atmega328 Reference Manual p213 -> 10uH ferrite bead and 100nF
- The Analog tracks aren't critical. I won't create an analog ground for these tracks

#### ICSP Connector

- Atmega Hardware Design Considerations p12

#### AREF

- Atmega Hardware Design Considerations p6 -> 100nF

### USB-C

#### Filtering 

- USB Hardware Design Guidelines for FTDI ICs p8 -> 10nF Cap + Ferrite Bead + 100nF Cap + 4.7uF Cap
- I disregarded such heavy filtering for the easier to implement 1uF and 100nF cap given in the CP2102 datasheet
- I added a polyfuse with Ihold=500mA and Itrip=1A.

#### Differential Pair

- USB needs 90 Ohm differential traces. 
- According to JLCPCB impedance calculator, with a JLC7628 prepreg and 6mil (0.15mm) space between lines
- I have to use 9 mil tracks -> 0.2 mm
- I will use a very short trace for D+ D- (around 2mm)
- I have to place vias because of the pinout of USB C and CP2102. Some other people have done it with no problems

#### CH340C

- Ch340 Datasheet: p10 -> 100nF between GND and V3.
- Ch340 Datasheet: p10 -> 100nF between GND and Vcc. Vcc to Vusb

#### AMS1117

- AMS1117 p4 -> 22uF tantalum capacitor on output
- I will use a 22uF to reuse the same capacitor
- I will reuse the output capacitor of AMS1117-5V to be the output capacitor of AMS1117-3.3V

#### 5V autoselector

- If USB is present and no external input voltage. The USB will power the ATMEGA
- If USB is present and there is external input voltage. The external voltage will power the ATMEGA
- If USB is not present and there is external input voltage. The external voltage will power the ATMEGA

## KiCad Render

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Uno/ProductionFiles/Photos/Easyduino%20Atmega%20Render%20Iso.jpg" width="60%">
</p>
