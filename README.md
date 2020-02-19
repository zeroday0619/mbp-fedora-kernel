# mbp-fedora-kernel

Fedora kernel with Apple T2 patches built-in (Macbooks produced >= 2018).

Fedora ISO (with mbp-fedora-kernel builtin) - <https://github.com/mikeeq/mbp-fedora>

There are multiple version of the kernel maintained on seperate branches (all compiled versions could be found in releases section):

- 5.4-f31 - <https://github.com/mikeeq/mbp-fedora-kernel/tree/v5.4-f31>
- 5.3-f31 - <https://github.com/mikeeq/mbp-fedora-kernel/tree/v5.3-f31>
- 5.3-f30 - <https://github.com/mikeeq/mbp-fedora-kernel/tree/v5.3-f30>
- 5.1-f30 - <https://github.com/mikeeq/mbp-fedora-kernel/tree/v5.1>

## How to update kernel-mbp

```
### First run
sudo -i
curl -L https://raw.githubusercontent.com/mikeeq/mbp-fedora-kernel/v5.4-f31/update_kernel_mbp.sh -o /usr/local/bin/update_kernel_mbp
chmod +x /usr/local/bin/update_kernel_mbp
update_kernel_mbp

### Next ones
sudo -i
update_kernel_mbp
```

## CI status

Drone kernel build status:
[![Build Status](https://cloud.drone.io/api/badges/mikeeq/mbp-fedora-kernel/status.svg)](https://cloud.drone.io/mikeeq/mbp-fedora-kernel)

Travis kernel publish status - <http://fedora-mbp-repo.herokuapp.com/> :
[![Publish Status](https://travis-ci.com/mikeeq/mbp-fedora-kernel.svg?branch=master)](https://travis-ci.com/mikeeq/mbp-fedora-kernel)

## TODO

- integrate `roadrunner2/macbook12-spi-driver` and `MCMrARM/mbp2018-bridge-drv` drivers into kernel
- add `kernel-headers` rpm generation

> Tested on: Macbook Pro 15,2 13" 2019 i5 TouchBar Z0WQ000AR MV972ZE/A/R1

```
Boot ROM Version:	220.270.99.0.0 (iBridge: 16.16.6571.0.0,0)
MacOS Mojave: 10.14.6 (18G103)
```

### Known issues

- Microphone (it's recognised with new apple t2 sound driver, but there is a low mic volume amp)
- Dynamic audio outputs change (on connecting/disconnecting headphones jack)
- Suspend/Resume (sleep mode)
- Thunderbolt

#### Working with upstream stable kernel 5.1

- Display/Screen
- USB-C
- Battery/AC
- Ethernet/Video USB-C adapters
- Bluetooth

#### Working with mbp-fedora-kernel

- NVMe
- Camera
- keyboard
- touchpad (scroll, right click)
- wifi
  - you need to manually extract firmware from MacOS
    - <https://github.com/Dunedan/mbp-2016-linux/issues/71#issuecomment-517444300>
    - <https://github.com/Dunedan/mbp-2016-linux/issues/71#issuecomment-515401480>

> The firmware files to use can be found by running `ioreg -l | grep C-4364` or `ioreg -l | grep RequestedFiles`, copy from `/usr/share/firmware/wifi` when being on MacOS

```
Put the firmware in the right place!
The .trx file for your model goes to /lib/firmware/brcm/brcmfmac4364-pcie.bin,
the .clmb goes to /lib/firmware/brcm/brcmfmac4364-pcie.clm_blob
and the .txt to something like /lib/firmware/brcm/brcmfmac4364-pcie.Apple Inc.-MacBookPro15,2.txt
```

#### Working with external drivers

>> with @MCMrARM mbp2018-bridge-drv

- keyboard
- touchpad
- touchbar
- audio

#### Not tested

- eGPU

## Docs

- Discord: <https://discord.gg/39Rmjh>

### Fedora

- <https://fedoraproject.org/wiki/Building_a_custom_kernel>
- <https://fedoramagazine.org/building-fedora-kernel/>
- <https://www.hiroom2.com/2016/06/25/fedora-24-rebuild-kernel-with-src-rpm/>

### Github

- GitHub issue (RE history): <https://github.com/Dunedan/mbp-2016-linux/issues/71>
- VHCI+Sound driver (Apple T2): <https://github.com/MCMrARM/mbp2018-bridge-drv/>
- AppleSMC driver (fan control): <https://github.com/MCMrARM/mbp2018-etc/tree/master/applesmc>
- hid-apple keyboard backlight patch: <https://github.com/MCMrARM/mbp2018-etc/tree/master/apple-hid>
- TouchBar driver: <https://github.com/roadrunner2/macbook12-spi-driver/tree/mbp15>
- Kernel patches (all are mentioned in github issue above): <https://github.com/aunali1/linux-mbp-arch>
- ArchLinux kernel patches: <https://github.com/ppaulweber/linux-mba>

## Credits

- @MCMrARM - thanks for all RE work
- @ozbenh - thanks for submitting NVME patch
- @roadrunner2 - thanks for SPI (touchbar) driver
- @aunali1 - thanks for ArchLinux Kernel CI
- @ppaulweber - thanks for keyboard and Macbook Air patches
