# Single-carrier Links

This guide includes activities for the workshop session of week 5. Please refer
to the following overview slides as needed.

- [Workshop 05 - Single-Carrier Links](https://canvas.lms.unimelb.edu.au/courses/151467/pages/workshop-05-single-carrier-links)

## Additional GNU Radio Concepts

In this workshop we will investigate a baseline GRC packet link example.
However, there are two more important GNU Radio concepts we should have some
understanding of before beginning our investigating. The first is the
*Hierarchical Block*, which is a convenient way to group commonly used blocks
together into a single block that can be included in our flowgraphs.

> **To Do:**
> 1. Review the GNU Radio tutorial on [Hierarchical Blocks](https://wiki.gnuradio.org/index.php/Hier_Blocks_and_Parameters)

Previously, we have also seen two ways in which GNU Radio blocks pass
information to downstream blocks: through writing samples to their output ports
or by using stream tags to attach metadata to specific samples within a stream.
It is also possible to pass information of fixed size asynchronously between
blocks through the use of *Message Passing*. Like stream tags, message passing
relies on the use of GNU Radio's support of
[Polymorphic Types (PMTs)](https://wiki.gnuradio.org/index.php/Polymorphic_Types_(PMTs)).

> **To Do:**  
> 2. Review the GNU Radio tutorial on [Message Passing](https://wiki.gnuradio.org/index.php/Message_Passing)

## GNU Radio Packet Transmitter

Many wireless digital communication systems transfer information in short,
time-limited bursts, called packets or frames, rather than as continuous
streams of data. This is common when multiple users are sharing the wireless
medium such as in 802.11 WiFi or Bluetooth. Packetized transmission of data
will be important for the CDC design project due to the bursty nature of the
frequency spectrum's availability. GNU Radio has several blocks that are
important for building up the transmit and receive functionality needed for
packetized data transfer.

> **To Do:**
> 3. Review the documentation for
> [GNU Radio’s Packet Example](https://www.gnuradio.org/doc/doxygen/page_packet_comms.html).
> You may also wish to also revisit the GNU Radio
> [Packet Communications Tutorial](https://wiki.gnuradio.org/index.php?title=Packet_Communications)
> as it covers similar concepts but with a slightly different setup.
> 4. Experiment with GNU Radio’s packet example. Code for the example can be
> found on the Ubuntu VM at the following location: `/use/share/gnuradio/examples/digital/packet`.
> You should make a local copy of the following GRC flowgraphs.
>
>   - `packet_loopback_hier.grc`
>   - `packet_tx.grc`
>   - `packet_rx.grc`
>

The files `packet_tx.grc` and `packet_rx.grc` are hierarchical blocks, so you
must first generate their code before using the blocks in the software
simulation application `packet_loopback_hier.grc`. Note it can be very
insightful to investigate the output of each signal processing block in the
transmit and receive chains to verify the output is as expected. This is
particularly useful in debugging.

## CDC Link

Although the GNU Radio packet example is basically functional, past teams have
encountered a number of issues in getting the link to operate reliably. To
support your project work, we will provide you with a CDC baseline link that
should have better reliability. This link will be available in the *gr-cdc*
Out-of-Tree (OOT), the repo for which is hosted on the FEIT Gitlab server.

> **To Do:**  
> 5. See the following [README](https://gitlab.eng.unimelb.edu.au/elen90089/2023/gr-cdc.git)
> for instructions on how to install the gr-cdc OOT. The gr-cdc module will be
> updated throughout semester, so it is a good idea to periodically pull the
> latest changes from Git server.

The intention of the gr-cdc OOT module is to provide you with a useful baseline
link for completing the design project. You will need to expand and optimize
the functionality of this link to achieve a successful project solution.
Currently, there is a software simulation example of the CDC packet link, which
is a modified version of the GNU packet link you just investigated.

> **To Do:**  
> 6. Investigate the CDC packet transmitter example:
> `gr-cdc/examples/cdc_packet_loopback.grc`.
> Note that this example relies on two hierarchical blocks: *CDC PHY Tx*
> and *CDC PHY Rx*. The code for these blocks has already been installed with the
> rest of gr-cdc, but the GRC files can still be inspected and used to create
> modified versions if desired.
>   - `gr-cdc/examples/cdc_phy_tx.grc`
>   - `gr-cdc/examples/cdc_phy_rx.grc`

## Single-Carrier Receivers

There is no one way to design a wireless communication link. Generally,
different receivers will have subsystems that perform similar functionality
(such as framing, timing recovery, carrier recovery, equalization, and
detection), but the order of subsystems and algorithms employed are likely to
vary from receiver to receiver. The GNU Radio packet example is just one
implementation. For the CDC design project, you have the freedom to experiment
with different receiver algorithms and system designs to find the best
performance.

> **To Do:**  
> 7. Review some of the following alternatives for the transmission and
>    reception of single-carrier waveforms. Compare and contrast these examples
>    with the GNU Radio example you have already seen.
>    - [MATLAB QPSK Transceiver](https://www.mathworks.com/help/comm/ug/qpsk-transmitter-and-receiver-in-simulink.html)
>    - [LiquidDSP FlexFrame](https://liquidsdr.org/doc/tutorial-framing/)
>    - [Chapter 5 - Dealing with Impairments](https://www.oreilly.com/library/view/introduction-to-wireless/9780134431871/)<br>Health, R. Introduction to Wireless Digital Communications: A Signal Processing Perspective

You may also wish to search for other documented single-carrier implementations
that might exist.
