---
layout: default
title: Troubleshooting
parent: Staff Guide
nav_order: 3
last_modified_at: 2023-10-20 14:37:48 -0500
---

### Services are failed
Use journalctl to see error logs of the service can usually give a better idea of what's going wrong.
```bash
$ sudo journalctl -u your_failed_service.service
```
If the `mbot-publish-info.service` is failed, you can go to `/var/log/mbot/mbot_pub_info.log` to see the detailed log.

### system util doesn't work
If you are using the `jetson-rob550_oct19.img.xz` image and have modified the mbot_config.txt file, but the robot does not show up in the IP registry or the OLED screen is not shown up, you can manuelly set things up.

1. Firstly you need an external monitor. Then connect the Jetson to wifi if you are using MWireless:
    ```bash
    $ cd ~/Downloads
    $ ./SecureW2_JoinNow.run     # this is wifi setup script
    ```
    - If you have message saying "...Configured Network is however not in range", it is likely that you have entered the wrong password, end the process and re-run the command.

2. Get your Jetson's IP address: `ifconfig wlan0`
3. Run the following commands to install system utilities 
```bash
$ cd mbot_sys_utils/
$ sudo ./install_scripts/install_mbot_dependencies.sh
# you should see "Jetson Nano detected Done Installing!" at the end
$ ./install_scripts/install_lcm.sh
# you should see "Done! LCM is now installed." at the end
```
4. Setup the MBot configuration
```bash
# copy the config file to boot directory
$ sudo cp mbot_config.txt /boot/firmware/
# edit the config
$ sudo nano /boot/firmware/mbot_config.txt
```
- `mbot_hostname`: give the robot a unique hostname in this file, it should match the name written on the mbot.
- `new_wifi_ssid` and `new_wifi_password`: you can also set up your home wifi here, enter your home Wi-Fi name and password accordingly.

5. Install udev rules and services 
```bash
# install udev rules
$ cd ~/mbot_ws/mbot_sys_utils/udev_rules
$ ./install_rules.sh
# Install the services needed to start the networking and report the robot’s IP
$ cd ~/mbot_ws/mbot_sys_utils/services
$ ./install_mbot_services.sh
```
6. Restart the robot to test
```bash
$ sudo reboot
```

If your hostname still does not appear, or OLED doesn't work, you can execute the following steps for troubleshooting:
```bash
$ cd ~/mbot_ws/mbot_sys_utils
$ ./systemctl_report.sh 
```