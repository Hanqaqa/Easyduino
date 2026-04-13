# ESP32

The most popular WiFi Microcontroller

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32/ProductionFiles/Photos/Easyduino%20ESP32%20Iso.jpg" width="60%">
</p>

## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

KiCad Schematic symbols, footprints and 3D Models were obtained from their [KiCad Github repository](https://github.com/espressif/kicad-libraries)

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>

## Specs

- Input Voltage: 5V-15V(External Source 5V Pin) 5V (USB) or 3.3V (3.3V Pin). ONLY USE ONE VOLTAGE INPUT AT A TIME
- Output Current at 3.3V : 1 A (External Source) 500mA (USB)
- No Polarity Protection (External Source)
- Overcurrent Protection: None 

## References 

### ESP32 WROOM 32E

#### Decoupling capacitors 

- ESP32 Wroom 32 E datasheet p24 -> 3.3V pin needs one 22uF and one 100nF capacitors

#### Enable pin (EN)

- ESP32 Devkit sch -> EN pin 10k resistor and 100nF capacitor

#### Thermal Pad

- ESP32 Wroom 32 E datasheet p26 -> GND Thermal needs vias between pads. Needed vias are too small for my manufacturer. I will use bigger vias

#### Automatic Bootloader

- ESP32 Devkit sch -> Automatic Bootloader.

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
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/ESP32/ProductionFiles/Photos/Easyduino%20ESP32%20Render%20Iso.jpg" width="60%">
</p>
