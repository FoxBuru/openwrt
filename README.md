# OpenWRT <!-- omit in toc -->

This is a fork of the [OpenWRT mirror on github](https://github.com/openwrt/openwrt) that has some custom modifications (original from [j-d-r](https://github.com/j-d-r/openwrt/commit/ea71fd2aca68e50fb95119d182f1f1a71783fbac)) and adapted to current stable versions on upstream. 

## Warning

To use this firmware over a non-modified EAP245, you need physical access to AP. That's because the bootloader included by the manufacturer is broken badly (as explained by j-d-r). You proceed on your own risk, be warned!

### Prerequisites:

- Latest binary [u-boot from j-d-r](https://github.com/j-d-r/u-boot-QCA956x)
- An RS-232 adapter/interface/microcontroller attached to computer (i.e. Arduino) to help to the install process
  - It seems is [not needed anymore](https://github.com/j-d-r/openwrt#das-u-boot-upgrade-no-longuer-required), but YMMV.
- A good understanding of the generic flashing procedure of openwrt (https://openwrt.org/docs/guide-user/installation/generic.flashing)
- Pay attention to the bootcmd variable on your u-boot:
  - If `bootcmd=bootm 0x9F040000`, you must do some manual editing on the `target/linux/ath79/image/generic-tp-link.mk` or the `target/linux/ar71xx/image/generic-tp-link.mk` on the `KERNEL` parameter.
  - Another option is to modify the `bootcmd` option to not look a normal applicatoin image, but a ELF-based one, with the argument `bootelf`. At the end, your bootcmd should look like: `bootelf 0x9F040000`. You can use this snippet inside u-boot to change the bootcmd env variable:
```bash
setenv bootcmd bootelf 0x9F040000
saveenv
```

Reference values for serial connection:

| Value | Reference |
| ----- | --------- |
|Baudrate* | 115200 or 111607 |
|Data bits | 8 |
|Stop bits | 1 |
|Parity | None |
|Flow Control | None |

### Build status

![Build: Docker image](https://github.com/FoxBuru/openwrt/workflows/Build%20new%20docker%20builderimage/badge.svg)
