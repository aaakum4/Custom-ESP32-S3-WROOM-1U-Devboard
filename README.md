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
(I’ll add a BOM table/photo here later.)

## Development Journal
Here’s the whole journey from start to finish.

## Researching Devboards
Before I even started, I had to figure out what a devboard actually is and what they’re used for. I knew I wanted to make my own, but I didn’t know much beyond that.
I spent a while reading, asking ChatGPT questions, and checking out examples online. I also made a plan for how my board would differ from the guide.

## Power System & USB-C
I started wiring up the power section first. At one point I went down the rabbit hole of trying to use a buck switching regulator, but eventually realised I was overcomplicating things.
So I scrapped that and switched to the MCP1700 LDO instead — way simpler and fits the project better.

## First Schematic Pass
Once I switched to the ESP32-S3 (instead of the RP2040 used in the guide), things got a lot more complicated. The datasheet helped, but there were still a ton of questions.
With help from Slack and ChatGPT, I put together the first full version of the schematic. Definitely not perfect, but it was a solid starting point.

## Finalising the Schematic
After some feedback from Reddit, I made a bunch of improvements and finally wrapped the schematic up.
At this point the board had everything I wanted: USB-C, MicroSD, UART, JTAG, reset/boot buttons, and I²C.
The hardest part was honestly just knowing whether what I did was correct, but the community feedback helped a ton.

## Footprint Assignment
Assigning footprints was next. Most were easy thanks to the guide, but a couple (like the MicroSD slot and ferrite bead) weren’t.
After some datasheet hunting, I got them sorted out without too much trouble.

##Organising Components
This part was surprisingly fun. At first I felt overwhelmed by the wall of random capacitors and resistors, but after spending a bit of time on it everything started to make sense.

## Routing + Adding Artwork
Routing took forever — easily the longest part. This is only the second PCB I’ve ever routed, so I spent a lot of time learning and undoing mistakes.
Two big things I learned:
- USB D+ and D− need to be the same length
- MicroSD lines should avoid vias if possible
After a bunch of restarts and hours of routing, I finally got it into a place I’m happy with.
I also added Gojo artwork on the front and back because the board needed some personality.

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
