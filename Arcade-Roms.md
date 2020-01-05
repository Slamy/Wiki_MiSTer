# Configuring Arcade Roms

## a.<arcade>.rom format

The original support for arcade games is in the format of rom files that are stored in the bootrom folder, or in the path in the format a.pacman.rom. These are created by running the windows bat file or linux sh file that is in the release folder of each arcade game.  You will need to provide a mame non-merged zip file that matches what the script is looking for.

## MRA Format

Because some arcade boards can change games by just putting in new roms, it made sense to move the RBF files out of sight from the menu list, and browse the MRA files instead. These MRA files specify which RBF file to use, and which mame rom zip files to create on the fly into a rom to pass to the arcade core. They will create the old a.pacman.rom style rom on the fly from mame roms, either merged or non-merged.

### Here is an example of where the files might go:
```bash
/_Arcade/<game name>.mra
/_Arcade/cores/<game rbf>.rbf
/_Arcade/mame/<mame rom>.zip
/_Arcade/hbmame/<hbmame rom>.zip
```
There are other locations for these files based on search paths.

### MRA Format
```xml
<misterromdescription>
  <name>Donkey Kong (US set 1)</name>
  <mameversion>0216</mameversion>
  <mratimestamp>201911270000</mratimestamp>
  <setname>dkong</setname>
  <year>1981</year>
  <manufacturer>Nintendo</manufacturer>
  <rbf>DonkeyKong</rbf>
<!-- rom index 1 or any other index can pass additional information to a rom.
useful to say this rom is game A or game 1.  Use it in case of multiple games for
the same RBF, ie: Dig Dug 2, Mappy -->
  <rom index="1">
    <part>0A</part>
  </rom>
<!-- rom index 0 is the standard rom. The zip will be added to the name inside the part, unless the
part has it's own zip. The md5 will be checked at the end. A file not found error is reported before an md5
error. -->
  <rom index="0" zip="dkong.zip" md5="05fb1dd1ce6a786c538275d5776b1db1" type="merged|nonmerged|split">
    <part name="c-2j.bpr"/>
    <part zip="another.zip" name="v-5e.bpr"/>
    <part name="v-5e.bpr" offset=1024 length=1024 />
    <part repeat="3328">00</part>
    <part>
80 80 80 80 80 80 7F 7F 7F 7F 7F 7F 7F 80 80 80
    </part>
  </rom>
<!-- if the first rom0 fails the md5 checksum, it will go ahead and try again if another entry is present. Otherwise it will skip the additional entries.
-->
  <rom index="0" zip="dkong.zip" md5="05fb1dd1ce6a786c538275d5776b1db1">
  </rom>
</misterromdescripton>

```

When creating a core you can pass additional data in using ioctl_index > 0. 

```
// Retrieve Title No.
always @(posedge clk_sys) begin
   if (ioctl_wr & (ioctl_index==1)) tno <= ioctl_dout[3:0];
end

```

You can use tno to hide dip switch settings and other things on a rom by rom basis. 

Be careful of reusing status bits since they are saved by rbf not mra. Don’t reuse the status bits for different arcade settings that mean different things. 

See Druaga core. 

