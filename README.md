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
sudo mkdir /mnt/ubuntu
sudo mount <root_device> /mnt/ubuntu # mounts root partition
sudo mkdir -p /mnt/ubuntu/boot/efi
sudo mount <efi_device> /mnt/ubuntu/boot/efi # mounts efi - if applicable

# Mounts necessary directories
sudo mount --bind /dev /mnt/ubuntu/dev
sudo mount --bind /proc /mnt/ubuntu/proc
sudo mount --bind /sys /mnt/ubuntu/sys
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
sudo umount /mnt/ubuntu/sys
sudo umount /mnt/ubuntu/proc
sudo umount /mnt/ubuntu/dev
sudo umount /mnt/ubuntu/boot/efi
sudo umount /mnt/ubuntu
sudo systemctl poweroff
```
