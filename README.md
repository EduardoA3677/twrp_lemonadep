# Device Tree for 9 Pro (lemonadep) for TWRP

## Setup repo tool
Setup repo tool from here https://source.android.com/setup/develop#installing-repo

## Compile

Sync TWRP manifest:

```
repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1

```

Make a directory named local_manifest under .repo, and create a new manifest file, for example local_manifests.xml
and then paste the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project path="device/oneplus/lemonadep" name="EduardoA3677/twrp_device_oneplus_lemonadep" remote="github" revision="a12" />
</manifest>
```
You might need to pick few patches from gerrit.twrp.me to get some stuff working.

Sync the sources with

```
repo sync -j$(nproc --all)
```
apply the patches as indicated by the minimum manifest
```
repopick 5405 5540
```
To build, execute this command:

```
. build/envsetup.sh; export ALLOW_MISSING_DEPENDENCIES=true; export LC_ALL=C; lunch twrp_lemonadep-eng; make -j$(nproc --all) adbd bootimage
```

To test it:

```
# To temporarily boot it
fastboot boot out/target/product/lemonadep/boot.img 

# you can flash the recovery with
fastboot flash boot boot.img
```

Kernel: https://github.com/LineageOS/android_kernel_oneplus_sm8350

##### Credits
- ApexLegend007 For Recovery Trees of Oneplus 9r
- The-Incognito For Recovery Trees of Oneplus 8T
- YumeMichi For Implementing Erofs and Other Misc
- bigbiff for decryption
- Systemad for original tree
- CaptainThrowback for original tree
- mauronofrio for original tree
- TWRP team
- Qnorsten for OOS fix
