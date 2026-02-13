## CRT High Voltage Gen.2 

## Status
- Completed, succeeded by main_supply_3_revised
- I would not recommend building this board

##  Design & Architecture 
The architecture was re-thought out from scratch over the previous supply. With the LM5180, they tended to work quite well, however they did have a bit of a major downside....regulation. Under extremely light load, the voltage would soar, and under very heavy load or it would tend to compensate by increasing the output voltage. Given the method of regulation is feedback sensing through the primary side, and high ratio step-up transformers are known for poor leakage inductance, the sensing ability of the converter could be quite poor at times. (See notes on Gen.1 V2 for more info on this)

Another reasons for ditching the LM5180 was due to was due to wanting variable output voltage, and the LM5180 uses a single resistor Rfb to determine this voltage. Not just did this require alot of tweaking, but provided no good method for changing the voltage with some level of signal control. Going back to a more conventional resistor divider style gave plenty of known proven options for this.

The new design uses an LM5155 and a far more conventional topology. The filament was powered through a TL431 regulated isolated flyback converter, and the A2/A3 generation was done through non-isolated ground referenced converters. A2 was referenced to ground, so the A2 supply generated the cathode potential at -400 - 2000V, and A3 was just the positive copy of A2. The main HV supplies use the NA5920-ALD, the only >1:10 ratio transformer available at the moment that is 

1) easily available
2) supports a >1000V HiPOT rating.

You might ask how I planned on getting 2000V out of a (barely) 1000V transformer. Well I'm going to use a voltage multiplier to just multiply the output by 3X. Seems like a good idea....cockroft-walton multipliers have been a proven choice of high-voltage generation for nearly a century. Well, we will get back to this in a bit. The exact topology follows the "boost mode style" found in a few LiDAR supplies and the like, which means that the charge pump caps are seperate from the filter caps, and the filter caps are larger. Otherwise, it operates the same way. Rough calculations say that 3x multiplier @ 2000V should keep the primary side at ~700V even at max voltage, should be fine for a 1500Vrms rated transformer. Primary side spiking thanks to the large 1:24 ratio would be kept at a meager 30V which would allow the choice of some more common low-voltage FETs.

Focus Amplifier was a somewhat odd design. As found on previous designs, the standard focus ladder stack was limiting for larger tubes. The highest voltage potentiometer easily available is 500V, and some larger tubes (7JP/7VP series) takes nearly 1kV on A1. The design was tested in LTspice, and validated in circuit. I did revise it for the next version, since the method of creating an isolated voltage was quite convoluted and featured poor regulation as beam current increased. It was beneficial that the focus voltage was now on the primary side, low voltage control.

## Troubleshooting & Bring-up 
The bring-up of this supply was quite troublesome. The main issue being that I did not realize the true nature of voltage-multiplied flybacks, being that they conduct on both halves of the cycle. This becomes a much bigger problem when you realize that reflected impedance is squared of the turns ratio, so the 12mA or so peak current on the secondary side becomes almost 7A on the primary side. The converter, running in current mode control, sees 7A and immediately trips, so it fails to actually regulate anything and just kinda bubbles with tiny little bursts. This is enough to get to sort of develop and open-load voltage but under load it just dies. 

To combat this, I dug up my transformer stock and found some 1:10 that would just about fit in its place. This would reduce my primary current during the forward mode of the supply to 1.2A, which was enough to sneak it past the 4A primary side current limit. Regulation still wasn't great, as evidenced by the screaming sound the supply made, but was able to supply 2W to a 2Mohm load which was excellent. Further tweaking of R/C COMP values helped. 

Among the main fault, a bunch of small issues that I found include the following:

- Wrong value resistors for the feedback chain for 400-2.1kV - A2
- Increase soft-start capacitance
- Transformer wrong: switch to Wurth 10:1 part
- MOSFET too low voltage: need >200V part
- Fix layout to not have GND overlapping underneath transformer
- Add RC filtering to A2,A3 + LC filtering to Filament
- Change TLV314 to TLV237, check >6.8V operation
- Fix the 20 ohm resistors in the VM’s to be in the correct spot
- Add soft start to filament supply 
- Capacitively couple feedback -> test this (only on A3)
- Change the RC filtering?? 2/2n + 100ohm & 1k R slope comp.
- Change connectors and remove focus amp from power supply side.
- Re-layout and silkscreen
- Add large input cap and filtering 
- UVLO resistors configured incorrectly to disable on low-voltage - 10k lower
- Fix diode on filament to be Schottky not HV rectifier
- Add 220n + 2k resistor on A2
- Add interlock if no power to op amp -> no A2 supply?
- ADD POWER TO THE AMPLIFIER FOR A2 FEEDBACK
- Wrong sense resistor values for Current sense - 0.02ohm
- Wrong value resistors for the feedback chain for 400-2.1kV - A3
- Opto feedback wired up wrong - fix

## Learnings
Hugely better understand of secondary side regulated Flyback converters and voltage multipliers

Output needs to be filtered 

Class-A style focus amp works great

Good architecture, continue developing.


