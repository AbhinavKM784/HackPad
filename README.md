# HackPad
Designing a 4 key hackpad for nusic playback. Forgot the volume knob
Designed it so that i can pause/play, mute, skip music,replay music in 4 buttons.

Schematic
<img width="559" height="587" alt="HackPad PCB Schematics" src="https://github.com/user-attachments/assets/8ea31ab3-7aa1-48fe-9cf7-9e9d4c5b9f1d" />

PCB
<img width="514" height="556" alt="HackPad PCB Editing" src="https://github.com/user-attachments/assets/f92ffdf8-c983-4b68-b57d-a10b7a6e1970" />

Case:
Top

<img width="353" height="383" alt="HackPad Top Cad" src="https://github.com/user-attachments/assets/d5cd8cbe-cee0-475b-b454-fff0897b099f" />

Bottom

<img width="1273" height="542" alt="HackPad Bottom Cad" src="https://github.com/user-attachments/assets/57de4c39-aef7-4b43-b06e-bd03b9bf8ce7" />

Half- Assembled

<img width="484" height="516" alt="assembled case" src="https://github.com/user-attachments/assets/87fcc677-c908-41bb-ab21-fb2d6051fbd5" />

Full-Assembled

<img width="331" height="383" alt="Full Assembled Case" src="https://github.com/user-attachments/assets/6701fc28-02b2-40db-938e-65aece50b30c" />

BOM:
Seeed XIAO RP2040 
Through-hole 1N4148 Diodes (Max 20x)
MX-Style switches (Max 16x)
EC11 Rotary encoders (Max 2x)
0.91 inch OLED displays (Max 1x) (make sure the pin order is GND-VCC-SCL-SDA, otherwise it WILL NOT WORK)
Blank DSA keycaps (White)
SK6812 MINI-E LEDs (Max 16x)
M3x16mm screws
M3x5mx4mm heatset inserts
3D PRINTED CASE ONLY. NO ACRYLIC.

QMK Firmawre for Keyboard
```
import board

from kmk.kmk_keyboard import KMKKeyboard
from kmk.scanners.keypad import KeysScanner
from kmk.keys import KC
from kmk.modules.macros import Press, Release, Tap, Macros


keyboard = KMKKeyboard()


macros = Macros()
keyboard.modules.append(macros)


PINS = [board.D3, board.D4, board.D2, board.D1]


keyboard.matrix = KeysScanner(
    pins=PINS,
    value_when_pressed=False,
)

Mute = KC.MACRO(
	Press(KC.LCTL)
	Tap(KC.F4)
	Delay(10)
	Release(KC.F4)

)
NextSong = KC.MACRO(
	Press(KC.LCTL)
	Tap(KC.F8)
	Delay(10)
	Release(KC.F8)

)
PrevSong = KC.MACRO(
	Press(KC.LCTL)
	Tap(KC.F4)
	Delay(10)
	Release(KC.F4)

)

Pause = KC.MACRO(
	Press(KC.LCTL)
	Tap(KC.F7)
	Delay(10)
	Release(KC.F7)

)


keyboard.keymap = [
    [Mute, , Pause, PrevSong,NextSong ]
]

# Start kmk!
if __name__ == '__main__':
    keyboard.go()
```




