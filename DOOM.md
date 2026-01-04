# DOOM on the CDJ-3000

> [!NOTE]
> This is meant for developers -- will streamline this for end users soon.

## Installing

### Compatibility

- Compatible with Renesas SoC based CDJ-3000s.

### Prerequisites

- A compatible CDJ-3000
  - Connected to your local network
  - Audio connected via Digital Out
- An SD-card with of at least 1 GiB in size
- A USB key formatted to FAT32

## Prepare your player with Magic Phono Loader

Magic Phono Loader works by toggling a boot flag in non-volatile memory to allow booting firmware from an SD-card.

If no bootable SD-card is present the CDJ-3000 will continue booting from internal firmware as usual.

The chances of this bricking your CDJ-3000 is low, however there is a non-zero chance something could go wrong.

> [!CAUTION]
> This tool is experimental software with the potential to brick your CDJ. **USE AT YOUR OWN RISK**.

To prepare your player:
- Download the pre-built <a href="https://github.com/Magic-Phono/cdj3k-magicphono-loader/releases/download/v1.0.0/CDJ3KvSDBOOT001.UPD">`CDJ3KvSDBOOT001.UPD`</a> update file.
- Copy it to a FAT32 USB key. Make sure there are no other update files on the USB key.
- Insert the USB key into your CDJ-3000. Enter udpate mode by pressing IN/CUE and RELOOP/EXIT while powering on the unit.
- Once complete, you can reboot your CDJ.
- Congratulations! You can now boot custom firmwares from an SD-card, such as <a href="https://github.com/Magic-Phono/cdj3k-magicphono-distro">MagicPhono Linux</a>.
- If no bootable SD-card is present the CDJ-3000 will continue booting from internal firmware as usual.

## Write Magic Phono Linux to an SD-card

- Download the pre-built <a href="https://github.com/Magic-Phono/cdj3k-magicphono-distro/releases/download/v1.0.0/magicphono-cdj3k-1.0-dev.img">`magicphono-cdj3k-1.0-dev.img`</a> image.
- Write it to a SD-card using a tool like <a href="https://www.raspberrypi.com/software/" target="_blank">Raspberry Pi Imager</a> (despite the name it can write any image file to an SD card).

## Download the DOOM levels to USB key

- Download <a href="https://distro.ibiblio.org/slitaz/sources/packages/d/doom1.wad">doom1.wad</a> and put it onto the USB key.

## Running

- On a CDJ-3000 with <a href="https://github.com/Magic-Phono/cdj3k-magicphono-loader">MagicPhono Loader</a> installed, put the SD-card in the SD slot and turn the CDJ-3000 on.
- MagicPhono Linux should boot from the SD-card.
- If booting from the SD-card fails, the CDJ-3000 will boot from its internal firmware as usual.

> [!WARNING]  
> Root access via SSH is enabled by default with no password. This will be disabled in future pre-built
> images as MagicPhono Linux stabilizes.

Currently, Magic Phono Linux will boot to a non-graphical environment with SSH enabled.

## Playing DOOM 

**need to fix* default.cfg, subucom_input, startx*

- Put the USB key with doom1.wad into the player.
- SSH into your player.
- Run:
```
mkdir -p /mnt/usb
cp /mnt/usb/doom1.wad /tmp

mkdir -p /home/root/.chocolate-doom/
cp default.cfg /home/root/.chocolate-doom/

export DISPLAY=:0
export SDL_AUDIODRIVER=alsa

subucom_input &
startx &

cd /tmp
chocolate-doom -iwad doom1.wad 
```

