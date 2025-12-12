# ESP32-S3 Devboard Project
This is my custom ESP32-S3-WROOM-1U devboard project. I loosely followed Kai’s guide, but made a bunch of changes along the way to fit the ESP32-S3 and to learn more about PCB design. The board includes USB-C power, a MicroSD slot, UART, JTAG, reset/boot buttons, and an I²C connector — plus some custom Gojo artwork because why not.

## BOM (Initial Planning)
- 2.4GHz antenna (https://www.ebay.com.au/itm/227057783591?chn=ps&_ul=AU&var=526207835011&_trkparms=ispr%3D1&amdata=enc%3A1JqkfGHxeTHa0H-Di2HTCtg9&norover=1&mkevt=1&mkrid=705-173151-935305-0&mkcid=2&mkscid=101&itemid=526207835011_227057783591&targetid=2367800370202&device=c&mktype=pla&googleloc=9071804&poi=&campaignid=21776442415&mkgroupid=173963205248&rlsatarget=pla-2367800370202&abcId=10047386&merchantid=7364522&gad_source=4&gad_campaignid=21776442415&gbraid=0AAAAAD97CxTGD4XsnoSlA3ppn-XnAxOJF&gclid=Cj0KCQiArt_JBhCTARIsADQZayk99jP863GEzN5mpCXxC3UyToZESEXPnro-gabtJ7L_-CaUlK0EnMoaAhjtEALw_wcB)

- Touch Screen (https://core-electronics.com.au/2-8-tft-display-240x320-with-capacitive-touchscreen.html)
A possible later addition

- USB-C Power (https://jlcpcb.com/partdetail/Korean_HropartsElec-TYPE_C_31_M12/C165948)

- Switch (https://jlcpcb.com/partdetail/XUNPU-TS_1088AR02016/C720477)

- https://www.arrow.com/en/products/1040310811/molex?utm_source=chatgpt.com

- https://core-electronics.com.au/male-pin-header-2-54mm-1x40.html

** Note much of these aren't used, but I thought I'd leave them here in-case anybody wants to do a similar project, here are some ideas.

## Bill of Materials (BOM)

<img width="1116" height="844" alt="BOM" src="https://github.com/user-attachments/assets/dd751c98-26c9-4f63-a60b-e9fb9b030e1e" />
** This list is by no means perfect.

## Development Journal
Here’s the whole journey from start to finish.

## Researching Devboards
Before I even started, I had to figure out what a devboard actually is and what they’re used for. I knew I wanted to make my own, but I didn’t know much beyond that.
I spent a while reading, asking ChatGPT questions, and checking out examples online. I also made a plan for how my board would differ from the guide.

<img width="2920" height="1726" alt="image" src="https://github.com/user-attachments/assets/7d3946df-89fa-44e0-86c5-83d0de3f3146" />

## Power System & USB-C
I started wiring up the power section first. At one point I went down the rabbit hole of trying to use a buck switching regulator, but eventually realised I was overcomplicating things.
So I scrapped that and switched to the MCP1700 LDO instead — way simpler and fits the project better.

<img width="2528" height="1094" alt="image" src="https://github.com/user-attachments/assets/1049ae48-5de7-46b1-8e20-7bf351c3b88f" />

<img width="1926" height="756" alt="image" src="https://github.com/user-attachments/assets/107c1d28-4e4b-43c1-8c7e-5c721e50d9a1" />

## First Schematic Pass
Once I switched to the ESP32-S3 (instead of the RP2040 used in the guide), things got a lot more complicated. The datasheet helped, but there were still a ton of questions.
With help from Slack and ChatGPT, I put together the first full version of the schematic. Definitely not perfect, but it was a solid starting point.

<img width="2320" height="1592" alt="image" src="https://github.com/user-attachments/assets/08edb633-6159-4817-9544-7c1e9136aa83" />

## Finalising the Schematic
After some feedback from Reddit, I made a bunch of improvements and finally wrapped the schematic up.
At this point the board had everything I wanted: USB-C, MicroSD, UART, JTAG, reset/boot buttons, and I²C.
The hardest part was honestly just knowing whether what I did was correct, but the community feedback helped a ton.

<img width="2982" height="1628" alt="image" src="https://github.com/user-attachments/assets/d044dd8e-20c8-4707-b566-d2f93bc6b8da" />

## Footprint Assignment
Assigning footprints was next. Most were easy thanks to the guide, but a couple (like the MicroSD slot and ferrite bead) weren’t.
After some datasheet hunting, I got them sorted out without too much trouble.

<img width="2884" height="1744" alt="image" src="https://github.com/user-attachments/assets/b0725e3c-2032-4644-b8bf-773bf669fc6d" />

## Organising Components
This part was surprisingly fun. At first I felt overwhelmed by the wall of random capacitors and resistors, but after spending a bit of time on it everything started to make sense.

<img width="1258" height="1370" alt="image" src="https://github.com/user-attachments/assets/151edddc-6813-4349-972c-25ae2ba7090b" />

## Routing + Adding Artwork
Routing took forever — easily the longest part. This is only the second PCB I’ve ever routed, so I spent a lot of time learning and undoing mistakes.
Two big things I learned:
- USB D+ and D− need to be the same length
- MicroSD lines should avoid vias if possible
After a bunch of restarts and hours of routing, I finally got it into a place I’m happy with.
** Note: A good peice of advice I got from Kai's guide was to not route ground and instead do a ground fill, this saved alot of time and actally looks really nice.
I also added Gojo artwork on the front and back because the board needed some personality.
Another important part was removing alot of the labeling like 'C6' for capacitor 6, it makes the board look alot cleaner.

<img width="886" height="1246" alt="image" src="https://github.com/user-attachments/assets/0fc87601-ceff-494a-919e-f20274631937" />

<img width="1006" height="974" alt="image" src="https://github.com/user-attachments/assets/50d310f4-8281-4284-88dc-e7d26920c36a" />

<img width="856" height="1036" alt="image" src="https://github.com/user-attachments/assets/089c1a68-fa1c-467c-aef7-331c91af267d" />

## Creating the Production ZIP
Before exporting anything, I did a full DRC check and gave the whole PCB a final look over.
The Gerbers and drill files exported fine, but the BOM and footprint position files needed their headers renamed so the manufacturer will accept them:
Footprint Position Fixes
- Ref → Designator
- PosX → Mid X
- PosY → Mid Y
- Rot → Rotation
- Side → Layer

BOM Fix
- Designation → Comment

After fixing those, I zipped everything up into a production-ready file.

<img width="1792" height="852" alt="image" src="https://github.com/user-attachments/assets/e9379595-cd79-4c4a-8778-bad9d4df6e27" />
