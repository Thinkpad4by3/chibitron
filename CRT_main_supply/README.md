## CRT HV Supply Gen1

## Status
- Completed, succeeded by CRT_main_supply_2
- I would not recommend building this supply

##  Design & Architecture 
Uses the LM5180 Primary Side Regulated flyback controller. This was the easiest control to implement, given the original prototype was based on the LT8304-1 controller, which is the Analog Design variant of the same IC. The following reference design was used as my starting point for an inital prototype made a few months prior. This proved to be enough to get some life into a 3BP1, so I continued forward with that. I used the same 0399-T208 transformer, rated for 1KV output at up to 15mA, which was great for availability when I started this project. 

The use of a PSR regulator was great since it eliminated the need for any output sense such as a TL431 or large resistor ladder, and made it quite easy to slap a few of them on for the A2, Filament & Grid drive all with one converter. The supply was biased such that the ground reference could be moved around as needed, for experimentation purposes. 

Focus and Brightness are controlled through resistor dividers between A2 and Cathode.

Otherwise, the overall design was quite simple, and would be further revised later. 

Link: https://www.analog.com/en/resources/technical-articles/1000-v-output-no-opto-isolated-flyback-converter.html

## Troubleshooting & Bring-up 
Main problem with bring-up on this was down to the LM5180's undiagnosed requirement for RC filtering on the primary side. Due to the large step-up ratio and leakage inductance within the transformer, ringing under load would go far above the >85V rating of the internal FET. This is less of a problem when used in a 1:1 or lower ratio, where the reflected voltage is more...reasonable. A 220p + 100 ohm resistor as suggested by the LT8304 ended up being a good solution to fix this ringing, however not before nuking about 10 of those LM5180s. Atleast they're more reasonably priced than the LT8304. 

Other major issue was that the Filament was tied to the -1500V rail instead of floating off the cathode. For the purposes of most tubes, this is not a problem. Most CRTs have a H-H-K arrangement, which means the cathode is indirectly heated, and can generally float within +/- 125V of the cathode. G1-cutoff should be no more than 100V from the cathode, so this is generally fine. However, on some tubes, they are tied H-HK where either the tube is directly heated and the cathode is the heater, or the tube has the two connections internally tied to save pin-count. Either way, given the goal of maximum compatibility, mandating a tied HK was necessary.

Supply was able to light up a 3BP1, at this point I did not have many tubes to test with and this was the only tube I felt safe to test with. It did provide a good picture, albeit a bit fuzzy. Some of this was due to unfiltered switching noise from the HV supplies. At this point, it just lit up with a dot since deflection_amp has not been brought up yet. It was however, good enough to get through deflection_amp developed, and therefore served its purpose.

## Learnings
LM5180 has some issues, regulation isn't wonderful and didn't like starting up the main filament supplies.

Ground reference can be set to GND -> A2 is optimal.

H-HK required.



