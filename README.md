WORK IN PROGRESS - NOT READY

# Input Shaping for the MK3S/+, an easy method for a powerful upgrade
Tired of seeing everyone upgrading to MK4s and feeling like you're missing out on the action? This project is an attempt to create simple, easy-to-follow documentation for performing an inexpensive, simple, and powerful upgrade to your Prusa MK3S/+. Originally based on work by dz0ny (https://github.com/dz0ny/klipper-prusa-mk3s).


**There are several reasons you should try this upgrade:**
1. **Speed** - As you may know, Input Shaping can allow for substantial speed and print quality improvements to your printer. It's all the rage right now in the 3D Printing community.
2. **Low Cost** - It's inexpensive, requiring just $50-100 in hardware, which is a reasonable savings compared to the Prusa MKS3.5 Upgrade Kit.
3. **Simplicity** - We have structured our instructions and documentation to make this as simple as possible, despite the fact that Klipper is involved, and historically has been thought of as difficult to implement. Klipper is very powerful, and can be simple when implemented correctly.
4. **Easy to Return to Stock** - Undoing this upgrade and returning to stock Prusa firmware takes just a few steps, and can be completed in under 15 minutes.
5. **No Waste** - Your MK3S/+ Printer will not collect dust. Many in the Prusa community recommend either buying an MK4 while selling or keeping your MK3S. This upgrade allows you to keep your printer, while substantially increasing speed, and potentially increasing print quality.

**How will we do this?**

We will implement Input Shaping on your MK3S/+ with the use of Klipper. "YIKES, Klipper?! Isn't that super complicated?" No, while Klipper can be difficult to use, we've put in the work for you to allow for a simple  installation and configuration of Klipper.

**What if I need to return to stock?**

Undoing this upgrade and returning to stock Prusa firmware takes just a few steps, and can be completed in under 15 minutes. Please see the section "Reverting to Stock Prusa Firmware".

## Hardware Required

- Prusa MK3S or MK3S+
  - Compatible hotends: Stock, Dragon ST, Dragon HF
  - Compatible extruders: Stock, Bondtech BMG 
- Raspberry Pi Zero 2 W - https://amzn.to/3ODvStE
  - Raspberry Pi 3B+/4/5+ will also work, but tend to be more expensive
  - Raspberry Pi Zero W is not recommended, and may not work

- USB Type B male to USB Type A male cable (Came with your Prusa)
- USB Type A female to MicroUSB male converter (if using a Pi Zero 2 W, included in kit linked above)
- KUSBA: Klipper USB Accelerometer (enables easier Input Shaping calibration) - https://amzn.to/4bzgAzA
  - Optional, but recommended.
- (HOW DOES THE KUSBA CONNECT TO THE PI? I actually don't fully know) FIXME
-

(INSTRUCTIONS SECTION)

(KUSBA Specific info gathering)
Discuss:
1) What is the KUSBA
2) Why we use this Rampon firmware
3) How this whole thing works lol
4) Link to their instructions: https://github.com/xbst/KUSBA/blob/main/Docs/v2-Rampon-Firmware.md











 

CURRENT PROGRESS MARKER - ALL BELOW IS FROM ORIGINAL REPO

## Pre-Check

- Get Z offset value from your current firmware (Menu -> Calibration -> Z-offset), you will need it for the Klipper config.
- Your bed needs to be perpendicular (based on XYZ Calibration). If not you will have to do the skew calibration before printing or you risk crashing your nozzle to the bed.
- Read https://github.com/dz0ny/klipper-prusa-mk3s/blob/main/printer.template.cfg
- Read https://www.klipper3d.org/Installation.html#building-and-flashing-the-micro-controller

## Install
1. Install https://docs.mainsail.xyz/setup/mainsail-os to SDCard and RPI Zero 2 W
2. Connect as described in https://help.prusa3d.com/en/article/raspberry-pi-zero-w-preparation-and-installation_2180
3. Update all components under Machine tab, otherwise config might not be able to load
4. Clone config ```git clone https://github.com/dz0ny/klipper-prusa-mk3s.git ~/printer_data/config/klipper-prusa-mk3s```

  > If you are adding this configuration after installing Klipper via [KIAUH](https://github.com/th33xitus/kiauh), the directory might be different - typically following `~/[printer_name]/printer_data/config`, where `[printer_name]` is the name you selected during the Kiauh installation

5. Add the following to the to `moonraker.conf` to enable automatic updates

```yml
[update_manager prusa]
type: git_repo
origin: https://github.com/dz0ny/klipper-prusa-mk3s.git
path: ~/printer_data/config/klipper-prusa-mk3s
primary_branch: main
is_system_service: False
managed_services: klipper
```

2. Copy https://github.com/dz0ny/klipper-prusa-mk3s/blob/main/printer.template.cfg to `printer.cfg` in your klipper config (THIS IS INCORRECT, THERE WAS NO PRINTER.CFG WHEN I INSTALLED, SO IT'S DUPLICATE, RENAME, and MOVE or whatever.)
3. Adjust config to your hardware
4. Flash Klipper to your printer https://www.klipper3d.org/Installation.html#building-and-flashing-the-micro-controller (MOVE THEIR COMMANDS INTO MINE, TOO MUCH EXTRA INFO IN THIS LINK. All that's needed is Change Folders, Configuration from this repo in it, check the serial ID # command, then flash)

You will still need a USB cable as you cannot flash via an internal serial port. You can also use any other computer to compile your firmware.

To use this config, the firmware should be compiled for the AVR atmega2560. To use via serial, in "make menuconfig" select "Enable extra low-level configuration options" and select **serial1** (the RasPi serial) or **serial0** when you plan to connect via the USB.

To flash:
`make flash FLASH_DEVICE=/dev/serial/by-id/usb-Prusa_Research__prusa3d.com__Original_Prusa_i3_MK3_CZPX0620X004XK70128-if00` (NOT CORRECT, YOU NEED TO USE YOUR SPECIFIC PORT ID)

7. Print


## Nice things
[Klipper mesh on print area only install guide](https://gist.github.com/ChipCE/95fdbd3c2f3a064397f9610f915f7d02)


## Screenshots
![image](https://user-images.githubusercontent.com/239513/141822711-2818978e-2b87-4110-9b93-e5f489c9cdc7.png)
![image](https://user-images.githubusercontent.com/239513/141831204-89ced257-e67f-4b1f-add7-a3806cdd2617.png)
![image](https://user-images.githubusercontent.com/239513/141831245-11476041-240d-424a-8ff8-ffd8a03c08be.png)
![image](https://user-images.githubusercontent.com/239513/141831272-31b88652-ab3f-4978-8a4c-c54a83817dd1.png)
