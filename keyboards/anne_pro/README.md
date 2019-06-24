# Anne Pro
QMK firmware port for the Obins Anne Pro 60% keyboard.

__This firmware is not created or supported by the creator of this keyboard!__

## Building the firmware
To build the firmware a few things have to be done.
First ChibiOS has to be patched, to do this use the provided script in the keyboard folder.
```
$ ./apply_patch.sh
```
After this build the Anne Pro firmware from the main folder.
```
$ make anne_pro
```
This produces a file `anne_pro_default.bin` in the main folder.

## Flashing the firmware
First find the correct device to flash.
```
$ dfu-util -l
...
Found DFU: [0483:df11] ver=0200, devnum=30, cfg=1, intf=0, path="20-1.1", alt=2, name="@BluetoothFlash  /0x1c000000/14*256 a,192*256 g", serial="017D37663036"
Found DFU: [0483:df11] ver=0200, devnum=30, cfg=1, intf=0, path="20-1.1", alt=1, name="@Internal Flash  /0x0c000000/64*256 a,192*256 g", serial="017D37663036"
Found DFU: [0483:df11] ver=0200, devnum=30, cfg=1, intf=0, path="20-1.1", alt=0, name="@Internal Flash  /0x08000000/64*256 a,192*256 g", serial="017D37663036"
...
```
Use the device with `Internal Flash 0x08000000` and specify the interface and alt. To flash use the following command.
```
$ dfu-util --alt 0 --intf 0 --dfuse-address 0x08004000 --download anne_pro_default.bin
```