# Carrier Synchronization

This workshop guide includes activities for lecture and workshop sessions of
week 4. Please refer to the following overview slides as needed.

- [Lecture 04 - Carrier Synchronization](https://canvas.lms.unimelb.edu.au/courses/151467/pages/lecture-04-carrier-synchronization?module_item_id=4520651)
- Workshop 04 - TBD

## 4.1: Carrier Frequency Offset

In the previous workshop on symbol synchronization, you operated a single
bladeRF device in a cabled RF loopback setup. When observing your received
constellation after timing recovery, you should have observed a fixed amplitude
and random phase rotation in the constellation points. The phase rotation
is a result of the signal propagation through the cable and random time at which
the local oscillators (LOs) are initialized. However, because the transmit and
received LOs are driven by the same underlying crystal oscillator no frequency
offset should have been present.

In this activity you will investigate the more realistic scenario in which the
transmit and receive chains run on seperate bladeRFs. As a result, there should
be a noticeable frequency offset present between the two devices. To begin,
connect two bladeRF devices together in an RF loopback setup as follows.

- Device A *TX1* port > 30 dB attenuator > Device B *RX1* port
- Device B *TX1* port > 30 dB attenuator > Device A *RX1* port

> **Note:** Although strictly speaking we only need to connect one transmit and
> receive port, for this setup we will connect both pairs. This will ensure that
> we do not accidentally damage the bladeRF by improperly selecting an  
> unterminated port in our GNU Radio flowgraph.

To configure the *Soapy BladeRF Sink* and *Soapy BladeRF Source* blocks to use
seperate bladeRF devices, we will need the corresponding device serial numbers.
These can be found either on the label on the underside of each device or
by running the following command after connecting the two devices to the host
computer via USB.

```
$ bladeRF-cli -p

  Description:    Nuand bladeRF 2.0
  Backend:        libusb
  Serial:         7674de4e4e284095801f09c859cb921c
  USB Bus:        4
  USB Address:    14

  Description:    Nuand bladeRF 2.0
  Backend:        libusb
  Serial:         fe9539e140b049e8b348ac8c88f5dbd9
  USB Bus:        4
  USB Address:    13
```

For a given *Soapy BladeRF* block, you can specify which bladeRF device it
should connect to by setting the parameter *Device arguments:* to be
`serial=<serial number>`. Here, you only need to enter enough initial digits of
the bladeRF's serial number to uniquely identify it, e.g., you could specify the
first device listed above by entering `serial=7674`.

Create the GNU Radio flowgraph shown in the figure below, which you will use to
measure the frequency offset between the two bladeRF devices. For the
*QT GUI Time Sink* set the *Number of points* parameter to be `n_fft` and
*Autoscale* to be `Yes`.

> **Note:** Please make sure to enter *DIFFERENT* serial numbers for the sink
> and source blocks.

<div align="center">

![Frequency offset flowgraph](images/w4_1a_flowgraph.png)

</div>

Run your flowgraph and determine the frequency offset between the two devices.
You should be able to determine this parameter based on the FFT bin with the
largest magnitude and the frequency of the *Signal Source* block.

> **FLUX Question:**  
> 1. What frequency offset do you measure between the two bladeRF devices?

Now that we have a measurement of the frequency offset between the two devices,
let's verify the impact on our received constellation. Modify your symbol
synchronization flowgraph of [Workshop 3](Workshop_3.md) to use separate
bladeRFs to transmit and receive. Run your flowgraph.

> **FLUX Question:**  
> 2. How does the frequency offset affect the received symbol constellation?

Although for a phase modulation such as QPSK we do not strictly need to
normalize the amplitude levels of the received constellation, this is a
requirement for proper operation of the feedback loops used in both symbol and
carrier synchronization. To do so we will add automatic gain control prior to
the matched filter block in our flowgraph. Include a *Feedforward AGC* block
after the *Soapy BladeRF Source* block in your flowgraph.

<div align="center">

![Two device pulse modulation](images/w4_1b_flowgraph.png)

</div>

Experiment with the *Reference level* parameter of the *Feedforward AGC* block
until your received symbol constellation has unit amplitude. <br>**Note:**
*Reference level* cannot be changed during flowgraph execution.

> **FLUX Question:**  
> 3. What reference level do you need to set to obtain the desired QPSK
>    constellation scaling?

## 4.2 Costas Loop

To correct for the frequency offset in our received constellation we will add a
*Costas Loop* carrier recovery block to our flowgraph. See the figure below
for the proper configuration. The Costas implementation in GNU Radio is a
*decision directed* PLL supporting BPSK, QPSK, and 8-PSK constellations. To
configure the constellation set the *Order* parameter to be the modulation order
of QPSK. The *Costas Loop* in GNU Radio is a critically damped ($\zeta = 1$)
PLL for which you can specify the normalized loop bandwidth.

> **FLUX Question:**  
> 4. Choose a loop bandwidth for the *Costas Loop* block based on the frequency
>    offset measured in Activity 4.1.

<div align="center">

![Costas loop carrier recovery](images/w4_2_flowgraph.png)

</div>

Run your flowgraph and verify that the received constellation after carrier
recovery is now stationary. Experiment with the loop bandwidth to see if there
is an impact on the measured EVM. At what loop bandwidth is the loop no longer
able to acquire an initial frequency lock?

> **FLUX Question:**  
> 5. What EVM do you measure for your choice of loop bandwidth?
> 6. At what loop bandwidth value can you no longer acquire an initial
>    frequency lock?
