# Easyduino Arduino Nano

The popular Nano version of the Arduino

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Nano/ProductionFiles/Photos/Easyduino%20Nano%20Iso.jpg" width="60%">
</p>

## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Nano/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Nano/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>

## Specs

- Input Voltage: 5.5V-9V(External Source Vin) 5V (USB). Both can be used at the same time. Preferable to only power from one source
- Output Current: 250 mA (External Source) 500mA (USB)
- 3.3V Output Current: None (External Source) 100 mA (USB)
- No Polarity Protection (External Source)
- Overcurrent Protection: None (External Source) 1A (USB)
- 5V Autoselector: can take both USB and external source. A diode will avoid short circuit. 
- External input Polarity Protection: None!! 

## References 

### Atmega 328p

#### Reset 

- Atmega Hardware Design Considerations p7,p8 -> 10kR and 330R for switch. The 100nF capacitor is not used for Arduino (Produces errors with DTR)
- The 100nF capacitor on DTR (CP2102) is used for tricking the Atmega into Bootloader mode

#### Crystal

- Atmega Hardware Design Considerations p16 -> 22pf

#### AVCC

- Atmega328 Reference Manual p213 -> 10uH ferrite bead and 100nF. 
- The Analog tracks aren't critical. I won't create an analog ground for these tracks.
- I also won't add the 10 uH ferrite

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

#### CP2102

- CP2102 datasheet p15 -> 1uF and 100nF for REGIN and VBUS
- CP2102 datasheet p15 -> 100nF for VDD output, 4.7 uF is optional for higher current circuits.
- CP2102 datasheet p23 -> The VDD or 3.3 output can only provide 100mA 
- CP2102 datasheet p23 -> Logic levels go up to 3.3 V, but Atmega328p is able to understand them. Despite being 5V
- CP2102 datasheet p15 -> RST and SUSPEND resistors have not been placed. Might produce bad results due to noise

#### XC6206P

- XC6206 Torex Datasheet p1 -> 1uF ceramic capacitor on input and output. 7V Maximum operating Voltage
- XC6206 UWM Datasheet p2 -> 1uF ceramic capacitor on the input and output. 9V Maximum operating Voltage

#### 5V autoselector

- If USB is present and no external input voltage. The USB will power the ATMEGA
- If USB is present and there is external input voltage. The external voltage will power the ATMEGA
- If USB is not present and there is external input voltage. The external voltage will power the ATMEGA. The 3.3V output won't work

## KiCad Render

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Atmega328p%20Arduino%20Nano/ProductionFiles/Photos/Easyduino%20Nano%20Render%20Iso.jpg" width="60%">
</p>
