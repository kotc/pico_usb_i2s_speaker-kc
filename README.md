# pico_usb_i2s_speaker-kc
It is a USB DDC that outputs i2s with master clock using RP Pico and tinyusb.
The USB stack uses tinyusb.
Additional mods by ariel/KotCzarny.

## i2s
I'm using pico-i2s-pio. The RP2040/RP2350 system clock is set to MCLK's integer multiples, and the low jitter mode does not use the choraltic divider of pio.
It supports 16bit right packing of i2s, PT8211, EXDF and i2s of the AK449X, and slave mode of i2s. It is also possible to operate the i2s and PT8211 with dual objects.

### Default config
i2s-slave mode, 48kHz

|name|pin|
|----|---|
|DATA|GPIO6|
|LRCLK|GPIO7|
|BCLK|GPIO8|
|MCLK|GPIO13|

## build
```bash
git clone https://github.com/kotc/pico_usb_i2s_speaker-kc
cd pico_usb_i2s_speaker-kc
mkdir build && cd build
cmake .. && make -j4
```
