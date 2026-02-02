## CRT High Voltage Gen.2 

## Status
- Completed, succeeded by main_supply_3_revised
- I would not recommend building this board

##  Design & Architecture 
The architecture was re-thought out from scratch over the previous supply. With the LM5180, they tended to work quite well, however they did have a bit of a major downside....regulation. Under extremely light load, the voltage would soar, and under very heavy load or it would tend to compensate by increasing the output voltage. Given the method of regulation is feedback sensing through the primary side, and high ratio step-up transformers are known for poor leakage inductance, the sensing ability of the converter could be quite poor at times. (See notes on Gen.1 V2 for more info on this)

(Mention the lack of a good method of adjustment due to the Rfb being a single resistor)

The new design uses an LM5155 and a far more conventional topology. The filament was powered through a TL431 regulated isolated flyback converter, and the A2/A3 generation was done through non-isolated ground referenced converters. A2 was referenced to ground, so the A2 supply generated the cathode potential at -400 - 2000V, and A3 was just the positive copy of A2. The main HV supplies use the NA5920-ALD, the only >1:10 ratio transformer available at the moment that is 

1) easily available
2) supports a >1000V HiPOT rating.

You might ask how I planned on getting 2000V out of a (barely) 1000V transformer. Well I'm going to use a voltage multiplier to just multiply the output by 3X. Seems like a good idea....cockroft-walton multipliers have been a proven choice of high-voltage generation for nearly a century. Well, we will get back to this in a bit. The exact topology follows the "boost mode style" found in a few LiDAR supplies and the like, which means that the charge pump caps are seperate from the filter caps, and the filter caps are larger. Otherwise, it operates the same way. Rough calculations say that 3x multiplier @ 2000V should keep the primary side at ~700V even at max voltage, should be fine for a 1500Vrms rated transformer. Primary side spiking thanks to the large 1:24 ratio would be kept at a meager 30V which would allow the choice of some more common low-voltage FETs.

Focus Amplifier was a somewhat odd design. As found on previous designs, the standard focus ladder stack was limiting for larger tubes. The highest voltage potentiometer easily available is 500V, and some larger tubes (7JP/7VP series) takes nearly 1kV on A1.




Revised from the LM5180, now uses the LM5155

designed to be SSR regulated, which was for better performance

higher voltage, more power

focus amplfiier was cursed, but it did work & iso-amp

moving the controls to the primary side for safety. 

opto feedback stuff 



NA5920-ALD transformer



## Troubleshooting & Bring-up 
lol SO MANY PROBLEMS

reversed problem with the opto-isolator.

missing soft-start

improperly UVLO spec'd resistors

- [ ] Wrong value resistors for the feedback chain for 400-2.1kV - A2
- [ ] Increase soft-start capacitance
- [ ] Transformer wrong: switch to Wurth 10:1 part
- [ ] MOSFET too low voltage: need >200V part
- [ ] Fix layout to not have GND overlapping underneath transformer
- [ ] Add RC filtering to A2,A3 + LC filtering to Filament
- [ ] Change TLV314 to TLV237, check >6.8V operation
- [ ] Fix the 20 ohm resistors in the VM’s to be in the correct spot
- [ ] Add soft start to filament supply 
- [ ] Capacitively couple feedback -> test this (only on A3)
- [ ] Change the RC filtering?? 2/2n + 100ohm & 1k R slope comp.
- [ ] Change connectors and remove focus amp from power supply side.
- [ ] Re-layout and silkscreen
- [ ] Add large input cap and filtering 
- [x] UVLO resistors configured incorrectly to disable on low-voltage - 10k lower
- [x] Fix diode on filament to be Schottky not HV rectifier
- [x] Add 220n + 2k resistor on A2
- [x] Add interlock if no power to op amp -> no A2 supply?
- [x] ADD POWER TO THE FUCKING AMPLIFIER FOR A2 FEEDBACK
- [x] Wrong sense resistor values for Current sense - 0.02ohm
- [x] Wrong value resistors for the feedback chain for 400-2.1kV - A3
- [x] Opto feedback wired up wrong - fix




## Learnings
really need to revisit how amplifiers works 

need to severely filter my output 

flybacks have sort of unregulated voltage

amp design seems good, continue with. 

8pF = slow feedback. will continue to monitor.


