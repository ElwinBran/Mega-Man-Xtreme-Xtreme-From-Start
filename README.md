# Mega Man Xtreme Xtreme Mode from Start
This patch for Mega Man Xtreme on the Gameboy Color makes the Xtreme and hard mode available from start.
A detailed description can be found [on the RomHacking page of this hack](http://www.romhacking.net/hacks/5020/), as well as an alternative download link.
In this README you will find further information on how this patch was made and reference material.

## Tools
- [The BGB emulator](http://bgb.bircd.org/#downloads), for disassembly, hex editing, memory viewing, testing and even breakpoints.
- [LunarIPS](https://www.romhacking.net/utilities/240/), to create a patch file.
- [HxD](https://mh-nexus.de/en/hxd/), a clean hex editor used to study the save files with.

## Process
This was the second game to have the extra modes unlocked from the start. This was a stroke of luck as this one turned out to be a lot harder and the earlier acquired knowledge turned out to be usefull.

The first steps were looking at the save file and doing comparisons. 
When this proved fruitless, the attention was turned the RAM values.
These were combed for values that remained static and when changed enabled or disabled the buttons. It remained elusive.
As a desperate measure the code was traced for large parts to see if a particular value stood out. This quickly turned out to be a difficult and unhelpful method. Firstly it is very hard to trace from a certain event (the pressing of the Start button for example) and then the actual tracing itself requires thousands of instructions to be inspected by hand and eye.

Finally it was theorized that the code for enabling or disabling the extra mode must also control the corresponding graphics. Using the tile and OAM memory viewers it was possible to compare between a full and new game. The enabling code HAD to write a certain value that represents a tile of the button towards video memory. Using an access breakpoint, more tracing and regular breakpoints from there, the code was found. The offset 0xD3C0 did actually directly store the mode. Likely because it was in the upper part of the RAM it escaped inspection. Very few variables were stored in there, after all.
Afterwards, using the same replacement method of tricking the code when this offset was called as Xtreme 2, the patched was completed by walking through the game.

## References
The same references as the other Xtreme project:
- [A visual opcode map for the gameboy Z80.](http://pastraiser.com/cpu/gameboy/gameboy_opcodes.html)
- [Detailed descriptions for the opcodes, which were confusing to me without it.](https://raw.githubusercontent.com/gb-archive/salvage/master/txt-files/gb-instructions.txt)
- [The full gameboy memory map explanation.](http://gameboy.mongenel.com/dmg/asmmemmap.html)
