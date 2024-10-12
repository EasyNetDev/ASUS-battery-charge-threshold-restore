# ASUS Laptop battery charge threshold restore
In Linux Plasma or Gnome you can change ASUS Laptop the battery charge threshold to a specific value. Normaly ASUS recomands 80% for charging the battery to prolongue then battery lifespan.
But each time the laptop is rebooted or resuming from hibernation, this value is reset to default 100%.

These software written in C is a multi-call binary with these applets:
1. An applet daemon which is using inotify to monitor changes in `/sys/class/power_supply/BAT0/charge_control_end_threshold`. As soon this file is changed by the user from CLI or Plasma/Gnome, it will write the new value into `/var/lib/battery-charge-threshold/value` file.
2. An applet restore is used in `/lib/systemd/system-sleep` to restore form hibernation or suspend the Charge Control End Threshold for the battery.
3. An applet save to save current value of `/sys/class/power_supply/BAT0/charge_control_end_threshold` manually to `/var/lib/battery-charge-threshold/value` .

Also the package will have a service to start the daemon on system booting.
