# pi-tm1638-lgpio

[日本語版はこちら / Japanese](README_ja.md)

A port of [pi-tm1638](https://github.com/mjoldfield/pi-tm1638) by Martin Oldfield,
updated to use [lgpio](http://abyz.me.uk/lg/lgpio.html) instead of bcm2835.
This enables support for Raspberry Pi 5 (RP1 chip) as well as earlier models.

## Background

The original pi-tm1638 library uses the bcm2835 library for GPIO access,
which does not work on Raspberry Pi 5 due to its new RP1 I/O chip.
This port replaces bcm2835 with lgpio, which supports both RP1 and earlier BCM chips.

## Confirmed Working

| Hardware | OS | Kernel |
|---|---|---|
| Raspberry Pi 5 | Raspberry Pi OS Bookworm (Debian 12, 64bit) | 6.12.62 |
| Raspberry Pi 4 | Raspberry Pi OS Trixie (Debian 13, 64bit) | 6.12.47 |

## Dependencies
```bash
sudo apt install liblgpio-dev
```

## Build
```bash
git clone https://github.com/kuboaki/pi-tm1638-lgpio.git
cd pi-tm1638-lgpio
autoreconf -fi
./configure
make
sudo make install
```

## Changes from Original

- `src/tm1638.c`: Replaced bcm2835 API with lgpio API
- `configure.ac`: Changed library dependency from bcm2835 to lgpio
- `src/Makefile.am`: Updated CFLAGS (`-std=c99` to `-std=gnu99`) and LIBS
- `examples/Makefile.am`: Updated CFLAGS (`-std=c99` to `-std=gnu99`)
- `examples/*.c`: Removed `bcm2835_init()/close()`, replaced `delay()` with `nanosleep()`

## Original

- Author: Martin Oldfield &lt;ex-tm1638@mjo.tc&gt;
- Repository: https://github.com/mjoldfield/pi-tm1638

## License

GPL v2 (same as original)
