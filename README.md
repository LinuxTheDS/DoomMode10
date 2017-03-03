# ![GodMode9](https://github.com/d0k3/GodMode9/blob/master/resources/logo.png)
_A full access file browser for the 3DS console_ :godmode:

GodMode9 is a full access file browser for the Nintendo 3DS console, giving you access to your SD card, to the FAT partitons inside your SysNAND and EmuNAND and to basically anything else. Among other functionality (see below), you can copy, delete, rename files and create folders.


## Warning
__This is powerful stuff__, it provides you with the means to do basically any thinkable modification to any system data available on the 3DS console. However, precautions are taken so you don't accidentially damage the data of your console. The write permissions system protects you by providing warnings and forces you to enter an unlock sequence for enabling write permissions. It is not possible to overwrite or modify any important stuff without such unlock sequences and it is not possible to accidentially unlock something.

__As always, be smart, keep backups, just to be safe__.


## Quick start guide
These short instructions apply to all users who have ARM9loaderhax and [Luma3DS](https://github.com/AuroraWright/Luma3DS) installed (Luma3DS set up with standard paths), which will be the majority of all GodMode9 users. Here's how to set it up quickly:
* Rename `GodMode9.bin`(from the release archive) to `X_GodMode9.bin`(change `X`to the button of your choice) and put it into `sd:/luma/payloads/`
* Get good versions of `aeskeydb.bin`, `seeddb.bin` and `encTitlekeys.bin` from somewhere (don't ask me!) and put these three files into `sd:/` or `sd:/files9` (optional but recommended for full functionality).
* Possibly helpful info: If you wonder how to backup your NAND, press the HOME button and enter the menu titled `More...`. You may also backup your NAND via just copying the `nand.bin` / `nand_min.bin` file in `S:/`.

You may now run GodMode9 via the X Button (or any other button you chose). See below for a list of stuff you can do with it.


## How to run this / entry points
GodMode9 can be built to run from a number of entry points, descriptions are below. Note that you need to be on or below 3DS firmware version v11.2 (v9.2 if not using SafeHax/FastHax) or have ARM9loaderhax installed for any of these to work. All entrypoint files are included in the release archive.
* __A9LH, Brahma & SafeHax__: Copy `GodMode9.bin` to somewhere on your SD card and run it via either [arm9loaderhax](https://3ds.guide/), [Brahma](https://github.com/delebile/Brahma2) or [FastHax](https://github.com/nedwill/fasthax)/[SafeHax](https://github.com/TiniVi/safehax). Brahma derivatives / loaders (such as [BrahmaLoader](https://gbatemp.net/threads/release-easily-load-payloads-in-hb-launcher-via-brahma-2-mod.402857/)) and A9LH chainloaders (such as [Luma3DS](https://github.com/AuroraWright/Luma3DS) and [BootCTR9](https://github.com/hartmannaf/BootCtr9)) will work with this as well. Build this with `make binary`.
* __Homebrew Launcher__: Copy `GodMode9.3dsx` & `GodMode9.smdh` into `/3DS/GodMode9` on your SD card. Run this via [Smealums Homebrew Launcher](http://smealum.github.io/3ds/), [Mashers Grid Launcher](https://gbatemp.net/threads/release-homebrew-launcher-with-grid-layout.397527/) or any other compatible software. Build this with `make brahma`.
* __CakeHax Browser__: Copy `GodMode9.dat` to the root of your SD card. You can then run it via http://dukesrg.github.io/?GodMode9.dat from your 3DS browser. Build this via `make cakehax`.
* __CakeHax MSET__: Copy `GodMode9.dat` to the root of your SD card and `GodMode9.nds` to anywhere on the SD card. You can then run it either via MSET and GodMode9.nds. Build this via `make cakerop`.
* __Gateway Browser Exploit__: Copy Launcher.dat to your SD card root and run this via http://go.gateway-3ds.com/ from your 3DS browser. Build this with `make gateway`. Please note: __this entrypoint is deprecated__. While it may still work at the present time with little to no problems, bugs will no more be fixed and it may be completely removed at a later time. Use CakeHax instead.

If you are a developer and you are building this, you may also just run `make release` to build all files at once. To build __SafeMode9__ (a bricksafe variant of GodMode9, with limited write permissions) instead of GodMode9, compile with `make MODE=safe`. For additional customization, you may also choose the internal font via `make FONT=6X10`, `make FONT=ACORN`, `make FONT=GB` and `make FONT=ORIG`.


## Write permissions system
GodMode9 provides a write permissions system, which will protect you from accidentually damaging you system, losing data and/or modifying important system data. To unlock a write permission, an unlock sequence must be entered. This is not possible by accident. The write permission system is based on colors and the top bar on the top screen will change color according to the current write permission level. No permission above the yellow level can be unlocked on SafeMode9.
* __Green:__ Modification to system files is not possible on this permission level. You can't edit or delete savegames and installed data. However, keep in mind that any non-system related or custom stuff on your SD card is not protected.
* __Yellow:__ You can modify system files on this permission level. Data that is unique to your console and cannot be gotten from anywhere else is still not modifyable. Any damages you introduce can be fixed in software, but loss of savegames and installed data is possible if you are not careful. __A NAND backup is highly recommended starting at this level.__
* __Orange:__ This is similar to the yellow permission level, but, in addition, allows edits to console unique data. Any damages you introduce are still fixable in software, but if you play around with this, __having a NAND backup is an absolute requirement__.
* __Red:__ The highest regular permission level. There are no limits to system file edits, and if you are not careful enough, you can brick your console and/or remove your A9LH installation. Bricks on this level may only be fixable in hardware. __If you don't have a NAND backup at this point, you seem to have a deathwish for your console__.
* __Blue:__ This permission level is reserved for edits to system memory. While, most likely, nothing bad at all will happen, consequences of edits can be unforeseen. There is even a (albeit very small) chance of bricking your console, maybe even permanently. __Tread with caution on this level__.


## Support files
For certain functionality, GodMode9 may need 'support files'. Support files can be placed into either `0:/`(the SD root folder), `0:/files9/` or `1:/rw/files9/` (all locations will work). Support files contain additional information that is required in decryption operations. A list of support files, and what they do, is found below. Please don't ask for support files - find them yourself.
* __`aeskeydb.bin`__: This should contain 0x25keyX, 0x18keyX and 0x1BkeyX to enable decryption of 7x / Secure3 / Secure4 encrypted NCCH files and 0x11key95 / 0x11key96 for FIRM decrypt support. It can be created from your existing legacy `slot0x??key?.bin`files in Decrypt9 via the 'Build Key Database' feature. As an alternative (not recommended), legacy `slot0x??key?.bin` files are also supported in GodMode9. 
* __`seeddb.bin`__: This file is required to decrypt and mount seed encrypted NCCHs and CIAs if the seed in question is not installed to your NAND. Note that your seeddb.bin must also contain the seed for the specific game you need to decrypt.
* __`otp.bin`__: This file is console-unique and is required - on entrypoints other than A9LH - for decryption of the 'secret' sector 0x96 on N3DS (and O3DS with a9lh installed). Refer to [this guide](https://github.com/Plailect/Guide/wiki) for instructions on how to get your own `otp.bin` file.
* __`sector0x96.bin`__ / __`secret_sector.bin`__ : A copy of the decrypted, untouched (non-a9lh) secret sector. This is required for decryption of the encrypted ARM9 section of N3DS FIRMs. It is not required for anything else. As an alternative you can also provide the required keys inside your aeskeydb.bin.
* __`encTitleKeys.bin`__ / __`decTitleKeys.bin`__: These files are optional and provide titlekeys, which are required to create updatable CIAs from NCCH / NCSD files. CIAs created without these files will still work, but won't be updatable from eShop.


## What you can do with GodMode9
With the possibilites GodMode9 provides, not everything may be obvious at first glance. In short, __GodMode9 includes improved versions of basically everything that Decrypt9 has, and more__. Any kind of dumps and injections are handled via standard copy operations and more specific operations are found inside the A button menu. The A button menu also works for batch operations when multiple files are selected. For your convenience a (incomplete!) list of what GodMode9 can do follows below.
* __Manage files on all your data storages__: You wouldn't have expected this, right? Included are all standard file operations such as copy, delete, rename files and create folders. Use the L button to mark multiple files and apply file operations to multiple files at once.
* __Actually use that extra NAND space__: You can setup a __bonus drive__ via the home menu, which will be available via drive letter `8:`.
* __Make screenshots__: Press R+L anywhere. Screenshots are in BMP format.
* __Use multiple panes__: Press R+left|right. This enables you to stay in one location in the first pane and open another in the second pane.
* __Search drives and folders__: Just press R+A on the drive / folder you want to search.
* __Format your SD card / setup a RedNAND__: Press the HOME button, select `SD format menu`. This also allows to setup a RedNAND on your SD card. You will get a warning prompt and an unlock sequence before any operation starts.
* __Handle multiple EmuNANDs / RedNAND__: Press the HOME button, select `Switch EmuNAND` to switch between EmuNANDs / RedNANDs.
* __Run it without an SD card / unmount the SD card__: If no SD card is found, you will be offered to run without the SD card. You can also unmount and remount your SD card from the file system root at any point.
* __Direct access to SD installed contents__: Just take a look inside the `A:`/`B:` drives. On-the-fly-crypto is taken care for, you can access this the same as any other content.
* __Build CIAs from NCCH / NCSD (.3DS) / TMD (installed contents)__: Press A on the file you want converted, the option will be shown. Installed contents are found (among others) in `1:/titles/`(SysNAND) and `A:/titles/`(SD installed). Where applicable, you will also be able to generate legit CIAs. Note: this works also from a file search.
* __Decrypt, encrypt and verify NCCH / NCSD / CIA / BOSS / FIRM images__: Options are found inside the A button menu. You will be able to decrypt/encrypt to the standard output directory or (where applicable) in place.
* __Decrypt content downloaded from CDN / NUS__: Press A on the file you want decrypted. For this to work, you need at least a TMD file (`encTitlekeys.bin` / `decTitlekeys.bin` also required, see _Support files_ below) or a CETK file. Either keep the names provided by CDN / NUS, or rename the downloaded content to `(anything).nus` or `(anything).cdn` and the CETK to `(anything).cetk`.
* __Batch mode for the above operations__: Just select multiple files of the same type via the L button, then press the A button on one of the selected files.
* __Access any file inside NCCH / NCSD / CIA / FIRM images__: Just mount the file via the A button menu and browse to the file you want. For CIAs and CDN / NUS content, prior decryption may be advisable for full access.
* __Mount ticket.db files and dump tickets__: Mount the file via the A button menu. Tickets are sorted into `eshop` (stuff from eshop, probably legit), `system` (system tickets, probably legit) and `unknown`(everything else, never legit) categories.
* __Inject any NCCH CXI file into Health & Safety__: The option is found inside the A button menu for any NCCH CXI file. NCCH CXIs are found, f.e. inside of CIAs. Keep in mind there is a (system internal) size restriction on H&S injectable apps.
* __Inject and dump GBA VC saves__: Look for a file called `gbavc.sav` inside the `S:` drive. Keep in mind that you need to start the specific GBA game on your console before dumping / injecting the save.
* __Dump 3DS / NDS / DSi type retail game cartridges__: Insert the cartridge and take a look inside the `C:` drive. You may also dump private headers from 3DS game cartridges.
* __Generate XORpads from `ncchinfo.bin` files__: Start this via the appropriate entry inside the A button menu.
* __Generate XORpads for any NAND partition__: Take a look inside the `X:` drive. You can use these XORpads for decryption of encrypted NAND images on PC. Additional tools such as [3dsFAT16Tool](https://github.com/d0k3/3DSFAT16tool/releases) are required on PC.
* __Check and fix CMACs (for any file that has them)__: The option will turn up in the A button menu if it is available for a given file (f.e. system savegames, `ticket.db`, etc...). This can also be done for multiple files at once if they are marked.
* __Directly mount and access NAND dumps or standard FAT images__: Just press the A button on these files to get the option. You can only mount NAND dumps from the same console.
* __Restore NAND dumps while keeping your A9LH / sighax installation intact__: Select `Restore SysNAND (safe)` from inside the A button menu.
* __Restore / dump NAND partitions or even full NANDs__: Just take a look into the `S:` (or `E:`/ `I:`) drive. This is done the same as any other file operation.
* __Transfer CTRNAND images between systems__: Transfer the file located at `S:/ctrnand_full.bin` (or `E:`/ `I:`). On the receiving system, press A, select `CTRNAND Options...`, then `Adapt to SysNAND`. After the modification finishes, you may copy `ctrnand_full.bin` to `S:` / `E` / `I` t to transfer it into your NAND.
* __Embed an essential backup right into a NAND dump__: This is available in the A button menu for NAND dumps. Essential backups contain NAND header, `movable.sed`, `LocalFriendCodeSeed_B` and `SecureInfo_A`.
* __Compare and verify files__: Press the A button on the first file, select `Calculate SHA-256`. Do the same for the second file. If the two files are identical, you will get a message about them being identical. On the SDCARD drive (`0:`) you can also write a SHA file, so you can check for any modifications at a later point.
* __Hexview and hexedit any file__: Press the A button on a file and select `Show in Hexeditor`. A button again enables edit mode, hold the A button and press arrow buttons to edit bytes. You will get an additional confirmation prompt to take over changes. Take note that for certain files, write permissions can't be enabled.
* __Inject a file to another file__: Put exactly one file (the file to be injected from) into the clipboard (via the Y button). Press A on the file to be injected to. There will be an option to inject the first file into it.


## License
You may use this under the terms of the GNU General Public License GPL v2 or under the terms of any later revisions of the GPL. Refer to the provided `LICENSE.txt` file for further information.


## Credits
This tool would not have been possible without the help of numerous people. Thanks go to...
* **Archshift**, for providing the base project infrastructure
* **Normmatt**, for sdmmc.c / sdmmc.h and gamecart code
* **Cha(N)**, **Kane49**, and all other FatFS contributors for FatFS
* **SciresM** for helping me figure out RomFS 
* **b1l1s** for helping me figure out A9LH compatibility
* **Gelex** and **AuroraWright** for helping me figure out various things
* **dark_samus** for the new 6x10 font and help on various things
* **Wolfvak** for the ARM9 binary launcher and other improvements
* **WinterMute** and **YodaDaCoda** for help testing DSi cart dumping
* **Al3x_10m**, **Supster131**, **imanoob**, **Kasher_CS** and all other fearless testers
* **Shadowhand** for being awesome and [hosting my nightlies](https://d0k3.secretalgorithm.com/)
* **Amazingmax fonts** for the Amazdoom font
* The fine folks on **freenode #Cakey**
* All **[3dbrew.org](https://www.3dbrew.org/wiki/Main_Page) editors**
* Everyone I possibly forgot, if you think you deserve to be mentioned, just contact me!