# Edit (Repack) existing ISO in LINUX :

## on linux (for UEFI)

### Install the require packages :

- Installing mkisofs :
```
sudo apt-get install mkisofs
```

- Installing xorriso :
```
apt-get install xorriso
```

- Install isohybrid :
```
sudo apt install syslinux-utils
```

### extract ISO image to a particular directory

```
mkdir -p ~/custom-iso/iso
cd ~/custom-iso
```

### copy original ISO to this directory
```
cp PATH/original-linux-install.iso ~/custom-iso
```

### Extract the original ISO to ~/custom-iso/iso
```
cd ~/custom-iso
```
```
xorriso -osirrox on -indev original-linux-install.iso -extract / iso
```

### Do the require changes :
```
cd ~/custom-iso/iso
<do the changes>
```

### Repack the new changed ISO (xxxx.iso):
```
cd ~/custom-iso/iso
```
```
sudo xorriso -as mkisofs -isohybrid-mbr isolinux/isolinux.bin -c isolinux/boot.cat -b isolinux/isolinux.bin -no-emul-boot -boot-load-size 4 -boot-info-table -eltorito-alt-boot -e boot/grub/efi.img -no-emul-boot -isohybrid-gpt-basdat -o ../custom-iso.iso .
```

### or

```
sudo xorriso -as mkisofs -graft-points -isohybrid-mbr isolinux/isolinux.bin -c isolinux/boot.cat -b isolinux/isolinux.bin -r -J -no-emul-boot -boot-load-size 4 -boot-info-table -eltorito-alt-boot -e boot/grub/efi.img -no-emul-boot -isohybrid-gpt-basdat -o ../custom.iso .
```

### Make this ISO bootable with isohybrid
```
sudo isohybrid ~/custom-iso/custom.iso
```