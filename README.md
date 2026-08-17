This repo is the originally ported from https://www.fischl.de/usbasp/ to Platformio environment for easy and simple compilation and also tested on USBasp hardware.
## Some technical information:
- VSCode Extension: PlatformIO 3.4.4
- PLATFORM: Atmel AVR (5.2.0) > USBasp stick
- HARDWARE: ATMEGA8 12MHz, 1KB RAM, 8KB Flash
- PACKAGES: toolchain-atmelavr @ 1.70300.191015 (7.3.0)

 **Have a try the modified main.c in main_mod folder experience little different behavior of LEDs on USBasp board.**

## To modify the USB Vendor ID (VID) and Product ID (PID):
In your custom USBasp firmware, you must make the changes inside src/usbconfig.h.Because V-USB is a software-only USB implementation, these IDs are defined as simple compilation macros that get baked straight into the device descriptors sent to your Operating System. Open src/usbconfig.h and search for USB_CFG_VENDOR_ID and USB_CFG_DEVICE_ID. You will find lines that look exactly like this:
```cpp
#define  USB_CFG_VENDOR_ID       0xc0, 0x16
/* This is the vendor ID for Thomas Fischl (0x16c0) */

#define  USB_CFG_DEVICE_ID       0xdc, 0x05
/* This is the product ID for USBasp (0x05dc) */
```
Notice that Thomas Fischl's official IDs are written backward!The actual Vendor ID is 0x16C0, but in the code, it is written as 0xc0, 0x16.The actual Product ID is 0x05DC, but in the code, it is written as 0xdc, 0x05.When you input your own custom IDs, you must swap the first and second byte because the USB protocol reads multi-byte values in Little-Endian format.
## Change Device Name:
While you are inside usbconfig.h, you can also change the textual name that pops up when you plug the device into your PC. Scroll down slightly and locate these fields:
```cpp
#define USB_CFG_VENDOR_NAME     'm', 'y', 'n', 'a', 'm', 'e'
#define USB_CFG_VENDOR_NAME_LEN 6

#define USB_CFG_DEVICE_NAME     'C', 'u', 's', 't', 'o', 'm', 'A', 'S', 'P'
#define USB_CFG_DEVICE_NAME_LEN 9
```
NOTE: Make sure USB_CFG_DEVICE_NAME_LEN exactly matches the exact count of single-quoted characters you type.
