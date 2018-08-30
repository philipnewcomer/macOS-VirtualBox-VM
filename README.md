# macOS VirtualBox VM

This is a preconfigured macOS VirtualBox Virtual Machine, along with a script for preparing a bootable install ISO image from a downloaded Mac OS installer app.

*Note: The `create_install_iso.sh` script is tailored to macOS hosts, and the macOS High Sierra installer app. The script will will need to be modified to work with the installer app for other versions of macOS.*

## Prerequisites

- You need a Mac to run the script `create_install_iso.sh` and generate HighSierra.iso file.
- You need a Virtualbox installed on your hypervisor host (Win/Linux/Mac/whatever)

## Part 1: Generate ISO on the Mac

- Download the macOS installer app if you have not already. It should be located in your `Applications` directory.
- Clone this git repo to your Mac.
- Run `create_install_iso.sh`, which will create a file named `HighSierra.iso` **on your desktop**, which is based on the downloaded macOS installer app. It will take about 1-2 minutes or more.
- Copy the resulting `HighSierra.iso` file from your desktop to your hypervisor host

## Part 2: Initial configuration of the VM on the hypervisor host

In the VirtualBox GUI: 
- Open the virtual machine from the repo
- Create a new virtual hard disk. Make sure that your new virtual hard drive is not set as an SSD, otherwise the High Sierra installer will format the drive as APFS, which is not yet recognized/supported by VirtualBox's EFI BIOS and you will not be able to boot from the hard drive.
- Set the `HighSierra.iso` as an inserted disk in the VM's optical drive 
  
## Part 3: Patch the configuration of the VM you have created.

- For Windows hosts, go to `%USERPROFILE%\.VirtualBox` folder
- Checkout the `macOS.vbox` file from this git repo and copy `uuid` and `name` properties of `Machine` XML tag from the .vbox of your freshly created configuration into `macOS.vbox`.
- Remove the .vbox file created by the Virtualbox (and copy the name of it into the clipboard)
- Rename `macOS.vbox` into the name from your clipboard. Put it into this folder (`%USERPROFILE%\.VirtualBox`)
- Edit the VM's CD and HDD - it will point to a wrong places until you edit it. Point them to a correct images you have created before.

## Part 4: installation

- Start the VM, and wait for the macOS installer boot.
- When the boot completed, open **Disk Utility**. From the **View** menu enable the option to "Show all devices", and erase the virtual hard disk image you.
- Quit the **Disk Utility**, and install macOS to the newly initialized hard drive.
- When the installer completes, reboot the VM. 
- Remove the ISO disk from the virtual optical drive and reboot the VM again.
- With the Installer ISO image not available to boot from, you will be dumped into the EFI Shell. Enter the following at the EFI prompt to boot macOS from the virtual hard drive and finish installation: `FS1:"macOS Install Data\Locked Files\Boot Files\boot.efi"` Alternatively, you can enter `exit` at the prompt to go to the EFI BIOS boot screen, and use the `Boot from file` option to navigate to boot.efi. This is required only once.

## Post installation steps

If you don't need to bind with your Apple Id (for example, if you are preparing the redistributable image), skip this step on the welcome steps after the installation (on the top of the form which asks you your e-mail Apple ID).

## Limitations

- No 2D/3D/OpenGL acceleration is supported for macOS, no 3D rendering is working (DRI view show as an empty zone on the screen)
- No Virtualbox Guest Tools are available for macOS, no shared folders are available
