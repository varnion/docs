# How to "burn" a iso in a USB stick

## Identify the sd\* code assigned to the stick
~~~
sudo fdisk -l
# or 
lsblk
~~~ 

We will assume the device is /dev/sdb. Replace it accordingly in the next commands.

## Unmount the stick
~~~
umount /dev/sdb*
~~~

## Format the stick
~~~

mkfs.vfat /dev/sdb -I

~~~

## Optional: Validate the iso MD5 checksum

Assuming you also downloaded a txt file (`MD5SUMS`) with the checksums, run:
~~~

$ md5sum -c MD5SUMS 2> /dev/null  | grep OK
debian-live-8.8.0-amd64-gnome-desktop+nonfree.iso: OK
debian-live-8.8.0-amd64-standard+nonfree.iso: OK  


~~~

In our example we will use the debian-gnome iso.

## Generate the bootable stick with DD

Simple usage:

~~~

sudo dd if=debian-live-8.8.0-amd64-gnome-desktop+nonfree.iso of=/dev/sdb bs=4096 \
    status=progress

~~~

The status parameter is optional and is only available in `GNU coreutils` 8.24+.


## Sources

- [How to create bootable USB drive using dd command](https://www.ostechnix.com/how-to-create-bootable-usb-drive-using-dd-command/)
- [AskUbuntu: How to check dd progress](https://askubuntu.com/a/215590)
