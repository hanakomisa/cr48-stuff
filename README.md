# cr48-stuff
I'm using this mostly to host files relating to the Cr-48.

# How to flash from stock to InsydeH2O
You will need to have the BIOS write pads physically isolated on the board. (TODO: add image.)

Once you've done that, toggle the switch to Developer Mode, it's inside the battery bay and hidden by a black sticker.

After that is toggled, your Cr-48 will show a splash screen, just wait, the machine will long beep twice, then load into ChromeOS.
(There is another way to skip the splash by a certain key combination, but I don't remember which. I'll add it if I find it again.)

First time the ChromeOS will be wiped switching to developer mode, this will take around 5 minutes, just let it do its thing. Then it will reboot,
splash screen, double beep, yada yada.

Once that's done, get to the setup screen and connect to Wi-Fi. Once you've done that press `Ctrl`+`Alt`+`F2`/(Forward button) to drop into a Dev console.

From here, login as `chronos`, there is no password by default. From there, escalate your privileges by doing `sudo su`, then backup the original BIOS and flash the InsydeH2O BIOS.

I'd recommend setting up a mount point with a USB drive, I did that by first finding where the USB drive is located with `fdisk -l`, and then `mkdir /tmp/mnt && mount /dev/sdXX /tmp/mnt`.

To back up the original BIOS, do `flashrom -r <backup name>.bin` and copy it somewhere safe (like the previously mounted USB drive). Once that's done, go to the next step.

Then you'd want to download the bios by doing `wget https://github.com/hanakomisa/cr48-stuff/raw/main/cr48.bin` flash your BIOS by doing `flashrom -w cr48.bin`
    Alternatively, just copy it to the USB drive beforehand and skip the `wget` step.

Once it's done (ignore any SPI errors), reboot and your Cr-48 should behave like a normal Netbook now. If not, then your flashing process may have went wrong.
    In this case, you'd likely have to do a physical BIOS flash, it's another can of worms I won't be touching at least right now.

# How to flash back to stock from InsydeH2O
TODO: add this. but a TLDR is get a Linux livecd, install flashrom, then flash the backup BIOS. `flashrom -w` alone may not work and might require additional arguments, I believe it was INTERNAL something.
