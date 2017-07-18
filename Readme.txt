............:::::::::::POKEs Database for ZX Spectrum V2.0:::::::::::::...........
Number of files: 2967.
Work done by: Lady Eklipse

Version history:
2.0 (22.06.2017)
This is entirely NEW version of the database. Here is the list of major changes.
 - The POK files are scraped from Gerard's website by a web crawler written in Python;
 - POK files were then extracted into XLSX sheet for easy manual check (side by side with original content on the website);
 - POK files are imported from that XLSX sheet and extracted programmatically, while checking for correctness, thus I can give 100% guarantee that every POK file will be opened in an emulator, if .POK format implementation is correct;
 - Cheats with variables (value=256) are added (for some reason I've overlooked those when I read the specification of POK format in 2010);
	(Note: variables can be anywhere from 0 to 255 unless mentioned otherwise)
 - I'm trying to keep cheats' names as short as possible, rephrasing where necessary;
 - Each game has one and only one POK file in this database;
 - Abbreviations are used in cheats' names to help find a cheat more easily 
	(especially when full cheat description cannot be displayed by your software).
	
List of abbreviations.
 [48K] - works on 48K ZX Spectrum models.
 [128K] - works on 128K models (often this includes +2A/+3  unless mentioned otherwise.
 [+2A] - cheat made specifically for ZX Spectrum +2A
 [+3] - cheat made with +3 (disk-based) model in mind.
 [1P] - 1 player mode.
 [2P] - 2 players mode.
 [P1] - Cheat for player 1 only.
 [P2] - Cheat for player 2 only.
 [en] - English version of the game.
 [es] - Spanish version of the game.
 [L*] - Level, where * is level number(s). Level is also equal to Mission or Stage.
 [Pt*] - Part, where * is part number(s), as mentioned on TheTipShop.
 

Eventually it will become part of my ZX Pokemaster project - a tool to sort ZX Spectrum files in different ways. It will find all ZX Spectrum games on your computer by MD5 hashes, place them in one folder and sort according to your needs (by year, by publisher, by genre etc.)
Also ZX Pokemaster Frontend is planned - a replacement for SGD and GameBase Speccymania databases, which will be based on ZXDB and be able to easily launch any ZX Spectrum game in any emulator found on your computer - with minimal tweaking and tuning to get the frontend up and running.
This database will then complement ZX Pokemaster and ZX Pokemaster Frontend.
Current dev status of the project can be watched here:
https://github.com/eklipse2009/ZX-Pokemaster


1.0-1.1 - First version created by hand.

Contents.
1. About this database.
2. The structure of a .pok file.
2.1 Modifying files for your purposes.
3. How to use .pok files in emulators.
4. Using the database on a real ZX Spectrum machine.

1. About this database.
	This is a collection of cheat codes (infinite lives, bullets, level warping etc.) for more than 2900 games for ZX Spectrum microcomputer. The main source for the codes in this database is the website http://www.the-tipshop.co.uk/ which is run by Gerard Sweeney.
	The purpose of the database is to simplify entering codes in games as much as possible. The .pok format is supported by many popular Speccy emulators for all platforms and you can even enter those if you have got a DivIDE interface along with a real ZX Spectrum machine.
	The database was created entirely by hand, using Notepad++ and a few simple macroses. Most of the files have been tested just to be opened, but I can't guarantee that all the cheat codes do what they are said to do: I have just assembled them in a convenient format.
	Files in the database are created after the full names of the games, most include year and developer name, but if I don't have a game in my romset, but the poke for it exist on the-tipshop.co.uk, I just create a new file with just a game name. Since I had absolutely no feedback I used the naming scheme comfortable for me personally.
	The files are sorted by alphabet, because loading of almost 3000 files could take a while, as well as scrolling through them, especially on the real hardware. But if you really want all the files to be in one directory, I've attached two .bat executables: !sort.bat and !unsort.bat. Just launch unsort.bat and you will have all pokes in one directory. sort.bat sorts all the files by alphabet: a single subdirectory for each letter of the alphabet and one separate for numbers. You can use these little sorters for your own purposes, of course, for sorting files of any kind at all whenever you have so many of them that it's tiring to do this manually. Just don't rename the .bat files, they must begin with !, otherwise they will sort themselves before all the work is finished.
	
	2. The structure of a .pok file.
	Every line in a .pok file begins with one of these letters (capitals only): N, M, Z, Y. .pok files are actually scripts, so adding a symbol in a place it should not be most likely will result in a .pok file to be unusable - until you find the syntax error and fix it.
N stands before the text description of a code.
After description you see one of more actual addresses to be modified (in decimal format) and their values (also in decimal).
M stands before every address to be modified except of the last one.
Z stands before the last or the only address in a cheat code.
Every .pok file must end with a line consisting of Y symbol.
For example let's take a look at this little .pok file:

NInfinite Lives
Z 8 45525 0 25
Y

You see four numbers after Z which represent the following:
8 - memory bank address. Usually you don't know or don't care about it so 8 stands for "any". If there is an actual number of bank where the address is, a number from 0 to 7 stands instead of 8, but this is a very rare case, so you will see 8 in 99.9% of codes.
45525 - the address to be modified.
0 - the value which will be placed into the memory address 45525 when the cheat is activated.
25 - the initial value of the address. This will be placed into 45525 if the cheat is turned off in an emulator or in DivIDE interface. In most cases this value is unknown, so I placed 0 at the end of most pokes, so once you activate them, they may become irreversable. 
There are times when you have to modify more than one address to activate a named feature using pokes. In this case the entry would look like this:

NInfinite Lives
M 8 45523 5 0
M 8 45524 1 0
Z 8 45525 66 0
Y

In this case when you turn Infinite lives on, three addresses will be modified: 45523, 45524 and 45525. They will have such values:
45523 - 5
45524 - 1
45525 - 66
When you turn Infinite lives off, the addresses will get 0 as their values.

2.1 Modifying files for your purposes.
I tried to make the codes as much straightforward as possible, but in some complex cases it was hard to make a cheat code which would satisfy all the users.
The easiest example is a poke making you have a certain number of lives, instead of initial 3 or 5 and NOT making them infinite:
NLives = 255
Z 8 23485 255 255
Y
It is obvious that 23485 is the address where the number of lives is placed by the game. When you force this address to get a value you want (255 is a technical maximum for 1 byte of memory), it will make the game think that you have the number of lives equal to that value.
In most cases I made the initial value 255 (the maximum), so by switching the cheat off you will gain 255 lives again.
If you don't want to have 255 lives right away or if the game becomes glitchy and doesn't respond correctly to such number of lives, you can just modify the .pok file or add a few more entries, for example:
NLives = 9
Z 8 23485 9 9
NLives = 99
Z 8 23485 99 99
NLives = 100 when ON, 3 when OFF
Z 8 23485 100 3
Y
Obviously this does not apply to lives only. Sometimes there are pokes modifying the room you or a certain important game object is in, the number of different resources you have, your current score and so on. If you are confused how does this or that cheat work, you can always check out the game's page at the-tipshop.co.uk, there might be a bit more information from the author of the cheat. The format of .pok files doesn't let me sometimes add full descriptions of some cheat entries.

3. How to use .pok files in emulators.
The .pok format was invented in 1996 and is supported by a wide variety of emulators, though they were hardly used, because there were not too many of those files. Actually, there is another database like this, but it features inconvenient 8.3 filenames, less than 1000 of games represented (3 times less than in this database) and some pokes I tried from it were not working.
In Spectaculator you may just drag and drop the .pok file onto the emulator window or use File - Open... in its menu. Then you check the cheats you want to turn ON any time you want, using Tools - Cheat options in menu. You are free to do that in any moment while you are playing, just remember that in most cases the game must be loaded before the poke can be applied, otherwise it may not work. Sometimes you have to apply the poke in a specific moment, e.g. before starting the game during the game menu.
I don't think that you will have any troubles with using .pok file from this database if you are using another emulator. I know that there is a good ZX Spectrum emulator for Nintendo DS, which supports .pok files.

4. Using the database on a real ZX Spectrum machine.
Yes, it's real!
Pokes became popular way before the emulation of Speccy. Although, you had to use a special device called Multiface, which uses hardware interruptions to halt your software and let you enter pokes. Manually, of course.
But now there is a multipurpose interface for ZX Spectrum, called DivIDE. It lets you load any ZX Spectrum software from a CompactFlash card withing fractions of second. Personally I recommend buying it from Ben Versteeg, but if he has them sold out, then it won't hurt you to search eBay for it. Believe me, it's a musthave for any Spectrum user. It can brick a Soviet ZX Spectrum though, it is for official machines only: 48, 48+, 128, +2, +2A, +2B & +3.
DivIDE can use nearly a dozen of firmwares. You have to use DemFiR firmware to use .pok files the same way as you would use them with an emulator. The downside is that Demfir is CD-ROM oriented, so you have to compile an ISO image with all your games and .pok files for them. Actually, I decided to create this database just because I wanted to use pokes in Demfir without much hassle.
If you have got the DivIDE you can download Demfir here:
http://velesoft.speccy.cz/zx/divide/divide-demfir.htm
There is a readme inside, so I hope you will get to know it yourself. I just have to add that it doesn't like filenames with a symbol '+' in it and you really should place your ISO on a fresh formatted CF card or place it manually in the beginning of the CF space, otherwise Demfir can take a long time to determine where the ISO is. Also don't forget that your ISO should have a bootsector for Demfir itself, there is a sample ISO file inside of the package, but you can use ImgBurn to create yours, just click "Write files/folders to disk" - then click "Advanced", choose "Bootable disk" and add demfirboot.img as Boot image.

Thanks for using this database, it took me a lot of time to create it for you.
You may always ask me questions:
email: eklipse2009 [@] gmail.com
skype: eklipse2009
facebook: http://facebook.com/ladyeklipsegamer
vk: http://vk.com/ladyeklipse
Sincerely yours,
Lady Eklipse.
