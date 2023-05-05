# Recovery

There's two different ways to access recovery.

1. _Already Booted:_ **Settings** -> **System** -> **System Update** -> **Reboot for Android Upgrade** -> Code `0000`. System will reboot into Recovery. Be sure not to have a USB Drive plugged in with a SW update file or it will flash it.
2. _On Boot:_ FAT32 USB Drive loaded with any FW version ZIP. On boot, the splash logo will show once, then go blank, at which point you immediately pull out the USB Drive. It will attempt and then fail, but drop you in Recovery on failure.

**Note:** If you cant access `adb` or `fastboot` in Recovery, then enter via the touch screen enter fastboot mode, then back to recovery.
