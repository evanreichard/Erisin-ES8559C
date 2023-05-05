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
