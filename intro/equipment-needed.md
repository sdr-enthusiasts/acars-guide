# Equipment Needed

## Computer equipment

### Single-board computer

ACARS software can be compiled to run on many types of hardware. To create a stand-alone station that will be running 24/7, most users will choose a single-board computer (like a Raspberry Pi) or a Linux x86 machine (for example, an Intel NUC or Dell OptiPlex). You will want to run a 64-bits Debian Linux version on this machine, for example Raspberry Pi OS, DietPi, or Ubuntu. Alternatively, you can use a Linux laptop or a virtualized environment, as long as this environment reliably handles high-speed USB data.

You can also add your ACARS/VDL-M2 receiver to your existing ADSB device:

- due to power limitations, Raspberry Pi devices can only handle up to 3 SDRs unless you use a powered USB hub
- a Raspberry Pi 4 with 3 SDRs for ADSB, ACARS, and VDL-M2 reception can be used safely and without stability issues
- x86 devices generally have more power available on their USB bus and can handle more than 3 SDRs
- lower-end devices, like Raspberry Pi 3B+, Raspberry Pi Zero 2, etc. will often run into CPU and memory limitations when using them for ADSB + ACARS + VDL-M2.
- You can safely configure a Raspberry Pi 3B+ as "stand-alone" for only ACARS and VDL-M2, as long as that device doesn't do too many extra, CPU-intensive tasks

A monitor and keyboard for your SBC are optional - once your OS is installed, you can configure, run, and monitor your station from the command-line or via a web browser.
You do not need to install a Desktop on your Linux machine*.

*) An exception to this is if you want to use your station for Iridium or Inmarsat ACARS reception - you will need to determine the frequency deviation of your device using a graphics tool that can only run on a desktop. However, this is a "far advanced" use case and most users won't need this initially

### SD-Cards

Since ACARS is data-intensive, if your SBC uses an SD card for storage (Raspberry Pi, etc), we recommend to get a high quality and very large SD card that is optimized for endurance. Each sector on an SD card has a limited number of writes that determine its lifespan. Linux writes to SD cards in a random fashion, so the larger the SD card, the lower the probability that the same sector is overwritten, the longer the theoretical lifespan. 128 Gb or larger SD cards are best; we recommend a minimum SD card size of 64 Gb. (Note that the storage space for `OS + ACARS/VDL-M2 software + data` is probably in the 10 - 20 Gb range, so yes - we are recommending SD memory that is much larger than the expected disk use.)

### Internet connection

A good internet connection is recommended if you share your data with aggregators. Generally, we have found WiFi to be unreliable at times, and we recommend a wired ethernet connection to your router.

## Software Defined Radios and accessories

### SDRs

The ACARS/VDL-M2 and related receivers generally use the [Pothosware SoapySDR](https://github.com/pothosware/SoapySDR) frontend to get data from your SDR, and any SDRs that are [supported by SoapySDR](https://github.com/pothosware/SoapySDR/wiki) (and that are suitable for use in the VHF bands) can be used.

The simplest solution is to get one or more RTL-SDR compatible SDRs. Make sure that the SDR is suitable for reception in the VHF (130 MHz) band: some SDRs contain filters that make them usable for a specific frequency range only. Unless you are SURE they can be used for ACARS, we would avoid them. Although we do not make recommendations for any specific SDR, here are a few models that we know will work:

- [RTL-SDR Blog v3]([RTL-SDR Blog](https://www.rtl-sdr.com/v3/))
- [RTL-SDR Blog v4](https://www.rtl-sdr.com/v4/)
- [ADSBExchange Orange](https://store.adsbexchange.com/collections/frontpage/products/adsbexchange-com-orange-r860-rtl2832u-0-5-ppm-tcxo-sdr-w-amp)
- any of the [NooElec NESDR SDRs](https://www.nooelec.com/store/sdr.html)
- Cheaper no-name or other brand RTL-SDR devices may work as well. We recommend devices that have a TXCO on board and that have a clock precision of 1 PPM or better

Specific SDRs you should avoid include because they contain band-pass filters that block ACARS/VDL-M2 frequencies:

- FlightAware Pro+ (blue)
- Radarbox Green or Red SDRs
- ADSBExchange Blue

Additionally, we've seen users use the following (non-RTL-SDR) devices:

- SDRPlay devices like the RSP-1A and RSP-1B - these work "OK" as they need an additional driver to be installed; for some users, this driver has had stability issues that caused the station to lose connectivity at random intervals.
- AirSpy SDRs - recommended if you want to do HFDL (shortwave ACARS reception)

### How many SDRs do you need

Each SDR is generally limited to receive 2 MHz of bandwidth once deployed. ACARS and VDL-M2 are generally found in the 130-132 MHz band and the 136-138 MHz band. Also, the ACARS and VDL-M2 receiver applications each expect their own, dedicated SDR(s). As a result, we see many people deploying 2 SDRs: 1 for ACARS reception in the 130-132 MHz band, and 1 for VDL-M2 reception in the 136-138 MHz band.
If you have only 1 SDR you can dedicate to ACARS/VDL-M2 reception, you should consider dedicating it to VDL-M2 because this is the "newer" protocol to which many airlines are switching. In North America, we see a reasonably equal mix between ACARS and VDL-M2 messages, with slightly more ACARS messages than VDL-M2. In Europe, most messaging (around 90%) is done using VDL-M2.

### Low Noise Amplifiers

Sometimes it's desired to have a LNA (low noise amplifier) between your SDR and your antenna. Some SDRs (for example the [ADSBExchange Orange](https://store.adsbexchange.com/collections/frontpage/products/adsbexchange-com-orange-r860-rtl2832u-0-5-ppm-tcxo-sdr-w-amp)) have a built-in LNA. If your SDR doesn't have a built-in LNA, you can optionally consider to add one between your SDR and your antenna.

We don't have a recommendation for a specific LNA model. We have seen people successfully use NooElec LNAs and cheap AliExpress LNAs. You should be careful to assess a few characteristics when using an LNA:

- Noise figure: this is the amount of noise that a LNA adds to the signal, even when nothing is received
- Overmodulation: some of the cheaper LNAs will suppress your ACARS signal if there is a strong signal close to the one you are trying to receive. You may want to consider a filter in this case; see [below](#filters)
- Some of the cheap LNAs appear to insert a lot of noise on the antenna-side of the device. This is normally not an issue, but if you use a splitter to send the signal from a single antenna to multiple devices, please be cognizant that your other devices may receive this noise. In this case, we would recommend inserting the LNA between the splitter and the antenna rather than between the SDR and the splitter.

Your LNA must be powered. Some LNAs have a micro-USB connector to supply power, other LNAs have can be powered from the SDR: this is called "Bias-T" or "Bias-Tee" powering. If you want to use this, make sure your SDR supports Bias-Tee (the RTL-SDR Blog v3/v4 and the SmarTee family of NooElec support this).

### Filters

For most stations, filters aren't necessary; however if you live close to an FM radio transmitter or in a dense urban environment, a filter may help avoiding overmodulation, especially when combined with a LNA. In this case, you may consider adding a filter that suppresses the FM Radio band. Note that ACARS and VDLM uses the 130 MHz - 137 MHz frequency band and your filter should NOT filter out these frequencies.

Note -- the [NooElec Sawbird+ NOAA](https://www.nooelec.com/store/sdr/sdr-addons/sawbird/sawbird-plus-noaa-308.html) is NOT suitable for use with ACARS, but may work with VDL-M2 reception.

### Antenna

Your antenna is one of the most important parts of your station. The range and message rate you can receive is directly dependent on the quality of your antenna, and how high and unobstructed it is mounted.

- For ACARS/VDL-M2, you need an antenna with vertical polarization that is optimized for the 130 MHz - 140 MHz frequency band. Antennas for Airband VHF reception will work, and antennas optimized for ACARS/VDL-M2 reception are perfect. Wideband antennas (like Discone antennas) may work as well, even though their gain is limited
- For HFDL, you need a HF antenna suitable for the frequencies you are receiving. (We will elaborate on this in the future)
- For SatCom / Jaero ACARS, you need an Inmarsat or Iridium antenna depending which satellite you are trying to receive. (We will elaborate on this in the future)

### Coax cable

Your SDR and your antenna generally have an impedance of 50 Ohms. As such, you should use a good quality 50 Ohms coax cable.

Signal loss because of long coax cables is still a factor for ACARS/VDL-M2 on 130 MHz, but less so than using the same coax for ADSB at 1,090 MHz or for ACARS via satellite on even higher frequencies. Even so, the shorter the coax and the fewer the losses, the better your signal! For your reference, [here is a table](http://rfelektronik.se/manuals/Datasheets/Coaxial_Cable_Attenuation_Chart.pdf) that allows you to compare the losses of coax; use the 148-174 MHz column as your guideline.

If you are willing to accept some losses, you can use a 75 Ohms (white TV) coax cable for ACARS/VDL-M2, but please note that this is sub-optimal. Your additional loss for using 75 Ohms coax is about 1.1 dB / 100 ft (30.1 m). Also note that white TV coax is generally not designed for outdoor use and the white plastic enclosure will deteriorate in sunlight.

Note that you cannot use your ADSB antenna for ACARS/VDL-M2 reception!

As always, the key to a successful station is your antenna. The better your antenna, the higher your antenna is mounter, and the fewer obstructions (houses, mountains, etc.) around your antenna, the better your reception will be.

### Use of splitters

If you have multiple SDRs in use for ACARS/VDL-M2/Airband that you want to connect to a single antenna using a splitter, please note that you will lose 3.5 dB (or half) of the signal for each split. 3-way splitters are often (internally) configured as 2x 2-way splitters, so 1 output will have 3.5 dB signal loss (only 50% of the signal left), and 2 outputs will have 7 dB signal loss (only 25% of the signal left). In this case, we recommend placing a LNA between the splitter and the antenna to mitigate some of the signal loss.

## Bill of Materials

This is a summary of the hardware you need to start receiving ACARS and VDL-M2 messages. This is for a "Minimally Viable Setup", receiving ACARS and VDL-M2 data directly from aircraft in the 130-138 MHz band:

- SBC (Raspberry Pi 4, NUC, Dell OptiPlex, etc.) with Debian Linux
  - Some SBCs do not have built-in storage, and you will need to add a SD card or SSD
  - A power supply for your SBC
- SDR(s) - 1 for ACARS, 1 for VDL-M2
- Optionally - a LNA
- Optionally - a splitter so you can use 1 antenna with both SDRs
- Antenna for 130-138 MHz
- Coax to connect the antenna to your station
