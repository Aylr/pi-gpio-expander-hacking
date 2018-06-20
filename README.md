# Raspberry Pi i2c GPIO Expander MCP23017

So, you've got a raspberry pi and want more GPIO? Grab one of these [expander hats](http://www.nationelectronics.com/raspberry-pi-extensions/174-raspberry-pi-hat-32-io-port-expander-v11-mcp23017-i2c-black-0648260628239.html).

This document will walk you through command line use of outputs.

## CLI

The main program we will use is [i2cset](https://linux.die.net/man/8/i2cset).

### Arguments You Need

1. `-y` disables interactive mode
2. `1` (the default i2c bus on the pi)
3. `0x23` IO chip address (set by 3 bit switches)
4. `0x00` 8 bit data address
5. `0x00` 8 bit data values

## How To Use Outputs

1. Set pin modes to output:
    - set A register `i2cset -y 1 0x23 0x00 0x00` (all outputs)
    - set B register `i2cset -y 1 0x23 0x01 0x00` (all outputs)
2. Send a command
    - All A pins off `i2cset -y 1 0x23 0x14 0x00`
    - All B pins off `i2cset -y 1 0x23 0x15 0x00`
    - All A pins on `i2cset -y 1 0x23 0x14 0xFF`
    - All B pins on `i2cset -y 1 0x23 0x15 0xFF`

## How To Use Inputs

1. Set pin modes to input:
    - set A register `i2cset -y 1 0x23 0x00 0xFF` (all inputs)
    - set B register `i2cset -y 1 0x23 0x01 0xFF` (all inputs)

## Resources

- [MCP23017 Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/20001952C.pdf)
- [Raspberry Pi HAT - 32 I/O Port Expander](http://www.nationelectronics.com/raspberry-pi-extensions/174-raspberry-pi-hat-32-io-port-expander-v11-mcp23017-i2c-black-0648260628239.html)
- [Interfacing an I2C GPIO expander (MCP23017) to the Raspberry Pi using C++ (i2cdev)](http://www.hertaville.com/interfacing-an-i2c-gpio-expander-mcp23017-to-the-raspberry-pi-using-c.html)
