# ONIE Packer

A tool to create ONIE installer image from regular Linux OS image files (ISO, IMG, etc.).

This tool can be used to create a specialized [ONIE installer](https://opencomputeproject.github.io/onie/overview/index.html) for whitebox switches from regular ISO images of various popular Linux distributions.

## Usage

`./onie_pack.sh [-i installer] os_image`

**installer** - is a script in `installers` directory, which will handle OS installation from a regular ISO image when it is launched by ONIE environment on a switch.
Default installer: `ubuntu2bin`

## Currently supported installers

### Ubuntu

* Supported versions: 20.04, 22.04
* Supported OS images:
  * ubuntu-20.04.4-live-server-amd64.iso
  * ubuntu-22.04.1-live-server-amd64.iso
* Default credentials:
  * ubuntu/ubuntu
  * root/pass

## Currently supported switches

* Tofino switches (tested on Ufispace S9180-32x)

## Examples

### Creating ONIE installer from Ubuntu Server ISO image

* Clone this repo: `git clone https://github.com/mariusz-stordis/onie-packer`
* `cd onie-packer`
* Download ISO file: `wget http://releases.ubuntu.com/focal/ubuntu-20.04.4-live-server-amd64.iso`
* Pack it into ONIE installer: `./onie_pack.sh ubuntu-20.04.4-live-server-amd64.iso`
* ONIE installer is ready: `ubuntu2bin-x86_64-<date>.bin`

### Installing OS on a switch

* Boot to ONIE Rescue shell
* `onie-nos-install ftp://user:pass@<ip>/ubuntu2bin-x86_64-<date>.bin`
* Wait until OS is installed
* `ssh admin@<switch_ip>`
