---
title: Hello world
date: 2021-06-09 13:46:29
---

# Linux file types

## `-` regular file

A regular file begins with `-`. For example we can list a regular file to see its file type symbol.

```
$ ls -l /etc/centos-release
-rw-r--r--. 1 root root 37 Nov 23  2020 /etc/centos-release
```


## `d` directory

A directory begins with `d`. For example we can list the current directory to see its file type.

```
$ ls -ld .
drwxr-xr-x  7 root  root  224 Jun  4 06:24 .
```

## `c` character device

A character device accepts character input and display characters, e.g. a terminal. We can list a terminal to see its file type.

```
# Show terminal that we are connecting to
$ tty 
/dev/ttys002
# see its file type
$ ls -l /dev/ttys002
crw--w----  1 quynhanhpham  tty   16,   2 Jun  5 05:44 /dev/ttys002
```

We can see that the file type of the terminal is `c`.

## `b` block device

Let's check disk and partition of the system.

```
$ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   20G  0 disk 
├─sda1   8:1    0  200M  0 part /boot/efi
└─sda2   8:2    0 19.8G  0 part /

```

We can see that we have `sda` as disk, `sda1` and `sda2` as partitions.

These are managed as files in the system. We can check the file type.

```
$ ls -la /dev/sda*
brw-rw----. 1 root disk 8, 0 Jun  4 21:01 /dev/sda
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```

The file type is `b`, so they are block devices.

## `l` symbolic link

A symbolic link is like a shortcut to another file. Let's check the following symbolic links.

```
$ ls -l /etc/system-release /etc/redhat-release
lrwxrwxrwx. 1 root root 14 May 11 20:55 /etc/redhat-release -> centos-release
lrwxrwxrwx. 1 root root 14 May 11 20:55 /etc/system-release -> centos-release
```

We can see that we have these 2 files with `l` character at the beginning, and they are both pointing to `centos-release`. They are symbolic links, shortcuts to `/etc/centos-release`.
