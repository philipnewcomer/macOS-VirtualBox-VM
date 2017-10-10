# macOS VirtualBox VM

This is a preconfigured macOS VirtualBox Virtual Machine, along with a script for preparing a bootable install ISO image from a downloaded Mac OS installer app.

*Note: The `create_install_iso.sh` script is tailored to macOS hosts, and the macOS High Sierra installer app. The script will will need to be modified to work with the installer app for other versions of macOS.*

## Usage

1. Download the macOS installer app if you have not already. It should be located in your `Applications` directory.
2. Clone this repo to your machine.
3. Run `create_install_iso.sh`, which will create a file named "HighSierra.iso" on your desktop, based on the downloaded macOS installer app.
4. In the VirtualBox GUI, open the virtual machine from the repo, create a new virtual hard disk, and set the `HighSierra.iso` image created in step 3 as a disk in the VM's optical drive. Make sure that you do not set the new virtual hard drive as an SSD, otherwise the High Sierra installer will format the drive as APFS, which is not yet recognized by VirtualBox's EFI BIOS and you will be unable to boot from the hard drive.
5. Start the VM, and wait for the macOS installer to boot.
6. Open Disk Utility, from the View menu enable the option to "Show all devices", and erase the VirtualBox hard disk image.
7. Quit Disk Utility, and install macOS to the newly initialized hard drive.
8. When the installer completes, reboot. The VM will boot from the USB drive; remove the disk from the virtual drive and reboot the VM.
9. With the Installer ISO image not available to boot from, you will be dumped into the EFI Shell. Enter the following at the EFI prompt to boot macOS from the virtual hard drive and finish installation: `FS1:"macOS Install Data\Locked Files\Boot Files\boot.efi"` Alternatively, you can enter `exit` at the prompt to go to the EFI BIOS boot screen, and use the `Boot from file` option to navigate to boot.efi.
