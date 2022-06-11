# NOTE:

As of today,June 11th 2022, Demo Code from https://www.waveshare.com/wiki/Pico-LoRa-SX1262-868M for this HAT did not work for me. 

I spent 6 weeks sending emails back and forth and all they could do was tell me my keys didn't work (even though I told them they worked on a Pico-RFM95W setup).

Anyway, the problem was traced to the file src/lorawan.c and some code, using sscanf("%shhx"), which corrupted the keys. I replaced calls to that with a simple method to convert the ascii hex keys to a byte array and the board now talks to TTN

NOTE: Sandeep Mistry has updated his code in src/board/rp2040/spi-board.c - that change is included here.


What follows is Waveshare's original readme.

# pico-lorawan
Enable LoRaWAN communications on your [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/) or any RP2040 based board using a [Semtech SX1276 radio module](https://www.semtech.com/apps/product.php?pn=SX1276).

Based on the Semtech's [LoRaWAN end-device stack implementation and example projects](https://github.com/Lora-net/LoRaMac-node).

## Hardware

 * RP2040 board
   * [Raspberry Pi Pico](https://www.raspberrypi.org/products/raspberry-pi-pico/)
   * [Adafruit Feather RP2040](https://www.adafruit.com/product/4884)
 * Semtech SX1276 board
   * [Adafruit RFM95W LoRa Radio Transceiver Breakout - 868 or 915 MHz - RadioFruit](https://www.adafruit.com/product/3072)
   * [Adafruit LoRa Radio FeatherWing - RFM95W 900 MHz - RadioFruit](https://www.adafruit.com/product/3231) 

### Default Pinout

| Raspberry Pi Pico / RP2040 | Semtech SX1276 |
| ----------------- | -------------- |
| 3.3V | VCC |
| GND | GND |
| GPIO 18 | SCK |
| GPIO 19 | MOSI |
| GPIO 16 | MISO |
| GPIO 7 | DIO0 / G0 |
| GPIO 8 | NSS / CS |
| GPIO 9 | RESET |
| GPIO 10 | DIO1 / G1 |

GPIO pins are configurable in examples or API.

## Examples

See [examples](examples/) folder.

There is a `config.h` file to your ABP or OTAA node configuration for each example.

## Cloning

```sh
git clone --recurse-submodules https://github.com/sandeepmistry/pico-lorawan.git 
```

## Building

1. [Set up the Pico C/C++ SDK](https://datasheets.raspberrypi.org/pico/getting-started-with-pico.pdf)
2. Set `PICO_SDK_PATH`
```sh
export PICO_SDK_PATH=/path/to/pico-sdk
```
3. Create `build` dir, run `cmake` and `make`:
```
mkdir build
cd build
cmake .. -DPICO_BOARD=pico
make
```
4. Copy example `.uf2` to Pico when in BOOT mode.

## Acknowledgements

A big thanks to [Alasdair Allan](https://github.com/aallan) for his initial testing of EU868 support!

This project was created on behalf of the [Arm Software Developers](https://developer.arm.com/) team, follow them on Twitter: [@ArmSoftwareDev](https://twitter.com/armsoftwaredev) and YouTube: [Arm Software Developers](https://www.youtube.com/channel/UCHUAckhCfRom2EHDGxwhfOg) for more resources!

