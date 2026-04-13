# JLCPCB Constraints for 2 layer boards

In order to make the boards as easy to manufacture as possible. I will choose the [2 layer boards constraints on JLCPCB](https://jlcpcb.com/capabilities/pcb-capabilities). Even though they were later manufactured using 4 layers for the sole reason of being easier to route.

### PCB constraints 

- Minimum clearance: 0.128mm
- Minimum track width: 0.128mm
- Minimum connection width: 0mm
- Minimum annular width: 0.1mm
- Minimum via diameter: 0.5mm
- Copper to hole clearance: 0.254mm (I mistakenly used 0.25mm! This has not been fixed as it would require retracking all the boards. The manufacturer has not complained about those 0.004mm)
- Copper to edge clearance: 0.4mm (Some boards were manufactured with 0mm clearance, but the gerbers were later fixed)
- Minimum through hole: 0.3mm
- Hole to hole clearance: 0.254mm (I mistakenly used 0.25mm)
- uVias: not used
 
 <p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Assets/JLCPCB%20Constraints/JLCPCB_2Layer_Constraints.PNG" width="60%">
</p>

### Assembly constraints

- 0402 maximum package for Economic assemble. Around $15 or 15€ cheaper than the Standard Assembly which allows 0201 parts.
- Check Confirm Parts Placement. They changed the polarity of my Tantalum capacitors on the Easyduino UNO without contacting me!! I had to resolder them later.

## Stackup constraints

I chose the [JLC04161H-7628](https://jlcpcb.com/impedance) stackup with the following characteristics:

 <p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Assets/JLCPCB%20Constraints/ImpedanceStackup.PNG" width="60%">
</p>

With Signal Layer (Layer 1) and a GND layer (L2) below. And with 0.2mm tracks and separated 0.15mm gives a differential pair impedance of approximately 90 Ohms. 

 <p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Assets/JLCPCB%20Constraints/ImpedanceStackupCalculation.PNG" width="60%">
</p>

## Fill zones constraints

 <p align="center">
    <img src="https://github.com/Hanqaqa/Easyduino/blob/master/Assets/JLCPCB%20Constraints/FillZoneClearances.PNG" width="60%">
</p>

## CPL (Component Placement List)

JLCPCB asks for the start of the position-top-pos.csv generated file by KiCad to be changed to:

```
Designator,Val,Package,Mid X ,Mid Y ,Rotation,Layer
```