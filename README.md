# chibitron
Chibitron is a Electrostatic CRT driver design built to solve the issues I've had with many of the other designs seen elsewhere on the internet. 

## Goals of the Project
* Fully Open Source HW/FW
* Compatible with as many CRTs as possible, as small as a 1EP1 or as big as a 7JP4.
* Single supply 12V input, with all necessary voltages generated on board.
* Onboard vector generation ability
* Ability to play Oscilloscope music with no extra equipment required.
* Built out of entirely currently stocked parts, using more common parts, when possible.

## Design of the system
Design of the system is designed around a two-part architecture. The main board provides all the required voltages to run the tube, mainly A2/A3/Focus control. This provides the main power for the electron gun, and can be adjusted from 400 - 2000V on mono-accelerator tubes (A2), or optionally boosted with another 400-2000V on post-deflection accelerator tubes(A2+A3). Total combined acceleration maxes out at 4kV which is sufficient for a very bright, very sharp image even on the most demanding of tubes. Filament voltage is supplied through a fully isolated 6.3V source, and focus is derived off A2 through a class-A amplfier. 

The 2nd board is the deflection board, which consists of all the required components to take any sort of vector control X/Y signal and amplify it to the +/- 150V required to move the beam around. This board is compatible with almost every type of ES-CRT, including single ended deflection type tubes. All plates are driven by 300Vpk-pk 500KHz bandwidth amplifiers, where gain/offset can be used to control picture size, and neutral voltage can set for astigmatism. Amplifiers are of a class-AB variety, and are closed loop for minimal distortion, and are powered by their own local bi-polar power supplies. 

Z-axis control is currently a WIP, but is going to be fully DC coupled. 

Currently, system has been tested with over a dozen CRTs, all showing clear and bright pictures with excellent clarity and brilliance. Tubes can be swapped in and out quickly with only minor tweaks to the board trimmer potentiometers. 

## Current files:
High Voltage supplies:
- main_supply: 1st generation 1000V
- main_supply_2: 1st generation 1500V + FILTERED
- main_supply_3: 2nd generation 2kV + 2kV 
- main_supply_3_revised: 2nd generation 2kV + 2kV BUG FIXED
Deflection:
- deflection_board: 1st generation ANALOG
- deflection_board_2: 2nd generation ANALOG
- deflection_board_3: 3rd generation DIGITAL 
- deflection_board_4: 3rd generation ANALOG
- deflection_board_5: 4th generation ANALOG + COMPOSITE

Check out the README under each folder for more information on the individual. 

Deflection_board & Deflection_board_2: analog input amplifiers. Wouldn't recommend building theese
Main_supply & main_supply2: HV supplies, I would not recommend building either.

deflection_board_3: RP2040 based digital board. code not available yet, but works pretty well. needs modification. 

