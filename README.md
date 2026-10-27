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
assumes picotool is installed in /usr/local
```bash
export PATH="$PWD/../picotool/build:$PATH"

#SAMPLE_RATE="44100"
SAMPLE_RATE="48000"

DBG_UART=1

WHAT='rp2040'; BOARD="pico"
#WHAT='rp2350'; BOARD="pico2"

cmake -S . -B "build-$WHAT-$SAMPLE_RATE" -G Ninja \
 -DPICO_SDK_PATH=../pico-sdk \
 -DPICO_BOARD="$BOARD" \
 -Dpicotool_DIR=/usr/local/lib/cmake/picotool \
 -DSAMPLE_RATE="$SAMPLE_RATE" \
 -DDBG_UART="$DBG_UART"

time cmake --build "build-$WHAT-$SAMPLE_RATE" \
 && ls -l "build-$WHAT-$SAMPLE_RATE/pico_usb_i2s_speaker.uf2"
```
