### macadmin-scripts

Some scripts that might be of use to macOS admins. Might be related to Munki;
might not.

#### createbootvolfromautonbi.py

A tool to make bootable disk volumes from the output of autonbi. Especially
useful to make bootable disks containing Imagr and the 'SIP-ignoring' kernel,
which allows Imagr to run scripts that affect SIP state, set UAKEL options, and
run the `startosinstall` component, all of which might otherwise require network
booting from a NetInstall-style nbi.

This provides a way to create a bootable external disk that acts like the Netboot environment used by/needed by Imagr.

This command converts the output of Imagr's `make nbi` into a bootable external USB disk:
`sudo ./createbootvolfromautonbi.py --nbi ~/Desktop/10.13.6_Imagr.nbi --volume /Volumes/ExternalDisk`

#### installinstallmacos.py

This script can create disk images containing macOS Installer applications available via Apple's softwareupdate catalogs.

It does this by downloading the packages from Apple's softwareupdate servers and then installing them into a new empty disk image.

Since it is using Apple's installer, any install check or volume check scripts are run. This means that you can only use this tool to create a diskimage containing the versions of macOS that will run on the exact machine you are running the script on.

For example, to create a diskimage containing the version 10.13.6 that runs on 2018 MacBook Pros, you must run this script on a 2018 MacBook Pro, and choose the proper version.

Typically "forked" OS build numbers are 4 digits, so when this document was last updated, build 17G2208 was the correct build for 2018 MacBook Pros; 17G65 was the correct build for all other Macs that support High Sierra.

If you attempt to install an incompatible version of macOS, you'll see an error similar to the following:

```
Making empty sparseimage...
installer: Error - ERROR_B14B14D9B7
Command '['/usr/sbin/installer', '-pkg', './content/downloads/07/20/091-95774/awldiototubemmsbocipx0ic9lj2kcu0pt/091-95774.English.dist', '-target', '/private/tmp/dmg.Hf0PHy']' returned non-zero exit status 1
Product installation failed.
```

Use a compatible Mac or select a different build compatible with your current hardware and try again.

Run `./installinstallmacos.py --help` to see the available options.

#### make_firmwareupdater_pkg.sh

This script was used to extract the firmware updaters from early High Sierra installers and make a standalone installer package that could be used to upgrade Mac firmware before installing High Sierra via imaging.

Later High Sierra installer changes have broken this script; since installing High Sierra via imaging is not recommended or supported by Apple and several other alternatives are now available, I don't plan on attempting to fix or upgrade this tool.
