# Repack bootable ISO
[![License](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://opensource.org/licenses/GPL-3.0)
[![PR's Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com) 

Perl script for editing and repacking any ISO file into a bootable image. Script authored by Intel Corporation. Modified and redistributed by Swattle to accustom repacking of the latest images. 

## On Linux

### Installing mkisofs

`apt-get install mkisofs`

### Editing ISO image

`mkdir /tmp/custom_iso`

`cd /tmp/custom_iso/`

`mount -t iso9660 -o loop ~/original.iso /mnt/`

`cd /mnt`

mnt is read-only, thus we need to copy the files in it in order to modify the files.

`tar cf - . | (cd /tmp/custom_iso; tar xfp -)`

You can now modify the files for making a preseed for example!

### Back in .iso

If not, go back to your /tmp/custom_iso folder

`cd /tmp/custom_iso`

Copy this line, modify it and paste it in order to create the .iso

`mkisofs -o output.iso -b isolinux.bin -c boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -J -R -V "Custom ISO Preseed" .`

### Make it bootable with isohybrid

Install isohybrid:

`sudo apt install syslinux-utils`

Then simply type the following to make it bootable:

`sudo isohybrid output.iso`

## On macOS

### Install brew 

Follow https://brew.sh/

### Install requirements

In order to install mkisofs, you need to get the cdrtools package for macOS:

`brew install cdrtools`

### Prepare folders

Make two folders: iso and custom.

`ro_iso` is going to be where the files of the iso will be mounted, read only.

`custom` will be where you will be able to modify the files

`mkdir ro_iso && mkdir custom`

### Attaching, mounting and editing

`hdiutil attach -nomount ubuntu.iso`

List the disks and get the disk image name usually `/dev/disk2`:

`diskutil list`

We will use `/dev/disk2`.

Now you can mount the disk into the read-only folder:

`mount -t cd9660 /dev/disk2 ro_iso`

We now need to copy the files in the `custom` folder in order to modify the files:

`tar cf - . | (cd $HOME/yourfolder/custom; tar xfp -)`

You can now begin editing the files.

### Back in .iso

If not yet, go back to your `custom` folder.

Copy this line, modify it and paste it in order to create the .iso

`sudo mkisofs -o output.iso -b isolinux.bin -c boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -J -R -V "Custom ISO Preseed" .`

### Make it bootable with isohybrid

Use the `isohybrid.pl` file of this repo like the following:

`sudo perl isohybrid.pl output.iso`

### umount and detach

Don't forget to do it, or you will can't be able to delete the `ro_iso` folder

`umount /dev/disk2`

`hdiutil detach /dev/disk2`

You now have a bootable USB iso file :)

## License
This project is licensed under the GNU General Public License v3.0. Permissions of this strong copyleft license are conditioned on making available complete source code of licensed works and modifications, which include larger works using a licensed work, under the same license. Copyright and license notices must be preserved. Contributors provide an express grant of patent rights. Any material found which vandalises or threatens any sort of plagiarism will be strictly given a legal action.

 <p align="center"> Copyright (c) 2020 Swattle Inc. All rights reserved.</p>

## Contributing
- Fork this project by clicking the ```Fork``` button on top right corner of this page.
- Open terminal/console window. 
- Clone the repository by running following command in git:
 ```bash
$ git clone https://github.com/[YOUR-USERNAME]/repack-bootable-iso.git
```
- Add all changes by running this command.
```bash
$ git add .
```
- Or to add specific files only, run this command.
```bash
$ git add path/to/your/file
```
- Commit changes by running these commands.
```bash
$ git commit -m "DESCRIBE YOUR CHANGES HERE"

$ git push origin
```
- Create a Pull Request by clicking the ```New pull request``` button on your repository page.

[![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://GitHub.com/swattle/) 
[![ForTheBadge powered-by-electricity](http://ForTheBadge.com/images/badges/powered-by-electricity.svg)](http://ForTheBadge.com)

<p align="center"> Copyright (c) 2020 Swattle Inc. All rights reserved.</p>
<p align="center"> Made with ❤ by <a href="https://github.com/swattle">Swattle</a></p>
