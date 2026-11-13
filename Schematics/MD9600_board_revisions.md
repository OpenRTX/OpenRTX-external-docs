# TYT MD-9600 / Retevis RT90 board revisions

The main board schematic here, [`MD9600_main_board_schematic_rev2.0.pdf`](MD9600_main_board_schematic_rev2.0.pdf), is
the V2.0 board. No schematic for a later board has been published. TYT's FCC filings for later boards list every part
they changed, using the same designators as that schematic. So the V2.0 schematic plus the changes below describes
V4.1 and V5.0.

## Revisions

| Board | Synthesizers (U801, U901) | IF chips (U601, U701) | Stock firmware | Source |
|---|---|---|---|---|
| V1–V3 | SKY72310 | AK2365A | 0x.xx (03.28–06.24) | V2.0 schematic |
| V4.1 | AK1590 | AK2365A | 1x.xx (16.24, 16.45; "(V4)" in file names) | FCC change, 2020-11-04 |
| V5.0 | LMX2571NJKR | GT3136 | 2x.xx (26.38–26.45; "(2571V5)" in file names) | FCC change, 2021-03-25 |

- The firmware major gives the board family: "V0x.xx is for V1, V2 and V3 radios. … V1x.xx is for V4 radios. … V2x.xx
  is for V5 radios" (G4EML on the OpenGD77 forum, see sources). Firmware isn't interchangeable between families.
- Firmware 26.57 is named "(2571V4)": an LMX2571 build for a V4-numbered board, called V4A in the RadioFoundry spec.
  No FCC filing covers it, and how its board differs isn't known.
- The V5.0 board is silkscreened "MD9600-UV-V5.0-201107" (FCC internal photos, 2021). The V2.0 board is
  "MD9600-UV-V2.0-161118" (TYT's placement plots).
- The V2.0 → V3.0 changes aren't documented anywhere we know of.

## V3.0 → V4.1

[`MD9600_FCC_change_V3.0_to_V4.1.pdf`](MD9600_FCC_change_V3.0_to_V4.1.pdf), TYT's Class II permissive change letter
dated 2020-11-04. TYT's reason: "PLL changes in LMR section due to firmware update by the supplier."

| Sheet (V2.0 schematic) | Old | New |
|---|---|---|
| UHF and VHF PLL & VCO | U801, U901 SKY72310 | AK1590 |
| VHF PLL & VCO | U903 UBP1509GV | not fitted |
| UHF TX power | L523 ER1.0\*3.0\*2T, L516 ER1.0\*3.0\*3T, L525 and L526 ER1.0\*2.5\*3T | ER1.0\*2.5\*2T, ER1.0\*2.5\*4T, ER1.0\*3.0\*2T, ER1.0\*3.0\*2T |
| UHF TX power | C508–C513, C520–C525, C561, C576; D506–D509 MA2S728 | not fitted |
| UHF TX power | C527 27P, C543 30P, C544 47P, C555 27P, C562 NC, C563 47P, C564 12P, C565 22P, C575 3P, C577 4P | 33P, 33P, 39P, 33P, 8P, 33P, 18P, 27P, 10P, 8P |

The letter gives L523's old part as "RE1.0\*3.0\*2T", presumably a typo for ER.

## V4.1 → V5.0

[`MD9600_FCC_change_V4.1_to_V5.0.pdf`](MD9600_FCC_change_V4.1_to_V5.0.pdf), dated 2021-03-25. TYT's reason: "end
life of old PLL, the supplier Japan AKM was on fire at the end of Year 2020".

| Sheet (V2.0 schematic) | Old | New |
|---|---|---|
| UHF and VHF PLL & VCO | U801, U901 AK1590 | LMX2571NJKR |
| UHF PLL & VCO | C801 104, C802 104, R801 330R, EC801 1UF/10V | 683 0402, 474 0402, 47R 0402, 3.3UF/10V |
| UHF RX, VHF RX | U601, U701 AK2365A | GT3136 |
| RX IF (new parts) | FD501, FD701; CF601, CF701; CF602, CF702 | JTBM450CX24; LTWC450F; LTWC450H |
| RX IF (new parts) | U602, U603, U703, U704 | UMC4N |
| RX IF (new parts) | D609, D610, D709, D710 | DAN222 |
| UHF TX power | C527 33P, C561 not fitted | 12P 1206, 33P 1206 |
| VHF TX driver | C483 22P, L417 47NH, C472 47P | not fitted, 33NH 0603, 82P 0402 |

The letter gives U901's old part as "AK15900", presumably AK1590. The new 450 kHz filters (FD, CF) and switches
(UMC4N, DAN222) belong to the GT3136 IF stage, whose circuit isn't in the V2.0 schematic.

## What didn't change

Neither letter lists a part on the FM AF, baseband and AF amp, MCU or power sheets (designators 1xx, 2xx, 3xx, 10xx).
Those sheets should still describe V4.1 and V5.0, apart from any undocumented V2.0 → V3.0 changes. The V5.0 FCC
photos show the same STM32F405VGT6, HR_C6000, LA4425A and W25Q flash.

TYT calls both changes "pin-to-pin compatible" and "electrically identical". That is the filing's wording: the
synthesizers and IF chips are different parts, and each board family needs its own firmware.

## Sources

- FCC ID POD-DMR3 (original grant 2017-12-28): https://fccid.io/POD-DMR3. The change letters are
  https://fccid.io/pdf.php?id=5000327 and https://fccid.io/pdf.php?id=5195313. The internal photos of the 2020-11
  (V4.1) and 2021-04 (V5.0) filings show the boards; the V5.0 set shows the silkscreen, the LMX2571s and the
  "3136"-marked IF chips.
- TYT's 2018 dealer service bulletins, mirrored by KD7TWW:
  https://qsl.net/k/kd7tww/Radios/TYT%20Radios/9600/MD-9600%20updated%20firmware%20issued%20on%2022nd%20Mar%202018/
  - V2.0 component placement plots, top and bottom, with designators (`MD9600-UV-V2.0-20170417-TOP(Location).pdf`,
    `-Bottom(Location).pdf`), and a V2.1 bottom plot with values.
  - "hand mic light on": a front panel fix adding a UMC4N switch so the hand mic's supply (RJ-45 pin 3, which feeds
    the electret bias and the keypad LEDs) follows the GPS enable line, with a photo of the front panel schematic.
- OpenGD77 forum, "MD-9600/RT-90 Schematic" (2024-03-07), where the V2.0 schematic was posted, with G4EML's note that
  it is "a very early schematic for V2 radios":
  https://www.opengd77.com/archive/viewtopic8990.html?f=18&t=3852
- G4EML on the firmware major and board family:
  https://www.opengd77.com/archive/viewtopic18db.html?f=18&t=3948#p36880
- RadioFoundry's MD-9600 hardware notes (MIT): pins, stock firmware files, revisions:
  https://github.com/RadioFoundry/RadioFoundry/blob/main/docs/spec/hardware-md9600.md
- In this folder: the hand mic schematic (`MD9600_mic_schematic.pdf`) and DG4EK's annotated bottom photo
  (`MD9600_bottom_annotated.jpeg`, a V1–V3 board from his 2018 article).
