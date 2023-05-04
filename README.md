# Erisin ES8559C - Porsche 981, 991

- [Erisin Unit](https://www.erisin.com/products/erisin-es8559c-7-ips-android-110-car-multimedia-wireless-carplay-android-auto-radio-for-porsche-cayman-boxster-718-911-981-997-gps-dsp-4g-sim-card)
- [Planet-9 Thread](https://www.planet-9.com/threads/replacing-pcm3-1-with-erisin-android-head-unit-diy.253721/)
- [Related 4PDA Thread](https://4pda.to/forum/index.php?showtopic=1040251)
- [Google Drive Folder](https://drive.google.com/drive/folders/1SYMp1a5Os9GRDkuh8CGBxYlm-jM6-T46?usp=sharing)

# Codes

| Code       | Description                      |
| ---------- | -------------------------------- |
| 0000, 3368 | Factory Settings (Depends on FW) |
| 0000121    | Boot Config Settings             |
| 0000122    | Debug Settings                   |
| 5555       | Wireless ADB On                  |
| 55550      | Wireledd ADB Off                 |
| 55551      | OTG Host Mode                    |
| 55552      | OTG Device Mode                  |
| 99990      | VLog                             |
| 99992      | Engineering Mode                 |
| 99994      | MMI Test                         |

**Note:** Codes can be derived by decompiling the `carSettings-gm-master.apk` file. They exist in the decompiled `./sources/android/car/app/setting/FactorySettingFragment.java` file.

**PROCEED CAREFULLY:**

| Unconfirmed Codes | Description             |
| ----------------- | ----------------------- |
| 102420483096      | Settings Debug          |
| 101010            | Old App Settings        |
| 147258            | Enable Remote Debugging |
| 741852            | Close Remote Debugging  |
| 3725              | Board Check             |

# Boot Logo

See relevant files in the [BootLogo Google Drive Subfolder](https://drive.google.com/drive/folders/1MrPHdhb-9Hv6WGKhL2jqCdGr9AXF10k5?usp=share_link).

**NOTE:**

- Images must be named in the following format: `android_1024x600_arbitrary_text.png`
- Images must be JPG or PNG with 1024x600 dimensions

**Steps:**

1. Format FAT32 USB drive
2. Create folder `CAR_LOGO` on the root of the USB drive
3. Add all images to the `CAR_LOGO` folder
4. **Car Settings** -> **Factory Settings** -> **3368** or **0000** -> **Logo Setting** -> **Ext**

**Sources:**

- https://www.planet-9.com/threads/replacing-pcm3-1-with-erisin-android-head-unit-diy.253721/post-2212164
- https://4pda.to/forum/index.php?showtopic=1040251&view=findpost&p=118407686

# Boot Animation

See relevant files in the [BootAnimation Google Drive Subfolder](https://drive.google.com/drive/folders/1IrtB-HQWUK1TXJi2oPLXuqodUnlivZjw?usp=share_link).

```
# Replace 192.168.1.2 with the IP of the device
adb connect 192.168.1.2
adb root
adb remount
adb shell mkdir /system/ziqi/bootanim
adb push bootanimation.zip /system/ziqi/bootanim/bootanimation.zip
```

**Sources:**

- https://4pda.to/forum/index.php?showtopic=1040251&view=findpost&p=114141497

# Wireless ADB

To install ADB, please see the following [XDA Post](https://www.xda-developers.com/install-adb-windows-macos-linux/)

**Steps:**

1. Connect unit to WiFi
2. Enable Wireless ADB in **Car Settings** -> **Factory Settings** -> **5555**
3. Connect to ADB:

```
# Replace 192.168.1.2 with the IP that step #2 gave you
adb connect 192.168.1.2
```

You can now use regular `adb` commands:

- `adb root` -> `adb shell` will now take you to a root user
- `adb remount` -> makes system writeable
- `adb shell` -> open an interactive `sh` shell
- `adb install app.apk` -> install `app.apk` from your machine
- `adb push somefile.txt /tmp/somefile.txt` -> copy a local file to the device
- `adb pull /tmp/somefile.txt` -> copy a remote file from the device to your machine

# Root (Temporary)

## ADB Root

There's two different ways to get root. You can either `adb shell` and run `su`. Or run `adb root` which will always enter you into a root shell.

```
# Option 1
adb shell
su

# Option 2
adb root
adb shell
```

## Persistent Root (SuperSU / Magisk)

TBD

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

# Miscellaneous Notes

## Extract Firmware & Mount

```
# Install brotli (any package manager will do)
nix-shell -p brotli

# Decompress
brotli --decompress vendor.new.dat.br -o vendor.new.dat

# https://github.com/xpirt/sdat2img
sdat2img.py vendor.transfer.list vendor.new.dat vendor.img

# On macOS: https://github.com/gerard/ext4fuse
# On Linux you can mount a loopback device while specifying ext4 as the fs
ext4fuse system.img system/
```

## Create Boot Animation (bootanimation.zip)

See [bootanimation format](https://android.googlesource.com/platform/frameworks/base/+/master/cmds/bootanimation/FORMAT.md).

```
# Goal: Folder Layout
.
├── desc.txt
└── p4
    ├── Image00001.jpg
    ├── Image00002.jpg
    └── ...
```

```
# desc.txt
1024 600 45
p 0 0 p4

```

```
# Generate Image Files From Video File
ffmpeg -i ~/Desktop/black_main.mov ./p4/Image00%03d.jpg

# Zip Contents - You MUST use "store" compression (i.e. not compressing)
zip -0qry -i \*.txt \*.png \*.wav \*.jpg @ ../new_boot_anim.zip *.txt p*
```
