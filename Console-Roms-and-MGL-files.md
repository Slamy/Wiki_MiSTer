### Under construction


# MGL files run console games directy

## MGL Format

```xml
<mistergamedescription>
	<rbf>nes</rbf>
	<file delay="2" type="f" index="0" path="dummy.nes"/>
</mistergamedescription>
```

delay: amount of seconds to wait before load/mount.

type:  f - loading, s - mounting.

index: Must be 0 for most console cores but 1 for e.g. the NeoGeo and Gameboy cores.

path:  path to file relative to core's games folder.

	    
All parameters must be present
		
Some cores popup OSD menu on start. To prevent it to popup increase delay parameter. 
Usually 2 seconds is enough.