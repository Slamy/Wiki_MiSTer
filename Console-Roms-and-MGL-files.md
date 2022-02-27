### **Under construction**


# MGL files run console games automatically

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
* delay: amount of seconds to wait before load/mount (e.g. 1:turbografx16/neogeo/gba/gameboy/genesis 2:snes).
* type:  f - loading, s - mounting.
* index: Must be 0 for most console cores but 1 for e.g. the NeoGeo and Gameboy cores.
* path:  path to file relative to core's games folder.

All parameters must be present

If a cores pops up the OSD menu after loading the game increase the delay.