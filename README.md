# mbp-fedora-kernel

Fedora 30 kernel with Apple T2 patches built-in (Macbooks produced >= 2018).

Fedora 30 ISO (with mbp-fedora-kernel builtin) - <https://github.com/mikeeq/mbp-fedora>

## CI status

Drone kernel build status:
[![Build Status](https://cloud.drone.io/api/badges/mikeeq/mbp-fedora-kernel/status.svg)](https://cloud.drone.io/mikeeq/mbp-fedora-kernel)

Travis kernel publish status - <http://fedora-mbp-repo.herokuapp.com/> :
[![Publish Status](https://travis-ci.com/mikeeq/mbp-fedora-kernel.svg?branch=master)](https://travis-ci.com/mikeeq/mbp-fedora-kernel)

## TODO

- integrate `roadrunner2/macbook12-spi-driver` and `MCMrARM/mbp2018-bridge-drv` drivers
- add `kernel-headers` rpm generation

### Known issues

- 5.2 kernel - random kernel panics - <https://github.com/Dunedan/mbp-2016-linux/issues/71#issuecomment-510652894>
  - <https://bugs.archlinux.org/task/63159#comment180568>

> Tested on: Macbook Pro 15,2 13" 2019 i5 TouchBar Z0WQ000AR MV972ZE/A/R1

#### Not working

- Microphone
- Dynamic audio outputs change (on connecting/disconnecting headphones jack)
- Suspend/Resume (sleep mode)

#### Working with upstream stable kernel 5.1

- Display/Screen
- Thunderbolt 3/USB-C
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

### Fedora

- <https://fedoraproject.org/wiki/Building_a_custom_kernel>
- <https://fedoramagazine.org/building-fedora-kernel/>
- <https://www.hiroom2.com/2016/06/25/fedora-24-rebuild-kernel-with-src-rpm/>

### Github

- GitHub issue (RE history): <https://github.com/Dunedan/mbp-2016-linux/issues/71>
- VHCI+Sound driver (Apple T2): <https://github.com/MCMrARM/mbp2018-bridge-drv/>
- hid-apple keyboard backlight patch: <https://github.com/MCMrARM/mbp2018-etc>
- TouchBar driver: <https://github.com/roadrunner2/macbook12-spi-driver/tree/mbp15>
- Kernel patches (all are mentioned in github issue above): <https://github.com/aunali1/linux-mbp-arch>
- ArchLinux kernel patches: <https://github.com/ppaulweber/linux-mba>

## Credits

- @MCMrARM - thanks for all RE work
- @ozbenh - thanks for submitting NVME patch
- @roadrunner2 - thanks for SPI (touchbar) driver
- @aunali1 - thanks for ArchLinux Kernel CI
- @ppaulweber - thanks for keyboard and Macbook Air patches