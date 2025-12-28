# Ubuntu

Useful information about ubuntu config and utilities.

Download this documentation: `$ curl -LO https://raw.githubusercontent.com/vncsmyrnk/ubuntu/refs/heads/main/README.md`

## apt repos

- [launchpad](https://launchpad.net/)

```sh
sudo apt-add-repository ppa:launchpad/ubuntu/ppa
```

## Chroot

Useful for manually mounting the system and check for broken packages and repair them. Can be useful for linux distros in general.

### Locate the devices

- Check for available devices: `$ lsblk`
- Check for partitions: `$ sudo fdisk -l /dev/<device>` (can be `/dev/nvme0n1`, `/dev/sda`)

### Mount the partitions

```sh
mkdir /mnt/ubuntu
mount <root_device> /mnt/ubuntu # mounts root partition
mount --mkdir <efi_device> /mnt/ubuntu/boot

# Mounts necessary directories
mount --bind /dev /mnt/ubuntu/dev
mount --bind /proc /mnt/ubuntu/proc
mount --bind /sys /mnt/ubuntu/sys
```

### Chroot into it

```sh
sudo chroot /mnt/ubuntu
```

### (useful) Check broken packages

```sh
apt update
apt upgrade
apt install -f
dpkg --configure -a
```

### Unmount everything and reboot

```sh
umount /mnt/ubuntu/sys
umount /mnt/ubuntu/proc
umount /mnt/ubuntu/dev
umount /mnt/ubuntu/boot/efi
umount /mnt/ubuntu
systemctl poweroff
```
