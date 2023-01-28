# Explanation of the Script
```
#!/usr/bin/bash
```
The declaration to use bash to execute this script. If it's not properly executing, check if you are pointing to the proper directory with bash.

```
if [[ -d "/roms2/godot" ]]; then
  GAMEDIR="/roms2/godot"
elif [[ -d "/storage/roms/godot" ]]; then
  GAMEDIR="/storage/roms/godot"
else
  GAMEDIR="/roms/godot"
fi
```
Looking for the directory of the godot folder. The `roms2/` directory is checked before the `roms/` directory because the `roms/` directory is usually the default.

ArkOS ROMs Directories:
  - `/roms/`
  - `/roms2/`

UnofficialOS ROMs Directories:
  - `/storage/roms/`

If your system uses a different directory structure or if you place your bins in a different directory, just add for a check here. If you know you're not using any other directory system, you can specifically just set `GAMEDIR` and delete this check.

```
LOGS="$GAMEDIR/logs"
res="640x480"
GAME="${1}"
```
`LOGS` - The directory for the Godot command line output.

`res` - The resolution of your system or the resolution you want the game to run at. `widthxheight` is the scheme.

`GAME` - The game's full path. So: `$GAMEDIR/any_intermediate_folders/game.zip` or `$GAMEDIR/any_intermediate_folders/game.pck`. Uses the first argument passed into this script.

```
cd $GAMEDIR/bin/
```
Change to the directory the Godot bins are in. Not really needed, but it shortens the command to execute the game.

```
now=$(date +"%m_%d_%H_%M_%S")
driver="opengl3"
```
`now` - The current date in the format of `month_day_hour_minute_second`. Used for naming log files.

`driver` - The rendering driver used by Godot. Ideally you would want to use Vulkan, but the drivers for the RG353M don't have Vulkan configured. Maybe when panfrost is stable. But if your device has Vulkan or if your Godot version supports OpenGL 2, just set the `driver` variable to it. But maybe not here, later below when you check which version to use would be more ideal.

## Checking Which Version of Godot to Use
Based on the way roms are stored, they can be in folders. So I name my folders to indicate which version to use and check for the folder name in the `GAME` path. You can use any way of detecting which version of Godot to use, but this was my first lazy implementation.
```
# Add the new bin in the bin folder and change FRT to use a different version of godot.
if [[ $GAME == *"/v400/"* ]]; then
# Godot v4.0.0 beta
  FRT="frt_210a_400-518b9e5_arm64v8.bin"
  LOG_TXT="$LOGS/v400/log_$now.txt"
  #driver="vulkan"
elif [[ $GAME == *"/v351/"* ]]; then
# Godot v3.5.1
  FRT="frt_210a_351_arm64v8.bin"
  LOG_TXT="$LOGS/v351/log_$now.txt"
else
# Default to Godot v3.5.1
  FRT="frt_210a_351_arm64v8.bin"
  LOG_TXT="$LOGS/default/log_$now.txt"
  echo "Defaulted to $FRT" >> $LOG_TXT
fi
```
`FRT` - Sets which binary to use. The current naming scheme is `frt_frtversion_godotversion-gitcommit_platform.bin`. You don't need to follow this scheme.

`LOG_TXT` - Path to the log file. Change this to whatever scheme you want.

`driver` - Just as above, but you can set it again here to change which driver you use for which version of Godot. Currently the vulkan option is commented out because the drivers on the RG353M does not have Vulkan configured for the Linux OS.

```
echo "Booting up the game: $GAME" >> $LOG_TXT
```
Writing the `GAME` path in the log file to know which game this log file is for.

```
sdl_controllerconfig="190000004b4800000111000000010000,retrogame_joypad,platform:Linux,a:b0,b:b1,x:b3,y:b2,back:b8,start:b9,rightstick:b12,leftstick:b11,dpleft:b15,dpdown:b14,dpright:b16,dpup:b13,leftshoulder:b4,lefttrigger:b6,rightshoulder:b5,righttrigger:b7,leftx:a0,lefty:a1,rightx:a2,righty:a3,"
```
Controller config for SDL to use of the in-built controller. This is hard coded right now, but PortMaster has a way of detecting what controller is used if you want to write a general way of detecting the controller config.

## Environment Exports
```
export FRT_NO_EXIT_SHORTCUTS=true
```
FRT has a shortcut built into it to exit the program cause you can't close the game normally. However, it's hardcoded to ALT+ENTER through keyboard or button 6 on Joypad. I'd like to use that button. So instead you have to code a way to exit Godot in your game or you're just stuck in game and have to reset your device or ssh and kill the program.

```
export SDL_GAMECONTROLLERCONFIG="$sdl_controllerconfig"
```
Exporting the controller config that SDL should use. It's the environment variable that SDL will check for.

```
export LD_LIBRARY_PATH="$GAMEDIR/lib"
```
Exporting the directory for any extra libraries that are needed for your game. Note that your OS will look for libraries in here first before checking the default directory, so any libraries it finds in here are used instead of any libraries on the OS, regardless of which version is newer.

Right now an older version of SDL is needed cause the newer version on UnofficialOS doesn't properly set up the controller config. ArkOS uses an older version of SDL and that works.

## Execution Code
```
./$FRT -f -v --rendering-driver $driver --resolution $res --main-pack $GAME 2>&1 | tee -a $LOG_TXT
```
`./$FRT` - Executes the bin. This is basically how you run Godot through the command line.

`-f` - Set mode to fullscreen mode.

`-v` - Use the verbose option. Useful for logging.

`--rendering-driver $driver` - Sets the rendering driver to the driver set in the `$driver` variable.

`--resolution $res` - Sets the resolution of your game to the value set in `$res`. `widthxheight` is the scheme.

`--main-pack $GAME` - Sets the main pack to the `$GAME` you gave it. This just tells it to run your game basically.

`2>&1 | tee -a $LOG_TXT` - Pipes the output of the command terminal to the log file since you can't see the command terminal.
