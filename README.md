# NxVMS_OS Install
Working files and tools for creating an unattended Ubuntu LTS Install. You will need to be running linux on your machine or a VM to create the bootable disk, the commands below will guide you.

# Warning
This will create a bootable linux usb install disk that will wipe any computer that boots it automatically, don't leave it in a machine you don't want to wipe.

## Download Dependencies
Download some tools to get your environment ready
```
sudo apt install git mtools syslinux wimtools -y
```

## Download Ubuntu
Go to http://releases.ubuntu.com/ and Select the latest LTS Desktop Image, download it to ~/Downloads

## Mount the ISO File
You will need to mount the ISO file so that you can edit the pertinent files. Substitute the file names for relevant files
```
mkdir -p /mnt/iso
mount -o loop ~/Downloads/ubuntu-18.04.3-desktop-amd64.iso /mnt/iso
```
## Copy the Files
Now you need to copy the mounted files so that you can edit it. Do it by:
```
mkdir -p ~/preseed_ubuntu
cp -rT /mnt/iso ~/preseed_ubuntu
````
## Make the files editable 
We can do that by using `chmod`:
```
sudo chmod -R ~/preseed_ubuntu
```

## Add in necessary Edited files
There are 3 modified files that are required:
/boot/grub/grub.cfg
/isolinux/txt.cfg
/preseed/nessvms.seed

Clone this Git Repository to download these files
```
cd
mkdir -p ~/git
cd git
git clone https://github.com/kvellaNess/NxVMS_OS.git
```

Copy the modified files to the working directory
```
cp ~/git/NxVMS_OS/boot/grub/grub.cfg ~/preseed_ubuntu/boot/grub/grub.cfg -r
cp ~/git/NxVMS_OS/isolinux/txt.cfg ~/preseed_ubuntu/isolinux/txt.cfg -r
cp ~/git/NxVMS_OS/preseed/nessvms.seed ~/preseed_ubuntu/preseed/nessvms.seed -r
```

## Set up tool to make the USB Disk
```
cd
wget https://git.io/bootiso
chmod +x bootiso
sudo mv bootiso /usr/local/sbin/
```

## Create new iso file
```
sudo mkisofs -D -r -V "NessVMS_OS" -cache-inodes -J -l -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -o ~/NessVMS-Unattended.iso ~/preseed_ubuntu
```

## Burn the iso file to USB
Insert a USB Stick in to the machine follow the prompts to write the ISO to it.
```
sudo bootiso NessVMS-Unattended.iso
```

Congratulations, You're done.
Try the disk out on a new machine.

#### Bug or suggestion?
Feel free to report any problem :)
Contact Kieran for changes.

## License
MIT License

Copyright (c) 2019 Ness Corporation

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

