---
layout: default
title: Manually Enter Bootloader Mode
parent: How-to Guide
grand_parent: Botlab
nav_order: 5
last_modified_at: 2024-10-16 16:37:48 -0500
---

> This post explains how to manually enter bootloader mode and flash calibration scripts and firmware to your MBot.

These instructions serve as an alternative to "MBot System Setup -> Set Up MBot Firmware -> 2. Calibrate the MBot and Flash the Firmware."
{: .text-red-200}

Use the method described here **only** if the one in the system setup post is unsuccessful.

### RST button + BOOTSEL button
1. Initiate a remote connection with VSCode.
2. Enter bootloader mode
    1. Press hold RST button and then press hold BOOTSEL button (you are pressing 2 buttons now).
    2. Let go RST button while still pressing BOOTSEL (you are pressing 1 button now).
    3. Let go BOOTSEL.

    The BOOTSEL button is indicated in the image, with the RST button located on the opposite side of the Type-C socket.

    <a class="image-link" href="/assets/images/botlab/system-setup/bootsel.png">
        <img src="/assets/images/botlab/system-setup/bootsel.png" alt=" " style="max-width:270px;"/>
        </a>

3. Upload the calibration file by the following commands:
```bash
$ cd ~/mbot_ws/mbot_firmware
$ sudo picotool load build/mbot_calibrate_classic_v1.1.0_enc48.uf2
```

4. Place the MBot on the floor in a spot with at least 2 feet of clear space all around the robot.
```bash
$ sudo picotool reboot
```
    - The Pico will reboot automatically, and will then run its calibration routine. Allow the Pico to finish its calibration routine without interference.

The calibration script will have saved parameters onto the Pico’s memory. We can now flash the firmware that will run on the Pico during operation.

Repeat the step 2 above to put the Pico to bootloader mode, then run
```bash
$ cd ~/mbot_ws/mbot_firmware
$ sudo picotool load build/mbot_classic_v1.1.0_enc48.uf2
$ sudo picotool reboot
```
