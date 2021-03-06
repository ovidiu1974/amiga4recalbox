##Custom Amiga Emulation for Recalbox

Compatible with ADF and WHD games

Using ChiPs UAE4ARM v0.4 for RPI https://github.com/Chips-fr/uae4arm-rpi

Installation
--------------
- copy the contents of /libs into /lib
- copy /emulateurs to /recalbox/share
- give chmod 755 to every script files in /recalbox/share/emulateurs
- verify that /recalbox/share/emulateurs/amiga/uae4arm/uae4arm has 755 rights
- mkdir ram at /recalbox/share (this will be used by the script has a ram drive)
- integration with EmulationStation : modify the es_systems.cfg file in /recalbox/share_init/.emulationstation (needs to change partition / to read and write) and add the following system :
   ```xml
   
   <system>
       <fullname>amiga1200</fullname>
       <name>amiga1200</name>
       <path>/recalbox/share/roms/amiga1200</path>
       <extension>.adf .Adf .ADF .uae</extension>
       <command>./recalbox/scripts/amigalauncher.sh %ROM%</command>
       <platform>amiga1200</platform>
       <theme>amiga1200</theme>
   </system>
   ```
- copy the amigalauncher.sh script into /recalbox/scripts and chmod 777 it

Usage
-------
- /emulateurs/amigascript.sh is the main script used for launching games in every format
- /emulateurs/genUae.sh is used to generate uae files for your WHD folders
- DO NOT USE MANUALLY THE OTHERS SCRIPTS, there are for internal usage by amigascript.sh only
- emulator can be quit with either the key shown at the beginning or stroke ctrl and select 'Quit' / press Q (that's simply ctrl then Q)
- keyboard and mouse are mandatory as many amiga games need custom key strokes to launch games
- your keyboard will need to be configured as US in recalbox.conf for some games to launch if you use an azerty keyboard, quitting the emulator will be done through ctrl and a
- games are launched by /emulateurs/amiga/uae4arm, ChiPs emulator in its 0.4 version
- ctrl launches the emulator menu

ADF games
---------
Just copy them to your amiga roms folder, if the game uses several ADF, make sure that the different adfs have the same name except for the number at the end, you have to rename it if the last character isn't the number of the disk (ie if your name is ADF (Disk 1 of 2).adf rename it to ADF Disk1, spaces are usable)

WHD games in direct mode
------------------------
- unzip them, delete the .info file at the same level than the folder, copy to your roms folder or subfolder
- you'll need a custom .uae file at the same level than the folder with the same name, generate one (genUAE.sh /recalbox/share/roms/amiga will generate an uae for every folder in the amiga roms folders, you can off course use subfolders), you can also simply copy and rename one of the sample whd uae file from recalbox/share/emulateurs

KNOWN BUGS
------------
- Launching a SampleWHDGame.uae with no folder at the same level with name 'SampleWHDGame' will cause the emulator to crash and force you to reboot your recalbox
- WHD games using several slaves can have intros shown after game itself
- aspect ratio and image centering : you'll have to modify your uaes manually for the moment, for parameters force_aspectratio use true if you're in widescreen (16/9) or false in 4/3, next two parameters for centering should be put to simple
- only one joystick supported at the moment
- CD32 isos not usable for the time beeing

COMING SOON
-------------
- bugs correction
- unique key configuration for quitting game (if possible)
