# Firmware

See relevant files in the [Firmware Google Drive Subfolder](https://drive.google.com/drive/folders/16vZuCxMRC8vhnoHR3iDkOce6DdQ5e448?usp=share_link).

## Instructions

1. Format FAT32 USB drive
2. Copy firmware file to root of drive (do not extract, do not rename)
3. Plug in to running system
4. System will ask if you want to update and it'll reboot

Alternatively, if you're soft-bricked (stuck in the boot screen), you should be able to do the same as above and restart the unit. The pinhole reset button did nothing for me. I had to remove the quadlock in the back and plug it back in to restart the unit.

**NOTE:** If you want to format data on FW install, create a "ZQ_UPDATE_CONFIG" file (no extension) on the root of the USB Drive with the following contents:

```
format_data=1
```

## Files

The following has been confirmed working for me on an Erisin ES8559C.

**NOTE:** I only use CarPlay, Radio, BT, WiFi - but those all worked fine.

| Firmware                                         | Description                             |
| ------------------------------------------------ | --------------------------------------- |
| ZQ_A007_C55_HA4_U464-12-EN-D_2022-12-21-1826.zip | Stock Android 12 (received from Erisin) |
| ZQ_A007_C56_HA11_U859-EN-D_2023-03-28-1635.zip   | 4PDA Forums                             |
| ZQ_A007_C56_HA5_U551-EN-D_2022-08-23-1720.zip    | 4PDA Forums                             |
