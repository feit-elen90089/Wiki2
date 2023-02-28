# Nuand bladeRF 2.0 micro

The bladeRF 2.0 micro is the second generation of highly capable SDRs produced
by Nuand, LLC. It will be the main SDR used for the CDC design project.

## Content

1. [Overview](#overview)  
2. [Command Line Interface](#command-line-interface)  
3. [SoapySDR Block](#soapysdr-block)
   - [Block Configuration](#block-configuration)  
   - [Message Port Interface](#message-port-interface)  
   - [Stream Tag Interface](#stream-tag-interface)  
4. [libbladeRF](#libbladerf)
5. [Performance](#performance)

## Overview

The key component on the bladeRF 2.0 board is an Analog Devices AD9361 wideband
transceiver, an RFIC which is also found in many other common SDRs (Ettus
USRP B series and ADALM PlutoSDRs).

The following is a list of useful references for understanding and using the
bladeRF. The bladeRF wiki is the best place to start.

- [bladeRF 2.0 micro](https://www.nuand.com/bladerf-2-0-micro/)
- [bladeRF wiki](https://github.com/Nuand/bladeRF/wiki)
- [libbladeRF documentation](https://nuand.com/bladeRF-doc/libbladeRF/v2.2.1/)
- [bladeRF source code](https://github.com/Nuand/bladeRF)
- [bladeRF 2.0 Schematic](datasheets/bladeRF-micro.pdf)

To use the bladeRF within our Ubuntu environment, it first must be connected to
the VM by selecting: *Devices > USB > Nuand bladeRF 2.0*

In CDC we will use the *xA9* version of the board, where board versions vary
only in the size of the onboard FPGA.

<div align="center">

| Version | Logic Elements |
| ------- | :------------: |
|   xA4   |       49k      |
|   xA5   |       77k      |
|   xA9   |      301k      |

</div>

> **Important Note:** To avoid violating governmental regulations and damaging
> the hardware, please acknowledge and adhere to the following guidelines:
> - Never transmit or receive on any band on which you are not licensed to
> operate
> - Always terminate TX and RX ports with a 50 Ohm load (either an antenna or SMA
> terminator)
> - Never connect a TX port directly to an RX port without proper attenuation
> at least 30 dB)


## Command Line Interface

The `bladeRF-cli` command line utility can be used to verify device connectivity
as well as query and set device parameters. For complete information, see the
following references.

- [Verifying Basic Device Operation](https://github.com/Nuand/bladeRF/wiki/Getting-Started%3A-Verifying-Basic-Device-Operation)
- [bladeRF CLI Tips and Tricks](https://github.com/Nuand/bladeRF/wiki/bladeRF-CLI-Tips-and-Tricks)

For our purposes, we will only use `bladeRF-cli` to verify connectivity and not
to set device parameters. To ensure the bladeRF is correctly attached, the
`--probe` or `-p` command can be used.

```
$ bladeRF-cli -p # probe for connected bladeRF devices

  Description:    Nuand bladeRF 2.0
  Backend:        libusb
  Serial:         991431a963384f8289baea2ba586720d
  USB Bus:        2
  USB Address:    2
```

The command line tool also has an interactive mode, which can be a more
convenient way of querying and configuring the board.

```
$ bladeRF-cli -i # enter interactive mode
```

Within interactive mode you can check the bladeRF driver, device firmware, and
FPGA versions currently loaded.

```
bladeRF> version

  bladeRF-cli version:       1.8.0-0.2019.07.rbuild1
  libbladeRF version:        2.2.1-0.2019.07-4build1

  Firmware version:          2.3.2
  FPGA version:              0.11.0 (configured by USB)
```

You can also read expanded device information.

```
bladeRF> info

  Board:                    Nuand bladeRF 2.0 (bladerf2)
  Serial #:                 991431a963384f8289baea2ba586720d
  VCTCXO DAC calibration:   0x1d11
  FPGA size:                301 KLE
  FPGA loaded:              yes
  Flash size:               128 Mbit
  USB bus:                  2
  USB address:              2
  USB speed:                SuperSpeed
  Backend:                  libusb
  Instance:                 0
```

See `bladeRF --help` for a full list of possible commands.

## SoapySDR Block

TODO

## libbladeRF

The bladeRF device can be controlled directly from Python and C/C++ programs
using the libbladeRF library.

- [libbladeRF documentation](https://nuand.com/bladeRF-doc/libbladeRF/v2.2.1/)

## Performance

This section will describe procedures for characterizing performance of the
bladeRF boards and report typical results.

Metrics:
- USB throughput
- Noise figure/floor
- Frequency Stability
- DC offset
- IQ imbalance
