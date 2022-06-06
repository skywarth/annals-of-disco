### If at any point you mess up big time (like completely removing network manager and drivers)
- Restart
- Before booting into ubuntu start pressing shift (or escape if UEFI)
- This will bring up the GRUB
- Go to advanced and select the older/oldest kernel
- It should boot just fine in a mostly working state
- `sudo apt-get update`
- `sudo apt-get dist-upgrade`
- `sudo apt-get install --reinstall linux-image-extra-virtual`
- `sudo ubuntu-drivers autoinstall`
