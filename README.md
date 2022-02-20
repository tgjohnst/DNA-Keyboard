# DNA-Keyboard
Documentation for building a simple 4-key USB Keyboard that has ACGT to act as the equivalent of a tenkey for bioinformatics

## Rationale


## Parts

The first build will be based on the [4Pack macropad](https://www.40percent.club/2017/07/4-pack.html)

### Parts
- PCBs and plates - [4pack PCB](https://github.com/di0ib/Misc/tree/master/4pack) fabricated by [JLCPCB](https://www.40percent.club/2017/09/ordering-foobar-pcbs.html)
- Pro Micro microUSB (or Elite-C v4 USB-C, will try both) controller with pin headers ordered from [KeebIO](https://keeb.io/collections/diy-parts)
- 9mm M2 standoffs and 6mm M2 screws from [KeebIO](https://keeb.io/collections/diy-parts)
- Keycaps - [R3 milk blanks](https://www.amazon.com/dp/B096Z2ZK2Y).
- LEDs - [3mm round flangeless dome-top LEDs (RGBY)](https://www.digikey.com/catalog/en/partgroup/3mm-t-1-round-with-domed-top-led-lamps/35724?mpart=OVLBB4C7)
- Resistors (2) (100 Ohm)
- Gateron KS-9 Red MX Keyswitches
- White silicone SKUF feet from [KeebIO](https://keeb.io/collections/diy-parts)
- microUSB / USBC cable
### Tools
- Soldering iron + Solder + Solder wick + Third hand + Ventilation


## Firmware
### Installing QMK
Install QMK (using conda within WSL, because I prefer a unix environment)
```
conda create -n qmk python=3
conda activate qmk
pip install qmk
qmk setup # Answer y to prompts
```
### Compiling the firmware
```
qmk compile -kb 40percentclub/4pack
qmk config user.keyboard=40percentclub/4pack
qmk config user.keymap=tgjohnst
qmk new-keymap
```
### Changing the Keymap
Edit the created keymap.c (to open `/home/lotus/qmk_firmware/keyboards/40percentclub/4pack/keymaps/tgjohnst` in explorer just cd there and do `explorer.exe .`) in a text editor. Change the layout to:
```
const uint16_t PROGMEM keymaps[][MATRIX_ROWS][MATRIX_COLS] = {
    [0] = LAYOUT( /* Base */
        KC_T, KC_G, KC_C, KC_A
    ),
};
```
Then, compile the new keymap (assuming the defaults were set with `qmk config` above
```
qmk compile
```
### Flashing the firmware
You cannot flash directly from WSL, so install QMK Toolbox https://github.com/qmk/qmk_toolbox .

Load up QMK toolbox and select the .hex file you created in the last compile step. Select `Auto-Flash`.

Connect your keyboard to a **USB 2.0** port (3.0 has issues). short out the ground and reset pin twice in quick succession to initiate a reset. QMK toolbox should detect the device and start flashing.
