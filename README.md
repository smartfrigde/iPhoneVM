# iPhoneVM

A preservation project for the historic **iPhoneVM.deb** package and its alternative LaunchDaemon-based swap configurations for jailbroken iPhone 2G, iPhone 3G, and iPhone 3GS devices.

## Background

Back in 2009, a Cydia package called **iPhoneVM.deb** appeared in several third-party repositories. It enabled virtual memory (swap) on older iPhones by leveraging Apple's built-in `dynamic_pager` utility. On memory-constrained devices such as the iPhone 3G with only 128 MB of RAM, users reported having significantly more free memory available after installation.

The original package has since been recovered (after a long search) and is preserved in this repository alongside alternative plist-based implementations documented by the jailbreak community.

## What Does iPhoneVM.deb Actually Do?

* It uses Apple's built-in `dynamic_pager` utility.
* It configures swap space through LaunchDaemons.
* It created swap files under `/private/var/vm` which is fixed to 256 MBs.
* Includes `/sbin/fm` which is a executable that measures available free memory, allocates roughly that amount of RAM, logs the number of bytes processed, then frees the memory and exits. 

The bundled `/sbin/vm` binary is simply Apple's `dynamic_pager` binary under a different name.

## Repository Layout

### `deb/`

Contains the recovered original **iPhoneVM.deb** package as distributed during the early jailbreak era.

This is preserved for historical and archival purposes. I very much recommend the plist method as it's cleaner and more flexible.

### `plist/`

Contains recreated and documented LaunchDaemon-based implementations derived from surviving forum posts and community research.

Available variants include:

* Dynamic swap (up to approximately 64 MB)
* Fixed 64 MB swap
* Fixed 128 MB swap
* Fixed 256 MB swap
* Fixed 512 MB swap

These versions use Apple's built-in `dynamic_pager` and can be installed manually without relying on the original package.

## How to verify that everything is working?

Run this command
```sh
du -shc /private/var/vm/*
```
Output should look something like this:
```sh
64M	/private/var/vm/iphone_swap0
64M	total
```

## Compatibility

Designed for:

* iPhone 2G
* iPhone 3G
* iPhone 3GS

Running:

* iPhone OS 2.x
* iPhone OS 3.x
* iOS 4.x

Usage on newer devices is unnecessary and untested.

## Installation

### Method 1: Original iPhoneVM.deb

Install the package using dpkg.

```sh
dpkg -i iPhoneVM.deb
```

The package can be found in: [deb/](deb/)

Reboot the device after installation.

### Method 2: Plist Variants (Recommended)

Downlod your selected plist variant: 
* [Dynamic swap](plist/dynamic/)
* [64 MB](plist/64mb/)
* [128 MB](plist/128mb/)
* [256 MB](plist/256mb/)
* [512 MB](plist/512mb/)

Copy the LaunchDaemon plist to:

```text
/System/Library/LaunchDaemons/
```

Reboot the device.


## Risks

Potential downsides include:

* **Increased flash wear** - old memory chips are not as durable as the modern ones
* Additional storage usage
* Slower performance when swapping occurs
* Possible UI lag under heavy memory pressure

## dynamic_pager manpage
Here's a missing (inside of OS-X) manpage taken from O'Reillys book - "Mac OS X for UNIX Geeks".
<img width="593" height="485" alt="obraz" src="https://github.com/user-attachments/assets/4eb6f167-4669-4197-9bfb-5118452c38e5" />


## Credits

* Original iPhoneVM authors (beyouriphone.com)
* jiztek for documenting the LaunchDaemon plist method
* Early jailbreak community researchers who analyzed iPhoneVM
* Archived forum discussions that preserved the original configuration
* Everyone involved in preserving legacy iOS software and jailbreak history
