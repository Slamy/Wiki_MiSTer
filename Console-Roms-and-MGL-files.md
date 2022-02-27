### **Under construction**


# MGL files run console games automatically

## MGL Format

Examples:

```xml
<mistergamedescription>
	<rbf>snes</rbf>
	<file delay="2" type="f" index="0" path="dummy.snes"/>
</mistergamedescription>
```


```xml
<mistergamedescription>
	<rbf>_console/gameboy</rbf>
	<file delay="1" type="f" index="1" path="dummy.gbc"/>
</mistergamedescription>
```

* `<rbf>`: the core name but add _console/ if your MGL file is not in the core folder
* delay: amount of seconds to wait before load/mount (e.g. 1:turbogfx16/neogeo/gba/gameboy/genesis 2:snes)
* type:  f - loading, s - mounting.
* index: Must be 0 for most console cores but 1 for e.g. the NeoGeo and Gameboy cores.
* path:  path to file relative to core's games folder.

All parameters must be present

If a cores pops up the OSD menu after loading the game increase the delay.