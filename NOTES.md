# Links

<https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable/you-will-need>

<https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/the-gpio-connector>

<https://elinux.org/RPi_Serial_Connection>

<https://www.instructables.com/id/Connect-the-Raspberry-Pi-to-network-using-UART/>

# Notes

* I'm using my MODEL B rev 1.0.

# Config

* Mounted partition 1 and added "enable_uart=1" to config.txt

# Serial console

* GND, RX, and TX on PIN6, PIN8, and PIN10, respectively.

## Console

Below does not work for console, you need to turn off hardware flow control (C-A Z -> O -> ...)

    _ nix run nixpkgs.minicom -c minicom -b 115200 -o -D /dev/ttyUSB0  

However, below works fine:

    _ nix run nixpkgs.screen -c screen /dedv/ttyUSB0 115200

# GPIO -> Relay

## Connecting

Relay IN:

    PIN25: GND -> GND
    PIN17: 3.3V -> VCC
    PIN19: GPIO10 -> Signal

Relay out:

Normally Open pin and COMmon pin, since we want HIGH to short-circuit.

## Enabling GPIO 10

PI:

    sudo -i
    echo "10" > /sys/class/gpio/export
    echo "out" > /sys/class/gpio/gpio10/direction

### Toggling GPIO 10

    echo "1" > /sys/class/gpio/gpio10/value
    echo "0" > /sys/class/gpio/gpio10/value
