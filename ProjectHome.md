# Introduction #
This is a very small project that aims to replicate parts of the functionality provided by LBTServ.exe, the Bluetooth service from Logitech that switches Bluetooth dongles from HID mode to HCI mode.

# Why should I use this? #
  * Because the standard Logitech service does not support some devices, for example the Logitech diNovo Mini Dongle. That’s the reason I initially wrote this service.
  * Because sometimes it’s just impossible to get the Logitech service to recognize/pair your keyboard and even if you succeed next time you reboot you’d have to do it all again. This happened to me with my Cordless Desktop MX 5000 Laser. The solution was to disable their service and use my own. And it’s been working ever since.


# What does it do? #
At system startup (service startup) or after a computer resume it will scan the computer for supported devices and switch them to HCI mode.

When a device is plugged in, if it is a supported device, the service will switch it to HCI mode.

At system shutdown/restart (service stop) it will convert all supported devices back to HID mode. I added this to make the keyboard/mouse work in BIOS after a hot reboot, when the dongle is not reinitialized.

# What it doesn’t do #
It will not try to automatically pair the keyboard/mouse with your computer like the original LBTServ.exe does, so you will need at least another mouse to do this (this is required once, for the pairing process).

# Supported Devices #
  * [Cordless Desktop MX 5000 Laser](http://www.logitech.com/index.cfm/433/162&hub=1&cl=us,en)
  * [diNovo Mini](http://www.logitech.com/index.cfm/keyboards/keyboard/devices/3848&cl=us,en)
  * diNovo Media Desktop Laser
  * diNovo Edge
  * MX900 Bluetooth Cordless Optical Mouse

If your device is not listed above, but lhid2hci is able to convert your dongle, install the service, open regedit, go to HKEY\_LOCAL\_MACHINE\SOFTWARE\CSa\LBTService and add a value corresponding to your device. The format of the value should be: Value Name – the name of the product, Value – the arguments passed to lhid2hci. [Restart the service.](http://technet.microsoft.com/en-us/library/cc736564%28WS.10%29.aspx) If it works please file a bug report to add the device in the installer.

# Installing WIDCOMM Bluetooth stack #
For some dongles you can install the WIDCOMM Bluetooth using the online installer from [here](http://www.broadcom.com/support/bluetooth/update.php)

For others, notably diNovo Mini, the above mentioned installer will say that it can not install the software for some reason and you should contact the manufacturer. To get around this install the software from an OEM which supplies the stack for their laptops. For Windows 7 I used [this](http://drivers.softpedia.com/get/Other-DRIVERS-TOOLS/Others/Acer-TravelMate-4730-Notebook-Broadcom-Bluetooth-Driver-621500-for-Win7.shtml) version and it works like a charm.

# Supported Platforms #
It has been tested on Windows XP SP3 and Windows 7 (32 bit & 64 bit), but it should also work on Windows 2000 and Vista.


# Thanks #
  * To [Nynaeve](http://www.nynaeve.net/?p=5) for his excellent porting of lhid2hci from Linux to Windows.
  * To [Bluez Team](http://www.bluez.org/)