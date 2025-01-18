# Flashing Custom BIOS for Asrock BC-250

## Overview

Flashing a custom BIOS onto the Asrock BC-250 was a critical part of this project, enabling manual control over the RAM allocation between the CPU and GPU. Below is a step-by-step guide on how to flash the custom BIOS using an SPI reader and ASProgrammer.

### Requirements:
- **CH431 SPI Reader** (or compatible SPI programmer)
- **ASProgrammer** (software for flashing BIOS)
- **Custom BIOS File** (the modified BIOS file you want to flash)
- **Backup of Original BIOS** (always ensure you have a backup before flashing)

## Steps to Flash the Custom BIOS

1. **Backup the Original BIOS:**
   - Use the **CH431 SPI reader** to connect to the BIOS chip on the Asrock BC-250 motherboard.
   - Using **ASProgrammer**, read and store the original BIOS file as a backup. This ensures you can restore the original BIOS if anything goes wrong.

2. **Flash the Custom BIOS:**
   - After backing up the original BIOS, load your custom BIOS file into **ASProgrammer**.
   - Ensure the custom BIOS is selected and the SPI reader is correctly connected to the BIOS chip.
   - Using **ASProgrammer**, proceed to flash the custom BIOS onto the chip.
   - Wait for the process to complete before disconnecting the SPI reader.

This process was made possible thanks to the work done by [TuxThePenguin0](https://github.com/TuxThePenguin0), whose documentation and contributions were essential in enabling BIOS modification on the BC-250.

---

## Warning

**Flashing the BIOS can be risky.** There is always a possibility of bricking your device if something goes wrong during the flashing process. **Proceed at your own risk.**

- **Backup your original BIOS** before making any modifications.
- **Ensure proper connections** when flashing to avoid corrupting the BIOS.
- **If the BIOS is flashed incorrectly**, it may cause permanent damage to your system or make it unbootable.

**I take no responsibility for any damage caused by flashing the BIOS.** You are responsible for the outcome of any modifications you make to your hardware.
