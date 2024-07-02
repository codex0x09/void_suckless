## 1- First Boot your Live Void Linux (glibc)

1. Use `Ventoy` to access the `ISO` image, instead of burn the `ISO`.

2. Plug your USB (that contents Live Void Linux image) in your machine to boot with.

- If you don't have one yet, here it is [Live Void Linux (glibc)]() ,
or just visit the [Void Linux]() and choose what you need .

## 2- The bootloader
Select the first option: -> `Void Linux -version- x86_64`

## 3- Login and fire the installer

1. Login as root: `username=root, password=voidlinux`
```
void-live login: root
pasword: voidlinux
```

2. To start the installation fire:
```
void-installer
```

3. And follow the on-screen instruction:
- After configuring the network you can use the following commands to install additional software
```
xbps-install   # to install/update packages
xbps-query     # to query for package info
```
>[!TIP]
> But really how to use this instructions after you issue `void-installer`?!  
> Well, if you don't have additional laptop/PC, just hit `Ctrl + Alt + F2` or `F3` to open new `tty` terminal,  
> now you can hack things, download `git` or a browser like `links` or my best browser `w3m`, that uses `vi` keys.  
> So far so good, now you can back to the `void-installer` by hitting `Ctrl + Alt + F1`,
> and keep switching between the `void-installer` and your `tty` to follow the instructions.

## 4- Partitioning Notes
Whatever your firmware is BIOS or UEFI use a GPT partition table,
because BIOS can deal with both GPT and MBR while UEFI can only work with GPT

## 5- Installation Wizard

1. First of all login as root `username=root, password=voidlinux` and fire the installer `void-installer`
```
void-live login:root
pasword:voidlinux

void-installer
```

2. Set your system keyboard:
- for me `us` what about you ?

3. Set up the network:

4. Set source installation, here you have two options:
- go with the first option `Local packages from ISO image`, after all you going to upgrade Right!?.

5. Mirror to select XBPS mirror:
- select the default mirror `repo-default.voidlinux.org` which can point to any Tier 1.
>[!NOTE]
> Tier 1 mirrors are maintained by the Void Linux Infrastructure Team and will always have the latest packages available!.  
> Tier 2 mirrors are not managed by Void, so they not always fresh and up-to-date,  
> but they may work, however the mirrors list in `/etc/xbps.d/`.

6. Hostname:
- for me of course `void` and you ?

7. Locale:
- for me `en_US.UTF-8`, what about you bro ?

8. Timezone: set system time zone
- for me `Africa` and live in `not found my country (>^.^<)` it's Ok

9. RootPassword: set system root password
- mine is `use strong and complicated password` and don't forget it !!

10. UserAccount: set primary user name and password
- Enter a primary login name: `codex`
- Enter a display name for login: `codex`
- Enter the password for login 'codex': `use strong and complicated password` and don't forget it !!
- Enter the password for login 'codex' again: `your strong and complicated password`
- Select group membership for login 'codex':
    *  [x] wheel:4 -> make sure `wheel` is checked, it allows you to user `sudo`
    *  [ ] floppy:8 -> I don't need this
    *  [x] audio:12
    *  [x] video:13
    *  [ ] cdrom:16 -> I don't need this too 
    * leave the reset as they are, or do what you want !!

11. BootLoader: Set disk to install `bootloader`
- Select the disk to install the bootloader
    * `/dev/sda` ; select your right disk.
        * `use a graphical terminal for the boot loader?` yes

12. Partition: Partition disk(s)
- select your disk and choose a tool to work with cfdisk (super easy) or fdisk (nice one)
>[!NOTE]
> If your host(PC/Laptop/VM/etc.) has BIOS or in Legacy BIOS mode, and
> you want to use GPT Partitioning table which is, that used in UEFI, then you need to do the following:
> 1. Create at the beginning of the disk `1M` of type `BIOS boot`,
> and don't touch it in the next section `13.FileSystems`
> 2. If you don't want to use `Zram`, then create `swap` partition  of size `1G` up-to `4G`,
> it's should be double of your `RAM` size, but `4G` is enough and try using `Zram` it's the best.
> 3. Finally if you have an other disk for `home` or not use the entire free space of type `Linux filesystem` for the root `/` 
> or do what you want !!.
> If you use `cfdick` then hit `write` and type `yes` and hit `quit`

13. FileSystems: Configure filesystemes and mount points
- If you follow the above instructions then you'll end with something like this:  
    \---------------------------------------  
    `/dev/sda1 Size:1M;fstype:none`  
    `/dev/sda2 Size:2G;fstype:none`  
    `/dev/sda3 Size:90G;fstype:none`   
    \---------------------------------------  
- Let's formatting and mouting the partitions: 
  * `/dev/sda1 Size:1M;fstype:none`
      + Leave it and let the system do the job, or modify it as you wish. 
  * `/dev/sda2 Size:2G;fstype:none`
      + `<change>` to `swap  Linux swap`  hit `<yse>`
  * `/dev/sda3 Size:90G;fstype:none`
      + `<change>` to `ext4  Linux ext4 (journal)` hit `<Ok>` and type `/` for mounting point, and hit `<Ok>`  
      if you have an other disk for `home`, then you can mount it here as `/home`. 

14. Install: Start installation with saved settings
- Hit `<Ok>` and hit `Yes` of course. That's it, now you have `Void Linux` installed `(>^.^<)`.
