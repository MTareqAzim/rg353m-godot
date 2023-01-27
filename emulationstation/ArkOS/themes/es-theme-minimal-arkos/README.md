# es-theme-minimal

**Words from the creator [lilbud](https://github.com/lilbud)**

> This theme is an attempt at making EmulationStation look more like a game system.

> Modern Game Systems (PS4, Xbox One, Switch, etc.) deliver a very specific experience compared to a computer. You turn it on, see a simple boot screen, and are in the menu in seconds. You know what you are getting in to. It's made abundantly clear that this is a video game machine. The games are front and center, and everything is wrapped up in a clean, minimal, interface...

> That is what I believe sets a game system apart from the Raspberry Pi. Sure, the interface is fast, and somewhat nice looking. But it doesn't feel like a video game system. This is where the Minimal theme steps in.

**This theme was made by lilbud / https://github.com/lilbud/es-theme-minimal**

---

# Abilities

This theme is super sleak and you can set VRAM to 40MB on a Raspberry system. \
So this is the smallest theme in foorprint as far as I know. \
\
This theme is highly customizable, you can change from **three** amazing layout by altering `theme.xml`\
Version 1 gets the original theme setting back as it was released 2017, whereas version 2 is a modernized layout in game list mode. Like the original author did, I decided to keep version 2 as default. The third option is a slighlty improved v1.

You can always add new backgrounds to the theme by altering the `bg.png` file.

You can get rid off the "blurry" looking overlay by altering the overlay color inside the version assets, by removing the color code line.
```
		<image name="background" extra="true">
			<size>1 1</size>
			<pos>0 0</pos>
			<origin>0 0</origin>
			<path>./../assets/bg.png</path>
			<zIndex>0</zIndex>
			<color>10667f</color>
		</image>
```

# Changes

2019/06/05

Added background image from Minimal v1 to `_extras` \
Enabled help system, this is can be disabled/enabled into ES now

* 2019/06/06
  * Added picture for Screenshots (BATOCERA/RECALBOX), own creation \
  * Added picture for ZX81, GX68000 and recolored Virtual Boy and Odyssey2 (=VIDEOPAC) \
  * Added picture for prboom (thx norbert79 from devianart for the B/W UAC graphics)
* 2019/06/07
  * Added background image from theme version 1.0 as default (the hexagons) \
  * Reencoded some files that were named as PNG but actually contained JPG.
* 2019/06/09
  * Added CPS1, CPS2, CPS3 system icons, recolored them (thank you anthonycaccese for your ArtBook theme) \
  * Readded Odyssey2 system icon, did some recoloring
* 2019/08/28
  * Added Solarus RPG system icon, recolored it (thank you to the Solarus Team designer, https://www.solarus-games.org/)
* 2019/10/04
  * Added OpenBOR system, ripped from RetroPie with some heavy recoloring

# Preview

Get in touch with the original theme author in [this thread via RetroPie Forum](https://retropie.org.uk/forum/topic/12435/)

### `V2.xml` theme (default)

![](https://i.imgur.com/KEEBkcO.png)

### `V1.xml` theme

![](https://i.imgur.com/5UR5yTF.png)
