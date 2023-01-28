# Emulation Station Files
Emulation Station checks the file `es_systems.cfg` to know what systems are used. But if you edit this file, it no longer gets updated when the respective OS pushes an update.
Instead, you can create an extension to this config with the name `es_systems_name.cfg`. So you just need to drop `es_systems_godot.cfg` into the `emulationstation/` folder.

## Extension File Configuration
```
<?xml version="1.0" encoding="UTF-8" ?>
<systemList>
  <system>
     <name>godot</name>
     <fullname>Godot</fullname>
     <manufacturer>Godot Game Engine</manufacturer>
     <path>{PATH_TO_PCK_OR_ZIP}</path>
     <extension>.pck .zip</extension>
     <command>{PATH_TO_GAMERUNNER_SCRIPT} %ROM%</command>
     <platform>godot</platform>
     <theme>godot</theme>
   </system>
  </systemList>
```
This is the basic contents of the extension file. Most of this is self-explanatory. Replace the things in curly brackets to the proper paths.

The `extension` tag tells Emulation Station what files are considered games. Godot only exports as PCK and ZIP for now, that is if you're not embedding your files into the executable. You shouldn't need to change this.

So long as the proper settings are set up for your project, PCK and ZIP files can be created without the need for export templates. So just ignore the export template missing warnings and export those files. PCKs can be encrypted if you don't want people snooping around your code whereas ZIPs are basically just your entire project's folder compressed.

## Command to Run
```
<command>{YOUR_COMMAND_HERE}</command>
```
This is the command that is run when you click on a game in Emulation Station. You can add other commands and customize what you do when you load a game. You could technicially just hard code the Godot execution command in here instead of running the gamerunner script.

ArkOS also does some extra commands like such:
```
<command>sudo perfmax On; nice -n -19 {PATH_TO_GAMERUNNER_SCRIPT} %ROM%; sudo perfnorm</command>
```
So I'm just copying that. They may even change what commands they run in future updates, so check the `es_systems.cfg` file from time to time to see what other commands are run for other systems.

# Themes
The theme tag tells the Theme the system is `godot`. Usually they use this to denote which files to use for the logo and background art and other things depending on the way the Theme you are using was coded.

In most of the themes, the logo is an SVG file with the name system name and the background is a PNG with the system name. So just drop `godot.svg` and `godot.png` into the same folder as all the other platform logos and backgrounds. Usually the background PNG needs to be made to fit with the theme, but the logo can just be the Godot SVG provided by the Godot team on their website.

![Godot Logo SVG](/emulationstation/UnofficialOS/themes/art-book-next/_inc/images/systems/godot.svg)
