# PiFace Real Time Clock
PiFace Real Time Clock is a Real Time Clock (RTC) for the Raspberry Pi.

## Install
### Attach PiFace Clock
[Download the install script](https://raw.github.com/piface/PiFace-Real-Time-Clock/master/install-piface-real-time-clock.sh) and copy it to your
SD card. Make the script executable and then run it:

    chmod +x install-piface-real-time-clock.sh
    sudo ./install-piface-real-time-clock.sh

### Enable I2C
Run:

    raspi-config

Then navigate to `Advanced Options` > `I2C` and select `yes` to enable the ARM I2C interface.

### Set the correct date
Reboot and then set the correct date with `sudo date -s`, for example:

    sudo date -s "14 JAN 2014 10:10:30"

Replace `14 JAN 2014 10:10:30` with today's date and time.

### Set the hardware clock
Finally, save the system clock to the hardware clock with:

    hwclock --systohc

## Old versions
If you installed PiFace RTC using the old script (earlier than 2016-05-04)
then you might need to **remove** the following lines from `/etc/rc.local`:

    modprobe i2c-dev
    # Calibrate the clock (default: 0x47). See datasheet for MCP7940N
    i2cset -y 1 0x6f 0x08 0x47
    modprobe i2c:mcp7941x
    echo mcp7941x 0x6f > /sys/class/i2c-dev/i2c-$i/device/new_device
    hwclock --hctosys
