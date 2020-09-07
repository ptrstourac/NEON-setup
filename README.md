# NEON setup
Repo containing guide and configs for my KDE Neon setup.

## System installation
Install system from live setup in normal way.

### Partitioning
Install whole system on **one** partition - subvolumes /@ and /@home will be created automaticcaly. I recommend using `btrfs` filesystem for snapshot creation capability.

Don't forget to mount system EFI partition as `/boot/efi`. **Don't format it!**

## Post installation 

### Setup timeshift
Use `sudo apt install timeshift` to install timeshift package. Then open timeshift and configure it as stated lower.
1. Select **BTRFS**
2. Make sure, that your partition with /@ and /@home subvolumes are selected
3. Config how often should be snaps created and how old will be kept
4. Select "Include /@home subvolume in backup" 
5. Create first snapshot and reboot.

### Install grub-btrfs package (for snapshot-boot capability)
Install **git** and **make** packages via `sudo apt install git make`.
Then clone **grub-btrfs repository** with `git clone https://github.com/Antynea/grub-btrfs`.
CD into its folder (`cd ~/grub-btrfs/`) and run `sudo make install`. 
Config can be customized in `/etc/default/grub-btrfs/config` (more on the repos URL).

**IMPORTANT!** - don't forget to run `sudo update-grub`, or you won't be able to boot next time.