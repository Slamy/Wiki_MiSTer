## Output frame locking
This technique allows to have output frame rate equaling to original emulated retro system. It gives a smooth scrolling and overall great experience in game playing.

## Analog TV
* All retro systems are targeted for analogue TV output which is very tolerant to off-spec parameters. Many PAL TVs can happily display frame rates as low as 47Hz or even lower. And it's the same for higher frame rates.
* Analogue TV doesn't have the parameter "pixel clock" as video is produced by continuous signal without quantization. So retro computers/consoles were free to choose any pixel clock most convenient for specific implementation. As a result, picture form such system had non-square pixel. And even if pixel looked like square it might be not 100% square as eye cannot distinguish small deviation on non-quantized analog display.
* Although analogue TV has defined amount of lines per field/frame it wasn't strictly followed by home systems. Some systems might supply 311 lines or 313 lines per field for PAL instead of standard 312.5. Some systems even supplied 320 lines due to simplified output logic giving in result 48Hz of frame rate.
* Some systems went more far and output irregular line lengths where some lines might be longer than others.

## Digital TV
* 