# NxVMS_OS Install
Working files and tools for creating an unattended Ubuntu LTS Install. You will need the latest LTS Image from Ubuntu

## Mount the ISO File
You will need to mount the ISO files so that you can edit the pertinent files. Substitute the file names for relevant files
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

Clone the Git Repository to download these files
```
sudo apt install git
cd
mkdir -p ~/git
cd git
git clone https://github.com/kvellaNess/NxVMS_OS.git
```

Copy the modified files to the working directory
```
cp ~/git/NxVMS_OS/boot/grub/grub.cfg ~/preseed_ubuntu/boot/grub/grug.cfg
cp ~/git/NxVMS_OS/isolinux/txt.cfg ~/preseed_ubuntu/isolinux/txt.cfg
cp ~/git/NxVMS_OS/preseed/nessvms.seed ~/preseed_ubuntu/preseed/nessvms.seed
```

## Get tools to make the USB Disk
```
cd
sudo apt install mtools syslinux wimtools -y
wget https://git.io/bootiso
chmod +x bootiso
sudo mv bootiso /usr/local/sbin/
sudo apt install mtools syslinux
```
## Create new iso file
```
sudo mkisofs -D -r -V "UNATTENDED_UBUNTU" -cache-inodes -J -l -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -o ~/ubuntu16-unattended-install.iso ~/preseed_ubuntu
```
## Burning the iso file to USB
```
sudo bootiso NessVMS-Unattended.iso
```

Congratulations, You're done.
Now, test the iso file on a virtual machine.

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

