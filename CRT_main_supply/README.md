## CRT HV Supply Gen1

## Status
- Completed, succeeded by CRT_main_supply_2
- I would not recommend building this supply

##  Design & Architecture 
Uses the LM5180 Primary Side Regulated flyback controller. This was the easiest control to implement, given the original prototype was based on the LT8304-1 controller, which is the Analog Design variant of the same IC. The following reference design was used as my starting point for an inital prototype made a few months prior. This proved to be enough to get some life into a 3BP1, so I continued forward with that. I used the same 0399-T208 transformer, rated for 1KV output at up to 15mA, which was great for availability when I started this project. 

The use of a PSR regulator was great since it eliminated the need for any output sense such as a TL431 or large resistor ladder, and made it quite easy to slap a few of them on for the A2, Filament & Grid drive all with one converter. The supply was biased such that the ground reference could be moved around as needed, for experimentation purposes. 

Otherwise, the overall design was quite simple, and would be further revised later.

Link: https://www.analog.com/en/resources/technical-articles/1000-v-output-no-opto-isolated-flyback-converter.html

## Troubleshooting & Bring-up 
Caps & stuff

## Learnings
LM5180 has some issues

Ground reference can be set to GND -> A2 is optimal



