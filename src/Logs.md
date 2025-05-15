# Budget Distortion Pedal Build

The end goal of this project is to build a DIY Distortion pedal that emulates a DS-1 as close as possible with a user friendly build guide and well documented journey. Another Goal is to also keep the price of the pedal as low as possible (<$25 CAD).

## Outline Ideas

* Have a small basic THT pcb board on which components can be solder and swapped out for different modifications.
* Possible Future Idea: Make a smaller smd version of this which can be used in places where space is a constraint, for example- inside a guitar

# Version 1

Version 1 is a small and compact board (approx 50x48mm) with holes for THT components.

Since the goal was emulate a DS-1 pedal I researched and tried finding the original schematics. After some research I was able to find a few of its schematics over the years, but the one that really stood out to me was the [ElectroSmash Boss DS-1 Circuit Analysis](https://www.electrosmash.com/boss-ds1-analysis). This article provided a really nice and simplified schematic for the DS-1 and even discussed modifications that can be done and how they would affect the sound.

### Initial Prototype

Before designing and ordering a pcb I wanted to see if the schematics even work so I built the whole pedal on a breadboard and it did not work. All it outputted was noise, and troubleshooting this prototype was practically impossible so I tried a really simple distortion circuit with just one transistor and well it did not work too which left me confused. After researching more I found out about EMI and how it plays a huge impact on circuits with audio. Since we were working with really small signals (100mv-500mv) and then amplifying it, any electrical noise from surrounding circuits also gets amplified which creates the noise, and In my case the breadboard and all the wires were acting like an antenna for noise, and you could really hear the effects of EMI from surrounding electronic circuits, an example of this was how I could hear more noise when a turned on a lamp that was right about my breadboard, I could hear the noise emitted from the lamp when it was turned on. I basically built a giant antenna for capturing noise.

The only thing I could do now was to either use perfboard or design a PCB, and due to the complexity of the DS-1 circuit a PCB was the only the feasible solution.

### Board Design

Now using the schematics from ElectroSmash I made a kicad schematic and then assigned THT footprints for the components, now since there were a lot components I had to be smart while making a PCB. My plan was to look at the original DS1 PCB and reverse engineering from that but I figured pretty soon that was probably not the best idea as the original pcb has a lot of empty space and the components are really spaced out, and since my goal was to make it as small as possible I just decided to completely redesign the PCB from scratch.
The original DS1 uses a single layer PCB with standard THT components. I decided to go with a 2 Layer design where all the components and traces are on top and the bottom is a just a solid ground plane.
For the PCB layout I started by grouping the schematic into its main parts (Power, Input Buffer, Transistor Boost, Op-Amp, Tone/Level, Output Buffer) and then grouping the components of these groups on the PCB and then routing them one at a time.
I went through 2 iterations of PCB design before finally getting something I liked. The final design was compact PCB with a footprint of 50.4mm x 48.4mm.

### Build Process

The PCBs were ordered from jlcpcb with standard 1.6mm thickness and lead free HASL.

Assembling the PCB was long and fun process. The PCBs silkscreen has text which you can compare with the BOM to find which part goes there (Example- R19 ->1M ohm resistor).
For the first PCB I added all the components at once and then started soldering which was not a good idea as the components kept slipping out and there were way to many leads, overall it was difficult and the end result was not aesthetically pleasing but still functional.

The next step was to make an enclosure for it. For this I created a simple box in Fusion360 and added holes for the potentiometers, power supply, input/output jacks and added a press fit mechanism. There were a lot of mistakes in my box designs as i forgot to account for tolerances so fitting the component shafts through the hole was practically impossible and also the press fit had no gap so the parts just basically stuck together. I had to rip off the top part with pliers. I redesigned the top part again account for tolerances and fixing the press fit problem and as for the bottom part I just used a soldering iron to slightly expand the holes. After all this I wrapped the insides of the case with aluminium foil and duct tape and then grounded the foil basically shielding the components inside from EMI.
I added another hole on the top part using soldering iron for a red status led which indicated if the effect was activate or bypassed through the 3PDT switch.

### Testing

Initial testing of the pedal were pretty good. True bypass worked perfectly and the distortion was also surprisingly good, there was a slight hum in the background whenever I switched to Distortion which I suspect was from the cheap power supply I was using. However the results were not very consistent, the pedal worked for only the half the time and then kept on malfunctioning. It was clear that using a plastic box with foil and duct tape was not a good idea and would not yield consistent results.

### Upgrades

It was clear that the 3D printed box was not a good solution so I decided to buy a 125B pedal enclosure which set me back about $12 CAD but it was not a huge deal as the cost for each individual assembled PCB itself was approximately $12 dollars. So now the total adds up to $24 which is just under my set budget limit of $25.
For my enclosure I decided to make my own drill template. I went on Fusion360 and added all the parts and made a rough layout of where the parts would go in the enclosure. After that I just used a sharpie and a ruler and approximated where the hole would be, I then used a step drill bit to drill a hole through the pedal. After that I screwed in all the parts onto the enclosure and then soldered everything together. To prevent the PCB from touching the aluminium case and shorting everything together I designed a small box with a open top where you can just snap the pcb inside so its bottom side is covered by plastic.

### Final Testing

The final pedal enclosed in the aluminium box worked flawlessly. True bypass worked, all the knobs worked and everything was perfect. There was however one tiny problem, when the pedal is active there is a humming noise being generated due to the noisy 9v power supply adapter, using a 9v battery fixes this issue and provides a clean and hum free output.

### Problems With The Design

Overall I would say that my DIY DS-1 pedal gave outstanding results and the final product worked well but there were still some problems which made the build process a bit more inconvenient.

**Problem 1. - PCB Shape**
While its not a major problem and doesn't really affect any electrical properties of the pedal, its slightly rectangular shape and weird dimensions (55.4m by 48.4m) made it a tiny bit inconvenient to work with while designing stuff for it.

**Problem 2. - THT Holes**
Another problem I had while assembly was soldering the transistors because their THT pads were so close which made the solder connect both pads. I faced a similar Issue while soldering the potentiometer wires to the PCB, the pads were small and placed very close together.

**Problem 3. - Silkscreen Labels**
The component number on the silkscreen is actually inside the component bounding silkscreen to save space, but this also means that once you put the parts in you can no longer see the labels which may cause problems if you want to switch out a component later.

**Problem 4. - Parallel Traces**
While this did not cause any major problems in my project, It is not good practice to have power traces parallel to signal traces, this could cause EMI and add noise to the audio signal.

**Problem 5. - Hum From Power Supply**
Using power from the wall introduced a 60hz humming noise to the final signal, which you can clearly hear when you are not playing anything.

**Problem 6. - Wire Connector**
This kind of relates back to problem problem 2 but this one focuses more on connection pads for the potentiometer, power and input/output. Instead of having THT pads something like a terminal screw in connector would be more convenient.

## Embedding The Pedal Inside A Guitar

Since the pcb was so small and compact it gave me an idea. Why don't I add the pedal inside my guitar and thats exactly what I did.
I found 3D models of stratocaster parts, layed them out in fusion 360 and then started working on componenet places. Now while stratocasters do have a fair bit of space inside them, It was not enough to house the new potentiometers. So now based off my layout in fusion360 I drilled holes in the pickguard for the new potentiometers and also drilled out the stratocaster body to fit these new potentiometers. I did not own any wood drill bits, so I just decided to use my step drill bit which did the job.

Instead of a 3pdt switch I opted for a dpdt toggle switch and a latching push switch. I used the dpdt to toggle between true bypass and distortion, and used the latching push switch to turn on/off the power from the 9v battery, while using a seperate button is not required for this and you could just connect the battery ground to the jack ground I opted for one because I just like having more switches.

Initially I covered the inside of the guitar with aluminium foil and wrapped it up with duct tape, this just made the insides more thicker and made it hard to place componenets inside. Additionally the foil did not work like I expected and actually generated more noise due to maybe a ground loop issue? It was clear the foil was not working so I ended up removing it and then placing everything back again.

After this I tested it again and true bypass seemed to work fine, but for some reason the distortion was quieter and the pots did nothing.
