![PrusaSlicer logo](https://github.com/prusa3d/PrusaSlicer/raw/master/resources/icons/PrusaSlicer.png)

# My Easythreed X1 config for Prusa Slicer
Although created for Easythreed X1, it should also work well on Easythreed X2, Labists X1, SONDORY PICO

*This repository and config itself is still work in progress*

## Installation
You can either download newest file by right clicking [here](https://raw.githubusercontent.com/JacekJagosz/Easythreed-X1-PrusaSlicer-config/master/EasythreedX1.ini) and choosing "save link as" or by going to [releases](https://github.com/JacekJagosz/Easythreed-X1-PrusaSlicer-config/releases) and downloading .ini from there.
Then go to PrusaSlicer, select File -> Import -> Import Config and find the `EasythreedX1.ini` file you just downloaded.

## My setup
I have an early Easythreed X1 without part cooling fan, and instead I use a PC 120MM fan standing next to the printer and connected to fan header in the electronics box.

I print in higher quality PET-G, which requies less cooling than PLA, but needs better tuning to avoid stringing.

My printer seems to suffer from less backlash than some others, so it seems frame of my frame is more rigid and I can get away with higher acceleration jerk settings.

I also oiled the rails and I printed spool holder for Prusa Mini to prevent any problems that could be caused by high friction.

## What I changed and why

![change indicators](https://user-images.githubusercontent.com/28653965/94260450-7da99400-ff30-11ea-8a84-9109ff72eb5a.png) orange padlock tells you I have changed something from PrusaSlicer's deafults, while orange back button tells you have changed something in the current profile and haven't saved it. By clicking one or the other you can see PS's defaults or what is in the profile respectively.

**Layer height** `0.3mm -> 0.2mm`- I lowered it to get more detail, as speed benefit from taller layer isn't that noticeable with such a small printer.

**Skirt** `1 -> 4, 6mm -> 2mm`- increased number of loops so the filament will start etruding corretly before it goes to the print, and increased distance from object so it doesn't cause big prints to not fit on the bed.

**Support - XY separation between between an object and its support** `50% -> 150%`- I had massive problems removing supports from the print, and this should make it easier to detach.

**Max print speed** `80mm -> 30mm`- Decreased it to 30mm/s for improving print quality. For now this is a quick fix, in the long run I should lower each speed value by hand.

**Extruder temperature** `200C -> 180C`- Set it to 180 and 190 for first layer, which gives me good bed adhesion and very little stringing. You filament might need different temperatures.

**Slow down if layer print time is below** `5s -> 10s`- Increased it so hopefully sharp tips will have more time to cool down and will look nicer. Shouldn't affect print time too much.

**Retract on layer change** `no -> yes`- Should reduce filament buildup where layer change happens, so seam should be less visible.

**Increase Y max Jerk** `0.4 -> 2 (M205 Y2)`- By deafult X1 has Y jerk set extremely low. Bringing it up to the same value as X jerk makes printing quality of curves better and speeds up the printing.

**Raise the nozzle before the printing** `Z5 -> Z40 (G1 Z40 F5000)`- By default it stayed very close to the bed making oozing filament stick to the nozzle and risking damaging the bed.

**And more minor changes**

## What you should tweak
![Mode switch](https://user-images.githubusercontent.com/28653965/94261311-ef361200-ff31-11ea-838e-6a9f6e857373.png) To see all settings mentioned below you will need to switch from **"Simple"** to **"Expert"**

Also remember when you hover over a checkbox it should show a tooltip explaining what that option does.

**Extruder temperature** is extremely important for your filament type and brand. Each roll has recommended temperatures written on it, in my experience X1 prints the best at lowest recommended one, even slightly below it. *helps: stringing and other artifacts*

**Extruder: Initial layer** setting is helpful when your prints have problem sticking to the bed. Increasing it compared to *other layers* is helpful, but don't do it too much or it will stick to the bed. *helps: printbed adhesion*

**Layer height** is the easiest thing to tweak and also one of the most influential. If need very fine detail you can lower layer height from 0.2mm to 0.15 or 0.1. This will increase printing time. *helps: fine detail*

**Brim** is printed around the object and is easily removable. Easiest way to make problematic prints stick. *helps: bed adhesion*

**Supports** are necessary when parts of the objects would have to be printed in mid-air. *helps: complicated objects, not designed for 3D printing*

**Infill density** influences print's strenght, but by not that much as you might think, as perimeters bring most rigidity. Still increase this if you want more strenght or if your top layers don't get enough support. *helps: filament used and print strenght

### Advanced tweaks

**Infill pattern** effects print strenght and printing time. Different ones are slower or faster, and have different strenghts in different axis (XYZ). So choosing the best one for specific print needs more research. X1 doesn't print gyroid too well and does best when it is just straight lines. *helps: printing time and strenght*

***TO DO***

### Start G-code tweaks
`;` character serves as a comment, whatever is in that line after this character is a comment and will be skipped by the printer

If you find *corners not sharp enough*, and want to get rid of bulging where the nozzle makes sharp turns consider adding
```
M205 X10 Y10
```
This increases max jerk from 2 to 10, meaning the printer doesn't stop on sharp corners. 
When the head slows down to turn the extruder doesn't, and keeps spitting out filament at the same pace. This causes excessive filament on sharp turns. 
You could make extruder "smarter" using linear advance, but that needs firmware changes. Instead whis makes head stop less, so the problem is less visible.
*this could lead to worse prints if your frame isn't rigid enough, but causes no problems on mine*


If you suffer from heavy *elephant foot* and first layers that are squished too much, you can add this to start G-code after `G28`:
```
G1 Z0.2 E2 F300
G92 E0 Z0
```
This is helpfull if your printer has loose Z axis belt and on first few layers the head wouldn't really move up because those moves would only take out slack from the belt. This command should stretch it and take slack out before the print. [Tip taken from Nerys' video](https://www.youtube.com/watch?v=IyCipO-2HYU)

## PS
I'm open for suggestions, please comment what you think, what I could improve and how well did it work for you.
Happy printing!
