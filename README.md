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

After reboot a new entry called "btrfs snapshots" in GRUB2 boot menu should appear. By selecting one of those snapshots you should be able to boot from it.

### Install NVIDIA - PRIME capable drivers
When using Neon (or Ubuntu), the installation is fairly simple.
In console use command `ubuntu-drivers list`. 
Check if the latest NVIDIA driver is listed. 
If yes, you can proceed by running `sudo ubuntu-drivers autoinstall` - the latest drivers will be installed automatically with their dependencies.

If the latest driver is not listed, try adding nvidia ppa: `sudo add-apt-repository ppa:graphics-drivers/ppa`.

After installation is complete, reboot your PC.

**IMPORTANT!! - This section is related to optimus-enabled laptops. If you're on desktop, or have only iGPU you can safely skip the next few lines.**

When booted, open **NVIDIA X server settings**, or run `sudo nvidia-settings`.

Open the **PRIME Profiles** tab - it should look like this:

![PRIME configuration](/img/NVIDIA-config.png)

Try all these profiles with secondary display.
Before making any changes I recommend creating a snapshot in case anything breaks. 
If everything works fine, you're done here.
