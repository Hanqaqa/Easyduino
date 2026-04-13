# Raspberry Pi Pico RP2040 v1.1 IN PROGRESS.

The new and easy to use Microcontroller from the Raspberry Foundation

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Raspberry%20Pi%20Pico%202040/ProductionFiles/Photos/Easyduino%20RP2040%20Iso.jpg" width="60%">
</p>

**The pictured version is v1.0 which had some pins mixed up in the flash memory and couldn't boot up. The project contains the v1.1 which corrects that mistake, adds a debug port and some test points. The photo will be updated when I receive and test the new board.**
**The mounting holes are not exactly in the same position as the original Pi Pico due to the size of USBC**

## Schematic

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Raspberry%20Pi%20Pico%202040/ProductionFiles/PDFs/Schematic_Page_1.png" width="60%">
</p>

KiCad's "Net classes" have been used in this schematic (The squares and romboids in the schematic). Net classes are useful for organising different nets on the circuit. For example, you can change all tracks widths for that net in just one menu.

## Gerbers

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Raspberry%20Pi%20Pico%202040/ProductionFiles/PDFs/Gerbers.png" width="60%">
</p>

## Specs

- Input Voltage: 5.5V-9V(External Source 5V) or 5V (USB). ONLY USE ONE VOLTAGE INPUT AT A TIME
- Maximum Output Current at 5V input : 200 mA at 3.3V output
- No Polarity Protection (External Source)
- Overcurrent Protection: None! 

## References 

### RP2040

- RPI Pico Schematic
- Hardware design with rp2040 p10 -> 12MHz crystal with 27 pF Capacitors 
- rp2040 datasheet p13 -> USB_DP and USB_DM need 27 Ohm Resistors
- rp2040 datasheet p13 -> Use a 12MHz Crystal
- rp2040 datasheet p13 -> TESTEN to GND
- rp2040 datasheet p155 -> USB_VDD connected to 3.3V and decoupled with a 100 nF capacitor
- rp2040 datasheet p155 -> IOVDD connected to 3.3V and decoupled with a 100 nF capacitor per pin (6pins)
- rp2040 datasheet p155 -> DVDD connected to VREG_VOUT = 1.1V and decoupled with a 100 nF capacitor per pin (2pins)
- rp2040 datasheet p156 -> ADC_AVDD connected to 3.3V and decoupled with a 100 nF capacitor. A better circuit (Pico Schematic) can be made when ADC is crucial
- rp2040 datasheet p160 -> VREG_VIN Internal 1.1V Voltage regulator Input. Connect to external 3.3V and decouple with 1uF
- rp2040 datasheet p160 -> VREG_VOUT Internal 1.1V Voltage regulator Output. Connect to 1.1V and decouple with 1uF

### USB-C

#### Differential Pair

- USB needs 90 Ohm differential traces. 
- According to JLCPCB impedance calculator, with a JLC7628 prepreg and 6mil (0.15mm) space between lines
- I have to use 9 mil tracks -> 0.2 mm
- I have to place vias because of the pinout of USB C and CP2102. Some other people have done it with no problems

### W25Q16JVUXIQ

- W25Q16JVUXIQ Datasheet p6 -> Use a 100nF and 1uF capacitor
- RPI Pico Schematic -> Use a 100nF and 2uF decoupling capacitors. A pull up resistor is not fitted
- Hardware design with rp2040 p9 -> Use a 100nF decoupling capacitor. Pull up resistor is not fitted, the flash can work without it. 
- I will only place the 100nF capacitor, since the devboard can work according to Hardware design guide. I will not place a pull up resitor


### XC6206P332MR-3.3V

- XC6206_Torex Datasheet p6 -> Two 1 uF ceramic capacitors on Vin and Vout

### Differences with Original Raspberry Pi Pico

- GPIO23 is not exposed or used. Since the voltage regulator used (XC6206...) doesn't have a Power Select mode
- GPIO29_ADC which is used for monitoring VSys (external battery) is not exposed or used in order to save costs
- In the Raspberry Pi Pico Schematic, 2uF capacitors are used for decoupling. I use 1uF decoupling capacitors as indicated in the rp2040 datasheet
- ADC_AVDD is powered only by 3.3V, no option for external Analog powering. This will be more noisy for projects where ADC is used. But in order to save space and cost. I will skip the option to power ADC_AVDD externally

## KiCad Render

<p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Raspberry%20Pi%20Pico%202040/ProductionFiles/Photos/Easyduino%20RP2040%20Render%20Iso.jpg" width="60%">
</p>
