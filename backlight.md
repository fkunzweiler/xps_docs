## Fix of OLED Backlight

- Install ddcci_backlight 
- add ddcci module

For Ubuntu 19.x:
- instal icc-brightness https://github.com/udifuchs/icc-brightness

Under pop.os 20.04 icc-brightness is not necessary anymore and the brightness works out of the box.

## Sync Backlight with external screens
- Install https://gitlab.com/ddcci-driver-linux/ddcci-driver-linux
- Add/Edit /etc/sudoers.d/reload_ddcci
  Add:
  `fkunzweiler ALL=(ALL) NOPASSWD: /sbin/modprobe -r ddcci_backlight`
  `fkunzweiler ALL=(ALL) NOPASSWD: /sbin/modprobe ddcci_backlight`
- Run sync_backlight.py


### Make backlight files editable by group video
replace the <vendor> with your vendor id. E.g. acpi_video0, intel_backlight)
cat /etc/udev/rules.d/backlight.rules
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="<vendor>", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="<vendor>", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
  
% usermod -aG video <user>
