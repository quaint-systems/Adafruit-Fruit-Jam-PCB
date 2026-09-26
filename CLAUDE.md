# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Open-source hardware design files for the Adafruit Fruit Jam (product 6200), a credit-card-sized (ISO/IEC 7810 ID-1, 3.375" x 2.125") RP2350B computer. There is no source code, build system, linter, or test suite — only EAGLE CAD design files, pinout docs, and prebuilt firmware binaries.

## Layout

- `Adafruit Fruit Jam.sch` / `.brd` — the main board. Schematic spans 2 sheets (~300 parts); board is 2-layer (`layerSetup (1*16)`) using the `adafruit 7-7` design rules.
- `Adafruit Fruit Jam Front Plate.sch` / `.brd` — a separate PCB used as a mechanical front plate (few parts, mostly outline/graphics).
- `Adafruit_Fruit_Jam_PrettyPins.svg` / `.pdf` — pinout diagram generated from the design; regenerate/update both together if pin assignments change.
- `factory-reset/` — prebuilt UF2 images for drag-and-drop flashing in the RP2350 bootloader:
  - `Adafruit_Fruit_Jam_Factory_Reset.uf2` — NeoPixel rainbow swirl on the 5 onboard NeoPixels.
  - `Adafruit_Fruit_Jam_Full_Demo.uf2` — full peripheral hardware test, built from the Arduino sketch in `adafruit/Adafruit_Learning_System_Guides` at `Factory_Tests/Fruit_Jam_Factory_Test/Fruit_Jam_Factory_Test.ino` (source is not in this repo).
- `assets/` — product photo used by the README.

## Working with the EAGLE files

- Files are EAGLE 9.6.2 XML (`eagle.dtd`), so they can be inspected with `grep` or an XML parser (e.g. Python `xml.etree`) instead of opening EAGLE. Useful elements: `<part>` / `<instance>` (schematic parts), `<net>` / `<segment>` / `<pinref>` (schematic connectivity), `<element>` (board placements), `<signal>` (board nets/copper).
- The main `.brd` is ~4 MB and the `.sch` ~1.3 MB — search with targeted `grep` rather than reading whole files.
- The `.sch` and `.brd` of a pair are forward/back-annotated in EAGLE; hand-editing only one side of the XML will break consistency. Prefer describing changes for the user to make in EAGLE unless a mechanical text edit (e.g. a part value or label) is clearly safe on both files.

## Key hardware (from README)

RP2350B (QFN-80), 16 MB flash + 8 MB PSRAM, USB-C (bootloader/device), microSD (SPI or SDIO), DVI out on the HSTX port, TLV320DAC3100 I2S DAC (stereo headphone + mono speaker), 2-port USB-A hub (PIO USB host), PicoProbe debug port, Stemma QT I2C, Stemma JST 3-pin, 5x NeoPixels, 3x tactile switches, 16-pin socket header (10 A/D GPIO + power).

## License

CC BY-SA (see `license.txt`). The README's license/attribution text must be kept in any redistribution.
