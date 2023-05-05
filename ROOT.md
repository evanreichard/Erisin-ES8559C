# Root

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

## Notes

The bootloader is unlocked. Rebooting into fastboot and running `fastboot getvar unlock` returns:

```
unlocked:yes
```

**Sources:**

- https://www.hovatek.com/forum/thread-19578.html
