# Edit (Repack) existing ISO in LINUX (using mkisofs) :



### Install the require packages :

- Installing mkisofs :
```
sudo apt-get install mkisofs
```

- Install isohybrid :
```
sudo apt install syslinux-utils
```

### Editing ISO image

```
mkdir /tmp/custom_iso

cd /tmp/custom_iso/

mount -t iso9660 -o loop ~/original.iso /mnt/

cd /mnt
```
"mnt" is read-only, thus we need to copy the files in it in order to modify the files.
```
tar cf - . | (cd /tmp/custom_iso; tar xfp -)
```

You can now modify the files. For example - making a preseed file!


### Repack the new changed ISO (xxxx.iso):
If not, go back to your /tmp/custom_iso folder

```
cd /tmp/custom_iso
```

Copy this line, modify it and paste it in order to create the .iso

```
mkisofs -o output.iso -b isolinux.bin -c boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -J -R -V "Ubuntu Custom ISO Preseed" .
```

### Make this ISO bootable with isohybrid
```
sudo isohybrid output.iso
```