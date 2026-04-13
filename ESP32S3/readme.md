# ESP32S3 TODO: PROBLEMS COMMUNICATING VIA THE NON UART USB

The new and powerful microcontroller from Espressif

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32S3/ProductionFiles/Photos/Easyduino%20ESP32S3%20Iso.jpg" width="60%">
</p>


## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32S3/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

KiCad Schematic symbols, footprints and 3D Models were obtained from their [KiCad Github repository](https://github.com/espressif/kicad-libraries)

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32S3/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>

## Specs

- Input Voltage: 5V-15V(External Source 5V) 5V (USB UART OR USB ESP32) or 3.3V. ONLY USE ONE VOLTAGE INPUT AT A TIME
- Output Current at 3.3V : 1 A (External Source) 500mA (USB)
- No Polarity Protection (External Source)
- Overcurrent Protection: None 

## References 

### ESP32 S3 WROOM 1

#### Decoupling Capacitors:

- ESP32 S3 WROOM 1 datasheet p25 -> 3.3V pin needs a 22uF and a 100nF capacitors. The 22uF doesn't have to be a tantalum capacitor. But I will use a tantalum to reuse components

#### Automatic Bootloader

- ESPS3 Sch -> Automatic Bootloader.
- ESPS3 Sch / ESP32 S3 WROOM 1 datasheet p25 -> EN pin 10k resistor and 100nF capacitor

#### Thermal vias

- ESP32 S3 WROOM 1 datasheet p27 -> GND Thermal needs vias between pads

### USB-C

#### Filtering 

- USB Hardware Design Guidelines for FTDI ICs p8 -> 10nF Cap + Ferrite Bead + 100nF Cap + 4.7uF Cap
- I disregarded such heavy filtering for the easier to implement 1uF and 100nF cap given in the CP2102 datasheet
- I added a polyfuse with Ihold=500mA and Itrip=1A.

#### Differential Pair

- USB needs 90 Ohm differential traces. 
- Using JLCPCB's JLC04161H-7628 stackup.
- Which with Signal Layer (Layer 1) and a GND layer (L2) below. And with 0.2mm tracks and separated 0.15mm gives a differential pair impedance of approximately 90 Ohms.
- For USB1 will use a very short trace for D+ D- (around 2mm)
- For USB2 (tracks that go to the internal ESP32 S3 pins and the pinout) the traces are long ~60mm for D+ D-, and have vias
- The Development board from ESP32S3 has no problem with these differential pairs with vias and is a 2 board layer
- I also have to place vias because of the pinout of USB C and CP2102. Some other people have placed vias without problems for signal integrity


#### CP2102

- CP2102 datasheet p15 -> VBUS will be tied to REGIN. 1uF and 100 nF will be added.
- CP2102 datasheet p15 -> ESD Supression Diode for all three inputs of USB  
- CP2102 datasheet p15 and p19 -> 100nF for VDD output, 4.7 uF is optional for higher current circuits.
- CP2102 datasheet p23 -> The VDD or 3.3 output can only provide 100mA. I will not use this as a voltage provider for the ciruit. I will use the AMS1117-3.3 
- CP2102 datasheet p15 -> RST and SUSPEND resistors are not present. Might produce bad results due to noise

#### AMS1117-3.3V

- AMS1117 Datasheet p1 -> 3.3V/1A Output with 5-15V Input
- AMS1117 Datasheet p4 -> 22uF tantalum capacitor on input and output.

## KiCad Render

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32S3/ProductionFiles/Photos/Easyduino%20ESP32S3%20Render%20Iso.JPG" width="60%">
</p>