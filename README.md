# NessVMS_OS Install
Working files and tools for creating an unattended Ubuntu LTS Install. You will need to be running linux on your machine or a VM to create the bootable disk, the commands below will guide you. 

MAKE SURE YOU HAVE ATLEAST 20gb SPACE AVAILABLE ON YOUR SYSTEM HDD

# Warning
Although these scripts are public facing, they are not intended for general consumption. Do not blindly run these scrips, they are unsupported. You WILL NOT receive technical support if you run these without direction.

This will create a bootable linux usb install disk that will wipe any computer that boots it automatically, don't leave it in a machine you don't want to wipe. 

## Linux Basics
 - Whenever you see `~` this means your *Home* directory
 - You can paste in to the terminal using Middle Click or Clicking the Mouse wheel

## Download Cubic Tool and Git to create the ISO
Download some tools to get your environment ready
```
sudo apt-add-repository ppa:cubic-wizard/release
sudo apt update
sudo apt install cubic git
```

## Make sure your local OS is up to date
```
sudo apt upgrade -y
```

## Download Ubuntu
Go to http://releases.ubuntu.com/ and Select the Ubuntu 18.04.6 LTS Desktop Image, save/download it to ~/Downloads

## Download necessary boot files to automate installation
There are 4 modified files that are required:
 - /boot/grub/grub.cfg
 - /boot/grub/looback.cfg
 - /isolinux/txt.cfg
 - /preseed/nessvms.seed

Clone this Git Repository to download these files
```
cd
mkdir -p ~/git
cd git
git clone https://github.com/nesscs/NessVMS_OS.git
```

Create a working Directory
```
sudo mkdir -p ~/cubic_ubuntu
```

## Run Cubic
Launch Cubic from the dock or application menu.

Select the working directory as ~/cubic_ubuntu

<img src="readme_images/cubic01.png" width="70%" >
<img src="readme_images/cubic02.png" width="70%" >

## Select the Ubuntu LTS iso you just downloaded
<img src="readme_images/cubic03.png" width="70%" >
<img src="readme_images/cubic04.png" width="70%" >

## Customise the release as you wish and press next
<img src="readme_images/cubic05.png" width="70%" >

## Skip past the terminal modification screen
<img src="readme_images/cubic06.png" width="70%" >

## Add the preseed file
These steps are *critical* that you compelte correctly. 
Add a new preseed file and call it `nessvms.seed`
Now open up the file manager and navigate to `~/git/NessVMS_OS/preseed`
Open the nessvms.seed file and copy and paste the contents back in to cubic in to the new entry you have created.

<img src="readme_images/cubic07.png" width="70%" >
<img src="readme_images/cubic08.png" width="70%" >

## Edit Boot configuration files
Similarly we must overwrite the 3 existing boot config files contents with the contents of the files below that we downloaded
```
home/git/NessVMS_OS/boot/grub.cfg
home/git/NessVMS_OS/boot/loopback.cfg
home/git/NessVMS_OS/isolinux/txt.cfg
```
Open each file with the file manager and completely overwrite and replace all the text in the existing files with the text from the git folder files by Copy/Pasting

<img src="readme_images/cubic09.png" width="70%" >

Once you have done that you can click Generate

## Generate USB ISO
The new OS Image ISO will now be generated and placed inside home/cubic_ubuntu

<img src="readme_images/cubic10.png" width="70%" >

Once complete you may choose to delete the working files

<img src="readme_images/cubic11.png" width="70%" >


## Write USB ISO To USB Stick
Now that the ISO is created, open the file manager, navigate to home/cubic_ubuntu
Right click on the new image file and Open with Disk Image Writer

<img src="readme_images/cubic12.png" width="70%" >

Write the file to a blank USB Stick that is larger than 4gb

<img src="readme_images/cubic13.png" width="70%" >
<img src="readme_images/cubic14.png" width="70%" >


Congratulations, You're done.
Try the disk out on a new machine. REMEMBER this disk will wipe the contents of any machine you commence the install on.

#### Support
There is no support! Contact Kieran for changes.

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

