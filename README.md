# macOS VirtualBox VM

This is a preconfigured macOS VirtualBox Virtual Machine, along with a script for preparing a bootable install ISO image from a downloaded Mac OS installer app.

*Note: The `create_install_iso.sh` script is tailored to macOS hosts, and the macOS High Sierra installer app. The script will will need to be modified to work with the installer app for other versions of macOS.*

## Usage

1. Download the macOS installer app if you have not already. It should be located in your `Applications` directory.
2. Clone this repo to your machine.
3. Run `create_install_iso.sh`, which will create a file named "HighSierra.iso" on your desktop, based on the downloaded macOS installer app.
4. Open the VirtualBox GUI, open the virtual machine from the repo, create a new virtual hard disk, and set the `HighSierra.iso` image as a disk in the VM's optical drive.
5. Start the VM, wait for the macOS installer to boot.
6. Open Disk Utility, from the File menu enable the option to "Show all devices", and erase the VirtualBox hard disk image.
7. Install macOS.
8. When the installer completes, reboot into your new macOS virtual machine.