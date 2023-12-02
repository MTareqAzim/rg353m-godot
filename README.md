# RG353M-Godot
Repository for running Godot on the RG353M

# Installation
1. Add the godot folder to your roms folder.
    - If you are using a second SD card placed in TF2, just put the godot folder in the SD card's main directory with all the other retro system folders.
    - ArkOS has two roms folders. The EASYROMS drive is the `/roms/` folder. SD/TF Slot 2 shows up as `/roms2/` folder in the system.
2. Navigate to your emulationstation folder on your device.
    - This can be done through ssh or using the in-built file manager on your handheld's OS.
    - Usually like `/etc/emuationstation/` or `/storage/.emulationstation/`
    - For ArkOS, you navigate to the `~/.emulationstation/` folder.
3. Add the appropriate files and folders from the emulationstation folder based on your OS.
    - All you really need to add is the `es_systems_godot.cfg` to this folder.
    - If you're not ssh into your system, just place the folder into your roms folder then move or copy it into the proper directory using the in-built file manager on your handheld's OS.
    - I've added a theme that adds the Godot logo to the theme.
    - If you are using ArkOS, depending on which folder, `/roms/`(SD/TF Slot 1) or `/roms2/`(SD/TF Slot 2), you use, choose the correct `es_systems.cfg`
    - More info on how the CFG file is written and the Themes are edited in the ![README](/emulationstation/README.md) in the emulationstation folder.
4. Restart Emulation Station to see the Godot system show up.
    - Note, the system won't show up if you don't have any games in the godot folder.

# Adding Games
1. Place your `.zip` or `.pck` files you exported in the `godot/v351/` folder for Godot 3.5.1 games and the `godot/v400/` folder for Godot 4.0 beta games.
2. Restart Emulation Station or scan for new games and it should detect any new files.

# Demo Game
I've added a demo game for each version of Godot available on the system. It basically helps to check if your handheld's buttons are mapped properly to the game/engine. Press start + select to quit the game. You can unzip the `.zip` files to see the code I use for this game.

# Logging
Games you play will log their output into the logs folder in their respective version folders. The logs are named as such `log_%month_%day_%hour_%minute_%second.txt`.

# The lib Folder
The lib folder is basically that. The folder to store libraries (Linux's dlls) you need for games. On UnofficialOS, you need an older version of SDL2 to get input mapping working properly. ArkOS doesn't need this cause it is already using an older version of SDL2.

# Making Games For These Handhelds
  - Basically you are building games for a Linux platform with an ARM processor and GPU with 2GB RAM and 1GB VRAM.
  - The ARM hardware means your rendering mindset should be for Android (no depth-prepasses, no face culling, simple lighting).
  - Vulkan is not avilable on the current drivers (January 2023) compiled for UnofficialOS and ArkOS. So build for OpenGL ES 3.0. (Compatability Mode in Godot v4.0)
  - Godot v4.0 is still in beta currently, so there will be unexpected bugs. Godot v3.5.1 is more stable, but may have some quirks due to the hardware it is running on.
  - Make sure you add an exit shortcut to your game. I do this by adding an AutoLoad that closes the game when start and select are pressed (Similar to quitting on RetroArch)
  - Check out the appropriate demo game `.zip` files to see some demo code.

# Exporting For These Handhelds
  - Make a Linux export. You do not need any export templates.
  - The Godot v3.5.1 compiled for this does not support webp so, just make sure your images stay as png or jpeg.
  - Check 64 bits.
  - Export just as a `.pck` or `.zip`.

# Notes
  - I mainly use UnofficialOS, so my bins are targetted for that OS. Godot v3.5.1 should work on ArkOS as well, but Godot v4.0 beta might need to be recompiled. For more info on how to compile bins for Godot, check our efornara's repository here: ![FRT Repository](https://github.com/efornara/frt). You can also download precompiled bins there as well to try out.
  - This should work for the other versions, the RG353P/V, out of the box following the same instructions.
  - If you understand how to write bash scripts, `gamerunner` in `/godot/tools/` is the script used to start the engine. You can change it to suit the handheld you have and get it running on that. You might have to recompile Godot to fit your system though. More info in the ![README](/godot/tools/README.md) in the godot/tools/ folder.
  - Ultimately, this is just for fast prototyping and playtesting. The better method of playing your finished game is using the Android frontend by exporting for Android. The hardware these handhelds are built on were made for Android devices and are more fully utilized on the Android side (Vulkan for instance). But Android's export method is not as quick as Linux's for prototyping. So this is just a compromise.
  
# Acknowledgements
  - The Godot team for their amazing game engine found here: https://github.com/godotengine/godot
  - Emanuele Fornara (efornara) for building Godot for ARM devices and SBCs found here: https://github.com/efornara/frt
  - christianhaitian for making and maintaining ArkOS found here: https://github.com/christianhaitian/arkos
  - The JustEnoughLinuxOS team for making JELOS found here: https://github.com/JustEnoughLinuxOS/distribution
  - RetroGFX for continuing JELOS support for Anbernic devices in the form of UnofficialOS found here: https://github.com/RetroGFX/UnofficialOS/tree/main
  
