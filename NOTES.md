# Notes

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
ffmpeg -i ../transition_cayman_s_white.mov -qscale:v 2 ./p4/Image00%03d.jpg

ffmpeg -i ../transition_cayman_s_white.mov -vf scale=1024:600 -qscale:v 2 ./p4/Image00%03d.jpg

# Zip Contents - You MUST use "store" compression (i.e. not compressing)
zip -0qry -i \*.txt \*.png \*.wav \*.jpg @ ../new_boot_anim.zip *.txt p*
```
