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
  <manufacturer>Nintendo of America</manufacturer>
  <category>Maze / Monkeys</category>
  <category>Platform</category>
  <category>Platform / Mario Bros.</category>
  <rbf>DonkeyKong</rbf>
<!-- dip switch information taken from "Pac-Man (Midway).mra"; for demonstration purposes only -->
  <switches default="FF,FF,C9">
    <dip bits="15"    name="Cabinet" ids="Cocktail,Upright"/>
    <dip bits="16,17" name="Coinage" ids="2c/1cr,1c/1cr,1c/2cr,Free Play" values="3,1,2,0"/>
    <dip bits="18,19" name="Lives" ids="1,2,3,5"/>
    <dip bits="20,21" name="Bonus Life After" ids="10000,15000,20000,None"/>
    <dip bits="22"    name="Difficulty" ids="Hard,Normal"/>
  </switches>
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
    <part name="v-5e.bpr" offset="1024" length="1024"/>
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

### Dip Switches

Dip switch support in the latest version of MRA is used instead of the status bits. The DIP config str is listed in the core, and the core is responsible for reading the up to 64bits of dip data that is sent via ioctl_index 254.

```
reg [7:0] sw[8];
always @(posedge clk_sys) if (ioctl_wr && (ioctl_index==254) && !ioctl_addr[24:3]) sw[ioctl_addr[2:0]] <= ioctl_dout;
```

Switches is the dip switch setting. The default are the default bytes. These are used so you can default the arcade into the proper factory settings. This is useful when the factory settings aren't all OFF/OFF/OFF.

```
 <switches default="FF,FF,C9">
```

The dip tag let's you put in a dip switch entry. The bit number (starting at 0) is based on the way the core was written. Often MAME source code can be used to understand the bits. The numbering will depend on the rom used, the arcade core, and how things are laid out.
 
* bits: bit number to fill out sent to the core in ioctl_data
* name: title for the OSD
* ids: title for each option in the OSD
* values: if you want the values to be different than 0,1,2,3 you can reorder them
 
```
    <dip bits="16,17" name="Coinage" ids="2c/1cr,1c/1cr,1c/2cr,Free Play" values="3,1,2,0"/>
```

