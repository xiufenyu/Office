1. Install Magisk App to the Android phone

2. Enable root access in adb shell   \
   Open Magisk-> Superuser -> [SharedUID] Shell -> Click Enable


3. Enable Zygisk   \
   Home -> Setting -> Magisk -> Zygisk -> Click Enable

   The correct Image of a rooted phone in Magisk: \
   Magisk: \
   Installed 8388113b (27007)   \ 
   Zggisk   Yes   \
   Ramdisk   Yes   \
   
   

5. Install movecert module in Magisk \
   upload movecert.zip to /sdcard/Download/movecert.zip
   (Android) $ adb shell   \
   (Android ) $ su   \
   (Android)$ magisk --install-modules /sdcard/Download/movecert.zip



6. Install MagiskFrida Module  \ 
   Download MagiskFrida from https://github.com/ViRb3/magisk-frida/releases            \
   $ adb push  MagiskFrida-16.5.1-1.zip /sdcard/Download/                              \
   (Android) $ magisk --install-module /sdcard/Download/MagiskFrida-16.5.1-1.zip       \
   $ adb reboot

   Check if frida is working               \
   (ubuntu)$ frida-ps -U 
   
