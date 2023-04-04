# CDC Link

## Installation

The CDC link is available in the [gr-cdc](https://gitlab.eng.unimelb.edu.au/elen90089/2023/gr-cdc) Gitlab repo.

### Dependencies

The CDC link assumes that `gr-bladeRF` GNU Radio OOT module for controlling the
bladeRF has been installed. See the [gr-bladeRF](bladeRF#gr-bladeRF) wiki
section for installation instructions.

### gr-cdc

To use the CDC link, you must first build and install the **gr-cdc** module.

```
$ git clone https://gitlab.eng.unimelb.edu.au/elen90089/2023/gr-cdc.git
$ cd gr-cdc
$ mkdir build && cd build
$ cmake ..
$ make
$ sudo make install
$ sudo ldconfig # if installing for the first time
```

## Overview

The CDC link is currently composed of two main hierarchical blocks: *CDC PHY Tx*
and *CDC PHY Rx*. The Python and YAML files for these blocks are installed with
the **gr-cdc** module, but they were originally generated with GRC. You can
investigate and create modified versions of the blocks using the following GRC
files.

- `./examples/cdc_phy_tx.grc`
- `./examples/cdc_phy_rx.grc`

Note that these GRC files will create blocks called *CDC PHY Tx (Mod)* and
*CDC PHY Rx (Mod)* so that there is no conflict with the installed versions.

Example GRC applications can be found in the **gr-cdc** repo.

- `./examples/cdc_phy_loopback.grc`
- `./examples/cdc_phy_bladeRF.grc`

Additional description of the CDC link is TBD.
