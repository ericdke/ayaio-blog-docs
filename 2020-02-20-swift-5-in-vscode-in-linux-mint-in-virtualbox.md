---
title: "Swift 5 in VSCode in Linux Mint in VirtualBox"
date: "2020-02-20"
categories: 
  - "dev"
  - "linux"
  - "swift"
tags: 
  - "english"
---

Getting VSCode on Linux Mint to properly run Swift with sourcekit-lsp in order to get syntax highlighting and code completion can be rather convoluted.

Here's how I did it.

# First steps

- Download and install VirtualBox 6.0.
- Download Linux Mint Xfce 19.3.

In VirtualBox, create a new virtual machine with these settings:

- Dynamic VDI disk, at least 40GB
- Chipset PIIX3
- At least 4GB RAM
- Activate IO-APIC (do not check EFI)
- UTC clock
- Activate PAE/NX (do not check VT-x)
- 1 CPU runs ok, but 2 or more is better
- 100% resources
- Activate pagination
- Graphics driver must be VMSVGA
- 64 MO video RAM or more
- Activate 3D acceleration (do not check 2D acceleration)
- CD Drive IDE type PIIX4 with E/S
- Storage SATA AHCI without E/S

# Installing Linux Mint

Add the Linux iso as the CD Drive then start the machine. Once booted, double click on the "Install Linux Mint" CD icon then follow instructions.

Once it reboots, press ENTER to continue, then create name/username/account. Once logged in, dismiss the welcome dialog box (you will address these points later if you want).

The _first_ thing you should do after that is to run

```bash
apt-get update
```

in the terminal.

Next, run

```bash
apt-get install virtualbox-guest-dkms
```

Once done, click the "Devices > Insert guest addtions CD image" menu in VirtualBox. Wait a minute while it does its thing.

Then run these commands:

```bash
sudo mount -t iso9660 /dev/sr0 /mnt
sudo apt install -y gcc make perl linux-headers-generic
sudo sh /mnt/VBoxLinuxAdditions.run
reboot
```

After reboot you should be able to resize the screen window and to properly run the VM on hidpi screens.

# Installing VSCode and Swift

Try running this command:

```bash
sudo apt install code
```

If it doesn't work, follow the detailed instructions specified on [VSCode Linux Install](https://code.visualstudio.com/docs/setup/linux).

Install the missing bits:

```bash
sudo apt install curl git clang libicu-dev libsqlite3-dev libblocksruntime-dev libncurses5-dev
```

Next, download Swift itself on swift.org.

I used [Swift 5.1.4](https://swift.org/builds/swift-5.1.4-release/ubuntu1804/swift-5.1.4-RELEASE/swift-5.1.4-RELEASE-ubuntu18.04.tar.gz). If you're using a different version, you will have to adapt the path accordingly in the rest of this tutorial.

Untar and install in the right place:

```bash
sudo tar xzf swift-5.1.4-RELEASE-ubuntu18.04.tar.gz -C /usr/local/bin
```

Add Swift to the command line path by adding this line at the _end_ of your ~/.bashrc file:

```bash
export PATH=/usr/local/bin/swift-5.1.4-RELEASE-ubuntu18.04/usr/bin:"${PATH}"
```

Reload the command line session then run:

```bash
swift --version
```

to make sure Swift was downloaded and installed correctly.

# Installing SourceKit for VSCode

In order to properly use Swift in VSCode you need to build an extension based on sourcekit.

Run these commands (the building step might take some time):

```bash
git clone https://www.github.com/apple/sourcekit-lsp.git
cd sourcekit-lsp
swift package update
swift build -Xcxx -I/usr/local/bin/swift-5.1.4-RELEASE-ubuntu18.04/usr/lib/swift
```

Move the resulting build to the right place:

```bash
sudo mv .build/x86_64-unknown-linux/debug/sourcekit-lsp /usr/local/bin
```

Install Node.js 12.x:

```bash
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Generate the extension for VSCode:

```bash
cd Editors/vscode
npm run createDevPackage
```

Install the extension:

```bash
code --install-extension out/sourcekit-lsp-vscode-dev.vsix
```

Launch VSCode then point sourcekit-lsp at your installed toolchain in VSCode’s settings.

Do "File > Preferences > Settings" then type settings.json in the search field.

Click "Edit JSON" then add this between the curly barckets:

```text
"sourcekit-lsp.toolchainPath": "/usr/local/bin/swift-5.1.4-RELEASE-ubuntu18.04/"
```

Save the file then reload your VSCode window (Control+Shift+P > Reload Window) or restart VSCode.

Done!
