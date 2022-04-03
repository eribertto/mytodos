# fix grub fedora 36 botched upgrade process
# using chroot per this guide 350 - Fix Your Broken Linux with chroot
# https://www.youtube.com/watch?v=D8DsR1P7cbQ

# some guides
# https://docs.fedoraproject.org/en-US/Fedora/22/html/Multiboot_Guide/common_operations_appendix.html
# https://docs.fedoraproject.org/en-US/fedora/f35/system-administrators-guide/kernel-module-driver-configuration/Working_with_the_GRUB_2_Boot_Loader/#sec-Terminal_Menu_Editing_During_Boot


take note of the reply in subreddit r/Fedora
You just need to re-run sudo grub-mkconfig -o /boot/grub/grub.cfg after you've mounted and chrooted back into the system. Note: /boot/ is wherever your boot partition is mounted. It may not be the same directory.

The Arch wiki has an article describing the basic process. Just remember to use chroot instead of arch-chroot.
https://wiki.archlinux.org/title/chroot

boot to live usb
check/browse the existing FS / device drive
ensure you are in the right folder when exec commands
note the boot folder of the existing fedora 
use fdisk to verify the correct drives, also see in grub UI

#commands, this is live user home folder
cd /mnt
sudo mkdir -p mydrive/boot
# find the right device drive of the botched OS before mounting
# in my case this is /dev/sda3
# λ mount | grep local
/dev/sda3 on /run/media/eribertt/fedora_localhost-live type btrfs (rw,nosuid,nodev,relatime,ssd,space_cache=v2,subvolid=5,subvol=/,uhelper=udisks2)

# note you are in /mnt drive
sudo mount /dev/sda3 /mydrive
# do an ls of the mounted drive to view the folders under /dev/sda3
ls mydrive
sudo mount -t proc none /mnt/mydrive/proc
# do an ls of the mounted proc folder
ls /mnt/mydrive/proc
sudo mount -o bind /dev /mnt/mydrive/dev
sudo mount -o bind /run /mnt/mydrive/run
# the moment of truth
# shows you the folders of the botched OS
ls mydrive/

# now the chroot command (this will make you root signaled by the prompt)
sudo chroot /mnt/mydrive /bin/bash
cd /mnt
ls # will show none??
cd /boot
ls # shows you the content of the folder
cd /home
ls # shows you the home folder of the user in fedora
# optional
# run update of system (but might have no internet so need to try this out)

# see this comment from reddit sub r/Fedora

You just need to re-run sudo grub-mkconfig -o /boot/grub/grub.cfg after you've mounted and chrooted back into the system. Note: /boot/ is wherever your boot partition is mounted. It may not be the same directory.

## note this alternative solution subject to edit to suite your conditions
## good link to tweak to my needs
## https://gist.github.com/Tamal/73e65bfb0e883e438310c5fe81c5de14

# Use Live CD to boot
$ sudo su # Switch to root
$ fdisk -l # Get names of root, boot & EFI partition names. you can also use blkid
$ mount /dev/mapper/fedora_localhost--live-root /mnt  # mount root partition
$ cat /mnt/etc/fedora-release
Fedora release 31 (Thirty One)
$ mount /dev/nvme0n1p2 /mnt/boot  # mount boot partition
$ mount /dev/nvme0n1p1 /mnt/boot/efi  # mount EFI partition
# Note: If you are not able to mount EFI partition ('Input/Output error'),
# You may have to repair ESP file system or format ESP.
# fsck.vfat /dev/nvme0n1p1
# mkfs.vfat /dev/nvme0n1p1 
# If formatted then we may have to update UUID at /etc/fstab
$ ls /mnt/boot/efi # should show all OS names under EFI

$ # mount the virtual filesystems that the system uses to communicate with processes and devices
$ for dir in /dev /proc /sys /run; do mount --bind $dir /mnt/$dir ; done

$ # enter chroot
$ chroot /mnt

$ # Now you can do all the work e.g. fix grub
$ dnf reinstall grub2-efi shim -y
$ grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg # Regenerate grub2

$ exit

$ # Check BIOS boot details
$ efibootmgr -v
$ # In case you need to create new entry in BIOS
$ efibootmgr -c -d /dev/nvme0n1p1 -p 1 -L Fedora -l '\EFI\fedora\grubx64.efi' # or, shimx64.efi
$ # Copy grubx64.efi from Live USB, if required
$ cp -p /boot/efi/EFI/grubx64.efi /mnt/boot/efi/EFI/fedora

# Check /etc/fstab UUID, update if necessary

$ # All things done; now exit from chroot
$ exit
$ # Now you can reboot


# another useful link
# https://tutorialforlinux.com/2021/09/28/step-by-step-chroot-fedora-35-easy-guide/

# become root
sudo su # or su -
# find the mounted partitions
df -h # or use gparted or lsblk and grep the target partition
# unmount it
umount /dev/sda3

# mount the new root target
mkdir /mnt/newroot
mount /dev/sda3 /mnt/newroot

# mounting pseudoterminal slave (what???)
if [!d "/mnt/newroot/dev/pts"]; then mkdir /mnt/newroot/dev/pts; fi

# mount it
mount -t devpts none /mnt/newroot/dev/pts # something is wrong here

# mount the proc
mount --bind /proc /mnt/newroot/proc
# binding means cloning the actual directories in a different point

# bind the devices dir
mount --bind /dev/ /mnt/newroot/dev

# bind the sysfs virtual FS
mount --bind /sys /mnt/newroot/sys

# bind the temp
mount --bind /tmp /mnt/newroot/tmp

# enable networking
# in case you're prompted then confirm to overwrite the existing one
cp /run/systemd/resolve/stub-resolv.conf /mnt/newroot/etc/resolv.conf

# perform chroot
chroot /mnt/newroot /bin/bash

# check your actual location
pwd # should give you in the new root folder /

# ping the network
ping -c3 google.com

# now do your chroot thing
