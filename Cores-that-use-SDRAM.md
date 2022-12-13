Here is a thorough list of Cores that may take advantage of or require an SDRAM Add-On Board in order to function. If a Core is not listed, it does not require nor take advantage of the SDRAM Add-On Board†:
## Service Cores
| Name | SDRAM Speed (MHz) | SDRAM Required? | Comments |
|:---:|:---:|:---:|:---:|
| [Boot Menu](https://github.com/MiSTer-devel/Menu_MiSTer) | 100 | No | Does not require the SDRAM board, but will use it if found<br>It will clear the entire SDRAM and DDR memory while running |
| [SDRAM Board Test](https://github.com/MiSTer-devel/MemTest_MiSTer) | 70-167 | Yes | |

## Computers - Classic
| Name | SDRAM Speed (MHz) | SDRAM Required? | Comments |
|:---:|:---:|:---:|:---:|
| [Acorn Archimedes](https://github.com/MiSTer-devel/Archie_MiSTer) | 126 | Yes | |
| [Acorn Electron](https://github.com/MiSTer-devel/AcornElectron_MiSTer) | 96 | Yes | |
| [Alice MC10](https://github.com/MiSTer-devel/AliceMC10_MiSTer) | 50 | Yes | |
| [Amstrad CPC 6128](https://github.com/MiSTer-devel/Amstrad_MiSTer) | 64 | Yes | |
| [Amstrad PCW](https://github.com/MiSTer-devel/Amstrad-PCW_MiSTer) | 64 | Yes | |
| [Apple Macintosh Plus](https://github.com/MiSTer-devel/MacPlus_MiSTer) | 65 | Yes | |
| [Atari 800XL](https://github.com/MiSTer-devel/Atari800_MiSTer) | 57 | No | Optional<br>Required for memory config over 320KB or Cartridge use |
| [Atari ST/STe](https://github.com/MiSTer-devel/AtariST_MiSTer) | 96 | Yes | |
| [BK0011M](https://github.com/MiSTer-devel/BK0011M_MiSTer) | 96 | Yes | |
| [Coleco Adam](https://github.com/MiSTer-devel/ColecoAdam_MiSTer) | 43 | Yes | |
| [Color Computer 2](https://github.com/MiSTer-devel/CoCo2_MiSTer) | 43 | Yes | |
| [Color Computer 3](https://github.com/MiSTer-devel/CoCo3_MiSTer) | 115 | Yes | |
| [Commodore 64](https://github.com/MiSTer-devel/C64_MiSTer) | 63 | Yes | |
| [Commodore Amiga](https://github.com/MiSTer-devel/Minimig-AGA_MiSTer) | 57 | Yes | |
| [MSX](https://github.com/MiSTer-devel/MSX_MiSTer) | 86 | Yes | |
| [MSX1](https://github.com/MiSTer-devel/MSX1_MiSTer) | 86 | No | Optional<br>Required for Slot 1 ROM usage and ROM sizes larger than 256KB |
| [NEC PC8801](https://github.com/MiSTer-devel/PC88_MiSTer) | 75 | Yes | |
| [IBM PC/XT](https://github.com/MiSTer-devel/PCXT_MiSTer) | 50 | Yes | |
| [SAM Coupe](https://github.com/MiSTer-devel/SAM-Coupe_MiSTer) | 96 | Yes | |
| [Sharp X68000](https://github.com/MiSTer-devel/X68000_MiSTer) | 80 | Yes | |
| [Sinclair QL](https://github.com/MiSTer-devel/QL_MiSTer) | 84 | Yes | |
| [Spectravideo SV-328](https://github.com/MiSTer-devel/SVI328_MiSTer) | 43 | Yes | |
| [TI-99/4A](https://github.com/MiSTer-devel/TI-99_4A_MiSTer) | 43 | Yes | |
| [TSConf](https://github.com/MiSTer-devel/TSConf_MiSTer) | 84 | Yes | |
| [ZX Spectrum](https://github.com/MiSTer-devel/ZX-Spectrum_MISTer) | 112 | Yes | |
| [ZX Spectrum Next](https://github.com/MiSTer-devel/ZXNext_MISTer) | 112 | Yes | |

## Consoles - Classic
| Name | SDRAM Speed (MHz) | SDRAM Required? | Comments |
|:---:|:---:|:---:|:---:|
| [Atari 5200](https://github.com/MiSTer-devel/Atari800_MiSTer) | 57 | No | Optional<br>Required for memory config over 320KB or Cartridge use |
| [Atari 7800](https://github.com/MiSTer-devel/Atari7800_MiSTer) | 57 | Yes | |
| [Atari Lynx](https://github.com/MiSTer-devel/AtariLynx_MiSTer) | 64 | Yes | |
| [ColecoVision](https://github.com/MiSTer-devel/ColecoVision_MiSTer) | 43 | Yes | |
| [Game & Watch](https://github.com/MiSTer-devel/GnW_MiSTer) | 50 | Yes | |
| [Game Boy, Game Boy Color](https://github.com/MiSTer-devel/Gameboy_MiSTer) | 67 | Yes | Also includes the [Game Boy & Game Boy Color 2P](https://github.com/MiSTer-devel/Gameboy_MiSTer/tree/Gameboy2P) |
| [Game Boy Advance](https://github.com/MiSTer-devel/GBA_MiSTer) | 101 | No | Optional<br>Using onboard DDR memory may result in less accurate gameplay<br>If SDRAM is used, it requires up to the 64MB module, depending on the game |
| [Game Boy Advance 2P](https://github.com/MiSTer-devel/GBA_MiSTer/tree/GBA2P) | 101 | Yes | Requires up to the 128MB module, depending on the game |
| [Gamate](https://github.com/MiSTer-devel/Gamate_MiSTer) | 35 | Yes | |
| [Neo Geo MVS/AES](https://github.com/MiSTer-devel/NeoGeo_MiSTer) | 97 | Yes | Requires up to the 128MB module, depending on the game |
| [Nintendo Entertainment System (NES)](https://github.com/MiSTer-devel/NES_MiSTer) | 86 | Yes | |
| [PlayStation (PSX)](https://github.com/MiSTer-devel/PSX_MiSTer) | 102 | Yes | |
| [Pokémon Mini](https://github.com/MiSTer-devel/PokemonMini_MiSTer) | 40 | Yes | |
| [Sega 32X](https://github.com/MiSTer-devel/S32X_MiSTer) | 107 | Yes | |
| [Sega CD/Mega-CD](https://github.com/MiSTer-devel/MegaCD_MiSTer) | 107 | Yes | |
| [Sega Genesis/Mega Drive](https://github.com/MiSTer-devel/Genesis_MiSTer) | 107 | No | Optional<br>Using onboard DDR memory may result in less accurate gameplay |
| [Sega Master System & Game Gear](https://github.com/MiSTer-devel/SMS_MiSTer) | 54 | Yes | |
| [Super Game Boy](https://github.com/MiSTer-devel/SGB_MiSTer) | 86 | Yes | |
| [Super Nintendo Entertainment System (SNES)](https://github.com/MiSTer-devel/SNES_MiSTer) | 86 | Yes | |
| [SuperVision](https://github.com/MiSTer-devel/SuperVision_MiSTer) | 64 | Yes | |
| [TurboGrafx-16/PC Engine](https://github.com/MiSTer-devel/TurboGrafx16_MiSTer) | 86 | No | Optional<br>Using onboard DDR memory may result in less accurate gameplay |
| [Vectrex](https://github.com/MiSTer-devel/Vectrex_MiSTer) | 96 | Yes | |
| [WonderSwan](https://github.com/MiSTer-devel/WonderSwan_MiSTer) | 111 | Yes | |

## Arcade Cores
| Name | SDRAM Speed (MHz) | SDRAM Required? | Comments |
|:---:|:---:|:---:|:---:|
| [Asteroids Deluxe](https://github.com/MiSTer-devel/Arcade-AsteroidsDeluxe_MiSTer) | 100 | Yes | |
| [Bally Midway Astrocade](https://github.com/MiSTer-devel/Arcade-Astrocade_MiSTer) | 57 | No | Optional<br>Required for samples in Seawolf II and Gorf (with speech) |
| [Bally Midway MCR-2](https://github.com/MiSTer-devel/Arcade-MCR2_MiSTer) | 80 | Yes | |
| [Bally Midway MCR-3](https://github.com/MiSTer-devel/Arcade-MCR3_MiSTer) | 80 | Yes | |
| [Bally Midway MCR-Mono](https://github.com/MiSTer-devel/Arcade-MCR3Mono_MiSTer) | 80 | Yes | |
| [Bally Midway MCR-Scroll](https://github.com/MiSTer-devel/Arcade-MCR3Scroll_MiSTer) | 80 | Yes | |
| [Cave](https://github.com/MiSTer-devel/Arcade-Cave_MiSTer) | 96 | Yes | |
| [Gauntlet](https://github.com/MiSTer-devel/Arcade-Gauntlet_MiSTer) | 93 | Yes | |
| [Ikari Warriors](https://github.com/MiSTer-devel/Arcade-IkariWarriors_MiSTer) | 107 | Yes | |
| [Irem M62](https://github.com/MiSTer-devel/Arcade-IremM62_MiSTer) | 72 | Yes | |
| [Irem M72](https://github.com/MiSTer-devel/Arcade-IremM72_MiSTer) | 96 | Yes | |
| [Jackal](https://github.com/MiSTer-devel/Arcade-Jackal_MiSTer) | 98 | Yes | |
| [Moon Patrol](https://github.com/MiSTer-devel/Arcade-MoonPatrol_MiSTer) | 48 | Yes | |
| [Raizing](https://github.com/MiSTer-devel/Arcade-Raizing_MiSTer) | 95 | Yes | |
| [Scramble](https://github.com/MiSTer-devel/Arcade-Scramble_MiSTer) | 98 | Yes | |
| [Sega System E](https://github.com/MiSTer-devel/SMS_MiSTer) | 54 | Yes | |
| [Sonson](https://github.com/MiSTer-devel/Arcade-Sonson_MiSTer) | 72 | Yes | |
| [Subs](https://github.com/MiSTer-devel/Arcade-Subs_MiSTer) | 48 | Yes | |
| [Space Invaders](https://github.com/MiSTer-devel/Arcade-SpaceInvaders_MiSTer) | 80 | Yes | |
| [Tecmo](https://github.com/MiSTer-devel/Arcade-Tecmo_MiSTer) | 96 | Yes | |
| [Tropical Angel](https://github.com/MiSTer-devel/Arcade-TropicalAngel_MiSTer) | 74 | Yes | |
| [Universal<br>Cosmic Games](https://github.com/MiSTer-devel/Arcade-Cosmic_MiSTer) | 43 | Yes | |
| [VBall](https://github.com/MiSTer-devel/Arcade-VBall_MiSTer) | 96 | Yes | |
| [Xain'd Sleena](https://github.com/MiSTer-devel/Arcade-XSleena_MiSTer) | 96 or 120 | Yes | Two Cores available with differing SDRAM speeds<br>96MHz Core offers higher stability<br>120MHz Core offers 60Hz gameplay|
| [Zaxxon](https://github.com/MiSTer-devel/Arcade-Zaxxon_MiSTer) | 48 | Yes | |

_Note: SDRAM Speed is rounded to the nearest whole number._<br><br>
†_New cores may have been added after the latest publish date of this article. Be sure to take note of the publish date of the core and this article. Always assume new cores require the SDRAM Add-On Board, unless this article is updated after the publish date of the core._