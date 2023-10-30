Libre Le Potato (AML-S905X-CC) Docs:
This repo is a collection of tools, best practices, guides, and tutorials we use for the Libre Le Potato SBC. At Every Flavor, Le Potato is one of our main Single Board Computers due to its low cost, good I/O support, and generally strong availability (looking at you RPi). It is definitely less performant than the Pi's and the Rockchip boards, but it sits at a lower price than almost all alternatives.

Unfortunately, the documentation is a little weak and it takes a little digging to find what you're looking for. We're compiling our best practices here so that we don't have to re-learn everything everytime we set this board up, hopefully you find some value in this as well!

## Official Docs
Here's a list of useful first party docs:
* [Help/Documentation Page](https://libre.computer/products/aml-s905x-cc/)
* [Resource Guide](https://hub.libre.computer/t/aml-s905x-cc-le-potato-overview-resources-and-guides/288)
* [Pinout Diagram](https://docs.google.com/spreadsheets/d/1U3z0Gb8HUEfCIMkvqzmhMpJfzRqjPXq7mFLC-hvbKlE/edit)
* [Boot Troubleshooting](https://hub.libre.computer/t/troubleshooting-general-boot-issues/47)


## Boot Setup
1. Download boot image.
  * [Official Supported Distributions](https://libre.computer/products/aml-s905x-cc/)
  * [Direct link to Ubuntu 22.04 Server](https://distro.libre.computer/ci/ubuntu/22.04/ubuntu-22.04.3-preinstalled-server-arm64%2Baml-s905x-cc.img.xz)
2. Copy to SD Card using [**Rufus**](https://rufus.ie/en/).

## Expected Boot Behavior
(Taken and modified from [here](https://hub.libre.computer/t/aml-s905x-cc-boot-behavior/52))
1. When power is attached, the red and blue LEDs will turn on, while the green LED remains off. At this time, There is no power to HDMI or USB. 
2. The BootROM scans for the bootloader at sector 1 or 512B on eMMC and then MicroSD. If the bootloader is not found and the USB dual role port is connected to a computer, it will go into ROM mode. If the USB dual role port is not connected to a computer, it will repeat the scan.
3. If a bootloader is found, it loads the bootloader which will initialize the DRAM and then run u-boot.
4. u-boot will turn on the green LED to indicate that the system has software running.

## Boot Troubleshooting
The [boot troubleshooting guide](https://hub.libre.computer/t/troubleshooting-general-boot-issues/47) has a good of good information about troubleshooting issues with the board boot. Below is a shortened version of our experience:

* Ensure you're using a good SD card. Often times, the Le Potato will not even begin booting with a low-quality SD card. As a bare minimum, we use SanDisk Ultra Class I cards. 
* Ensure that your imaging tool is correctly imaging the SD card. We have never found success with Win32DiskImager, only with Rufus. Check our #disk-imaging guide for more details
* Ensure that your power supply is capable of delivering up to 1.5 amps, otherwise the board may brown out during boot.

## Wifi Drivers
* Wifi Driver available [here](https://github.com/morrownr/8821au-20210708) for TP-Link Archer T2U Plus High-Gain Wifi Antenna
  * Installing this requires updating the default gcc version to gcc-12. `sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 50`
*  `sudo nmcli dev wifi connect "SSID" password "PASSWORD"`
