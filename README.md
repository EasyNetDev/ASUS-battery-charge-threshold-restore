# ASUS Laptop battery charge threshold restore
In Linux Plasma or Gnome you can change ASUS Laptop the battery charge threshold to a specific value. Normaly ASUS recomands 80% for charging the battery to prolongue then battery lifespan.
But each time the laptop is rebooted or resuming from hibernation, this value is reset to default 100%.
These software is compose from 2 parts:
1. A small daemon written in C using fanotify to monitor to monitor changes in /sys/class/power_supply/BAT0/charge_control_end_threshold. As soon this file is changed, will will write the new value into /var/lib/asus/charge_control_end_threshold file.
2. A service which starts on system boot and will restore the value saved in /var/lib/asus/charge_control_end_threshold to /sys/class/power_supply/BAT0/charge_control_end_threshold .
3. A script /lib/systemd/system-sleep/asus-restore-battery-threshold that will be executed after system resume from hibernation and will restore the value saved in /var/lib/asus/charge_control_end_threshold to /sys/class/power_supply/BAT0/charge_control_end_threshold .
