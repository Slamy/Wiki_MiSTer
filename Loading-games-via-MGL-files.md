### !!! **Under construction** !!!


# MGL files run games automatically

You can add your favorites games to the main menu or inside inside a folder called _Favorites, for instance.

## MGL Format

Examples:

```xml
<mistergamedescription>
	<rbf>_console/snes</rbf>
	<file delay="2" type="f" index="0" path="dummy.snes"/>
</mistergamedescription>
```


```xml
<mistergamedescription>
	<rbf>_console/gameboy</rbf>
	<file delay="1" type="f" index="1" path="dummy.gbc"/>
</mistergamedescription>
```

* `<rbf>`: path to the core and its name. If the core is outside the _console folder just its name.
* `<file delay=` amount of seconds to wait before load/mount (e.g. 1:turbografx16/neogeo/gba/gameboy/genesis/c64 2:snes).
* `type=` f: load file. s: mount
* `index=` 0 for most console cores but 1 for e.g. the NeoGeo and Gameboy cores.
* `path=` path to game file inside the core's games folder. E.g. Puzzles/Dummy.bin

All parameters must be present.

If a cores pops up the OSD menu after loading the game increase the delay.


Until a complete list of cores and their index numbers and file types is ready you can simply test different index numbers and file type

... or look at the code for each core here on Github. E.g. for the TurboGraphics core look at the file TurboGrafx16.sv

Find a section that starts with
```"parameter CONF_STR"```
and in that section look for the rom type you are loading/mounting. In this case it will be:

```xml
CODE: SELECT ALL

"S0,CUECHD,Insert CD;"
```

Notice the S0, that is the "s" type with index of 0.