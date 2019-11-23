# Linux

## debian base

* update: `sudo apt update & sudo apt upgrade`

## red hat - RHEL

* update: `sudo yum update`
* update: `sudo dnf upgrade`

## arch base

* update: `sudo pacman -Syu`

## Compress

```sh
tar -cvzf jpegarchive.tar.gz /path/to/images/*.jpg
```

```sh
tar -xvf filename.tar
```

## Make Bootable Disk

```sh
sudo dd bs=4M if="/home/mohsen/linux-image.iso of=/dev/sdb1" status=progress oflag=sync
```

