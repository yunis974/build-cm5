# build-cm5 — PemuOS pour Raspberry Pi CM5

Configuration Buildroot pour construire **PemuOS** sur un Raspberry Pi Compute Module 5 (carte CM5IO).

- Base : `raspberrypicm5io_defconfig` (Buildroot 2026.08)
- Noyau : raspberrypi/linux (defconfig `bcm2712`)
- Hostname : `pemu`, shell : zsh, SSH : dropbear, DHCP sur `eth0`

## Fichiers

| Fichier | Rôle |
|---|---|
| `cm5_defconfig` | defconfig Buildroot minimal |
| `images/genimage.cfg` | partitionnement de la carte SD |
| `images/rpi-firmware/config.txt`, `cmdline.txt` | config de boot |

## Build

```sh
git clone https://github.com/buildroot/buildroot.git
cd buildroot
make O=../build-cm5 defconfig BR2_DEFCONFIG=../build-cm5/cm5_defconfig
cd ../build-cm5 && make
```

Image finale : `images/sdcard.img`.

> **Notes**
> - `BR2_TARGET_GENERIC_ROOT_PASSWD` est vide dans le defconfig : définis ton mot de passe root avec `make menuconfig` avant de builder.
> - `BR2_ROOTFS_OVERLAY` pointe vers un dossier overlay local (`pemuos/overlay`) qui n'est pas inclus ici : adapte le chemin.
