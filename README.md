# chibitron

Chibitron is a Electrostatic CRT driver design built to solve the issues I've had with many of the other designs seen elsewhere on the internet. 

## Goals of the Project
* Fully Open Source HW/FW
* Compatible with as many CRTs as possible, as small as a 1EP1 or as big as a 5XP11. (Maybe a 7JP4 eventually....)
* Single supply 12V input, with all necessary voltages generated on board.
* Onboard vector generation ability
* Ability to play Oscilloscope music with no extra equipment required.
* Built out of entirely currently stocked parts, using more common parts, when possible.

## Design of the system
Currently, the prototype boards are setup to run X/Y mode and generate HV. The anode is referenced to ground, with the cathode being at -1500V. HV is generated through a flyback, and Deflection is generated through two boost converters making a total of 250V. The main amplifiers are a class-AB with full 250V swing ability, GBWP of ~10MHz, and 100KHz @ 200V with minimal distortion. Amplifiers are closed loop feedback and setup in pairs for the pairs of deflection plates. Current Gen3 Deflection amp runs off a RP2040, altho subject to change in later revisions. 
