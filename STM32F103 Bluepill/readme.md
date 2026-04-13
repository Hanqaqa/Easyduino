# Easyduino Bluepill STM32F103

The Industry Standard in the Microcontroller World

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/STM32F103%20Bluepill/ProductionFiles/Photos/Easyduino%20STM32F1%20Iso.jpg" width="60%">
</p>

## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/STM32F103%20Bluepill/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/STM32F103%20Bluepill/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>


## Specs

- Input Voltage: 5.5V-9V(External Source through 5V pin) or 5V (USB). ONLY USE ONE VOLTAGE INPUT AT A TIME
- Maximum Output Current at 5V input : 200 mA at 3.3V output
- No Polarity Protection (External Source)
- Overcurrent Protection: None 

## References 

### STM32F103C8T6

#### Decoupling Capacitors 

- STM32F103x8 Datasheet p36 -> one 100nF decoupling capacitor per VDD pin except one 4.7uF capacitor in VDD3. I will use a 1uF capacitor in VDD3 to save costs
- STM32F103x8 Datasheet p36 -> one 10nF decoupling capacitor plus a 1uF capacitor for VDDA. I will not be needing very precise analog measurements. I will only use a 100nF capacitor

#### Crystals 

- STM32F103x8 Datasheet p54 -> PC14 PC15 use a 32.768 KHz resonator with approximately 15pF capacitors on each side. I will use 18pF
- STM32F103x8 Datasheet p52 -> PD0 PD1 use 8MHz crystal. Use 5-25 pF capacitors on each side. I will use 18pF

#### USB 

- STM32F103x8 Datasheet p 73-> No info about USB Data lines resistors. USB_D+ must be pulled up to 3.3 via 1.5k 
- Bluepill Schematic -> 20 Ohm USB Data lines terminator and a 4.7k pull up resistor
- Blackpill Schematic -> 10 Ohm USB Data lines terminator and a no pull up resistor
- I will trust the datasheet and not place resistors in USB lines and pull up to 3.3V. The Bluepill schematic is probably badly designed

#### NRST 

- STM32F103x8 Datasheet p67 -> NRST is connected to a switch and 100nF cap
- Bluepill Schematic -> 10k resistor and 100nF cap
- F031K6 Schematic -> NRST connected to a switch and 100nF cap
- Again I will trust the datasheet

#### Boot0 and Boot1 

- STM32F103x8 Hardware Development p16 -> Normally HIGH via a 10k resistor 
- Bluepill Schematic -> 100k resistors for both Boot0 and Boot1.
- Blackpill Schematic -> Boot1 tied to GND via 10k resistor. Boot0 tied to GND via 10k resistor and a push button to 3.3V
- The Blackpill and the Hardware Development guide agree. So i will place the 10k resistor and add a push button to Boot0

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

#### XC6206P332MR-3.3V

- XC6206_Torex Datasheet p6 -> Two 1 uF ceramic capacitors on Vin and Vout

## KiCad Render

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/STM32F103%20Bluepill/ProductionFiles/Photos/Easyduino%20STM32F103%20Render%20Iso.jpg" width="60%">
</p>