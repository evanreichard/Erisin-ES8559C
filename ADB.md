# ADB

Wireless is the easiest option. However, if you need to get `adb` or `fastboot` access via USB (needed in recovery or fastbood mode), you will need to create your own USB cable.

To install ADB, please see the following [XDA Post](https://www.xda-developers.com/install-adb-windows-macos-linux/)

## Wired ADB

Fortunately on the back of this Erisin unit theres a connector for USB OTG access. The connector should be labeled "OTG" and is directly to the right of the normal USB connector. It is labeled as "E".

The pinout is on the device itself, but if you need it:

```
+--------------------+-------------------+
| (1) Data Negative  | (2) Data Positive |
+--------------------+-------------------+
| (3) Ground         | (4) +5V           |
+--------------------+-------------------+
```

**Steps:**

1. Enable Developer Options (**Settings** -> **About Device** -> Tap **Build number** a bunch of times)
2. Enable USB Debugging (**Settings** -> **System** -> **Developer Options** -> Toggle **USB Debugging**)
3. Enable USB OTG Device Mode (**Settings** -> **Car Settings** -> **Factory Settings** -> Code **55552**)
4. Once the OTG USB cable is wired up and connected to your device, you should see the device in `adb devices`

## Wireless ADB

**Steps:**

1. Connect to WiFi
2. Enable Wireless ADB (**Settings** -> **Car Settings** -> **Factory Settings** -> Code **5555**)
3. Connect to ADB over WiFi:

```
# Replace 192.168.1.2 with the IP that step #2 gave you
adb connect 192.168.1.2
```

## ADB Commands

- `adb root` -> `adb shell` will now take you to a root user
- `adb remount` -> makes system writeable
- `adb shell` -> open an interactive `sh` shell
- `adb install app.apk` -> install `app.apk` from your machine
- `adb push somefile.txt /tmp/somefile.txt` -> copy a local file to the device
- `adb pull /tmp/somefile.txt` -> copy a remote file from the device to your machine
