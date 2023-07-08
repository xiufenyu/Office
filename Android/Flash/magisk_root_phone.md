1. How to edit "/system/etc/hosts"
Magisk: Settings-> Systemless hosts

# Root Android with Magisk

1. Download and install Magisk Manager in the android phone: https://github.com/topjohnwu/Magisk/releases

2. Download the Factory android image from the website: https://developers.google.com/android/images

$ oriole-sq31.220705.004.a1-factory-1fb143dd.zip

$ unzip oriole-sq31.220705.004.a1-factory-1fb143dd.zip

$ cd oriole-sq31.220705.004.a1-factory-1fb143dd

$ unzip oriole-sq3a.220705.004.a1.zip

$ cd oriole-sq3a.220705.004.a1

$ adb push boot.image /sdcard/Download

3. use MagiskManager to install boot.img
    Magisk Install 

4. Download the patched image to Linux

$ adb pull /sdcard/Download/magisk_patched-25200_3JvWa.img  ~/Downloads/

$ adb reboot bootloader

$ fastboot devices

-> 19261FDF60051D   fastboot


5. Try boot first

$ fastboot boot magisk_patched-2500_3JvWa.img


6. if it is working, flash firm to the bootloader

$ fastboot flash boot magisk_patched-2500_3JvWa.img

$ fastboot reboot


Question:  command(boot) is not allowed when locked?

$ fastboot flashing unlock