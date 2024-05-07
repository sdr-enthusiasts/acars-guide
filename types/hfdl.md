# HFDL

## Introduction

High Frequency Data Link (HFDL) is a data link in the high frequency range (3 - 30 MHz) with virtually global coverage. HFDL is used to convey short data messages over long distances, bi-directonally between ground stations and aircraft using the [propagation effect](https://en.wikipedia.org/wiki/High_frequency) of high frequency radio waves.

16 ground stations provide redundant global coverage. There are 12 bands/groups of frequencies in the HFDL range (2 - 21 MHz), and these are covered in more detail in the frequencies section below

## Hardware

For a basic set up covering a couple of adjacent bands you can get up and running with a Raspberry Pi4, RTL-SDR v4 and a suitable HF antenna (e.g. MLA-30+). For more complete setups covering all bands all of the time a lot of CPU and USB bus bandwidth is required and a Raspberry Pi4/5 will not be sufficient in some usecases. Unless you go with an example of the high-spec computer below expect your HFDL set up to require dedicated hardware with no other SDRs and little or no additional software running on them.

### SDRs

- **RTL-SDR v4** - These are a good entry point into the world of HFDL ACARS. Cheap, with a reasonable bandwidth, but they lack the sensitivity of other HF capable devices. NOTE: The RTL-SDR v3 can do HF by direct sampling - don't waste your time.
- **SDRPlay SDR** - e.g. RSP1A/B. More expensive option, however the RSP1A are reasonably priced second hand since the introduction of the RSP1B. Both are good in the HF range with the RSP1B being better. High bandwidth and can cover lots of the bands in one go.
- **RSP1 clones** - Based on the RSP1 architecture these Chinese clones vary in price, quality and longevity. Similar performance to the RSP1A and able to cover several bands at a time.
- **AirspyHF+ Discovery** - Another step up in expense. Very high sensitivity, but low bandwidth. These will only cover one band at a time, however they will pick up messages the the other suggestions will not.

### Computers

- **Raspberry Pi 4** - A low powered entry point. Able to handle a single SDRPlay SDR running a 2 Mbps sample rate. Or a couple of RTL-SDR v4 at low sample rates. Good place to get started if you wish to monitor only a couple of bands or using a frequency switching script.
- **Raspberry Pi 5** - A mid powered entry point. Able to handle two SDRPlay devices running at 2 Mbps or one at 6 Mbps sample rate. Able to handle four RTL-SDR v4 covering bands 8 - 21 and with the use of a band switching script bands 2 - 21 (just not all at the same time - 8 - 21 during day time and 2 - 13 during night time).
- **Trigkey G4 N100** - (or similar N100 based mini PC) A higher spec mid entry point. Similar in price point to a Raspberry Pi5 with case and PSU. Able to handle two SDRPlay devices running at 6 Mbps sample rate
- **Old PC with Core i3-10 or better** - A high spec, higher cost entry point. Able to handle more than 2 SDRPlay devices. The amount will vary depending on processor and USB bus architecture. Going down this route, get the best specifications you can for the money you are prepared to spend.

### Antennas

- **MLA-30+** - An active loop antenna. Try and avoid the clones.
- **You-loop** - Passive loop antenna.
- **Longwire**

### Splitters / Multicouplers

If you wish to use more than one SDR then a splitter or multicoupler will be required. Splitters halve the signal for each split + insertion loss. Multicouplers are powered Splitters that output the same signal as received and they only incur an insertion loss. The costs of multicouplers range from low to high.

- **Simple SMA splitter wires** - Can be found most places.
- **Active RF Isolation Distributor Suitable for RF Signal Radio Antenna SDR** - A low cost battery powered splitter from Banggood. Can be run with the charging cable in all the time for continuous use . Only has four outputs.
- **Cross Country Multicoupler** - Expensive, excellent mains-powered multicoupler, 5 outputs.

## Software

### Bare metal installation

- [dumpHFDL](https://github.com/szpajder/dumphfdl) - a mature HFDL decoder. Installation instructions are found on the readme of the [dumpHFDL](https://github.com/szpajder/dumphfdl) github repo. There is also a step-by-step guide to installing SoapySDR for SDRPlay and RTL-SDR devices with instructions on installing dumpHFDL and setting up system services for auto start etc., which can be found [here](https://github.com/rikgale/hfdl_install).
- [xng](https://github.com/airframesio/xng) - a next-generation multi-decoder client for SDRs, written in Rust for Linux, Windows, MacOS.

### Docker installation

- SDR-Enthusiasts (SDR-E) [`docker-dumphfdl`](https://github.com/sdr-enthusiasts/docker-dumphfdl) - a docker wrapper for dumphfdl with a built in auto frequency selector or manual frequency selection. Assumes some prior knowledge of using [SDR-E](https://github.com/sdr-enthusiasts) docker containers and some familiarity with using soapySDR (no soapySDR installation required).

## Frequencies

### 12 Frequency bands

2, 3, 4, 5,6, 8, 10, 11, 13, 15, 17, 21.

Not all bands are active all the time and not all frequencies within the bands are in use. Consult the latest system table for current frequencies. (WORK IN PROGRESS)

```text
version = 52;
stations = (
{ id = 1; lat = 38.384587; lon = -121.759647; frequencies = ( 21934.0, 17919.0, 13276.0, 11327.0, 10081.0, 8927.0, 6559.0, 5508.0 ); name = "San Francisco, California"; },
{ id = 2; lat = 21.184428; lon = -157.186846; frequencies = ( 21937.0, 17919.0, 13324.0, 13312.0, 13276.0, 11348.0, 11312.0, 10027.0, 8936.0, 8912.0, 6565.0, 5514.0 ); name = "Molokai, Hawaii"; },
{ id = 3; lat = 63.847168; lon = -22.455754; frequencies = ( 17985.0, 15025.0, 11184.0, 8977.0, 6712.0, 5720.0, 3900.0 ); name = "Reykjavik, Iceland"; },
{ id = 4; lat = 40.881922; lon = -72.63762; frequencies = ( 21931.0, 17919.0, 13276.0, 11387.0, 8912.0, 6661.0, 5652.0 ); name = "Riverhead, New York"; },
{ id = 5; lat = -37.015757; lon = 174.809637; frequencies = ( 17916.0, 13351.0, 10084.0, 8921.0, 6535.0, 5583.0 ); name = "Auckland, New Zealand"; },
{ id = 6; lat = 6.937536; lon = 100.388451; frequencies = ( 21949.0, 17928.0, 13270.0, 10066.0, 8825.0, 6535.0, 5655.0 ); name = "Hat Yai, Thailand"; },
{ id = 7; lat = 52.744089; lon = -8.926752; frequencies = ( 11384.0, 10081.0, 8942.0, 8843.0, 6532.0, 5547.0, 3455.0, 2998.0 ); name = "Shannon, Ireland"; },
{ id = 8; lat = -26.129658; lon = 28.206078; frequencies = ( 21949.0, 17922.0, 13321.0, 11321.0, 8834.0, 5529.0, 4681.0, 3016.0 ); name = "Johannesburg, South Africa"; },
{ id = 9; lat = 71.25849; lon = -156.577447; frequencies = ( 21937.0, 21928.0, 17934.0, 17919.0, 11354.0, 10093.0, 10027.0, 8936.0, 8927.0, 6646.0, 5544.0, 5538.0, 5529.0, 4687.0, 4654.0, 3497.0, 3007.0, 2992.0, 2944.0 ); name = "Barrow, Alaska"; },
{ id = 10; lat = 35.032377; lon = 126.238644; frequencies = ( 21931.0, 17958.0, 13342.0, 10060.0, 8939.0, 6619.0, 5502.0, 2941.0 ); name = "Muan, South Korea"; },
{ id = 11; lat = 9.084681; lon = -79.373969; frequencies = ( 17901.0, 13264.0, 10063.0, 8894.0, 6589.0, 5589.0 ); name = "Albrook, Panama"; },
{ id = 13; lat = -17.671199; lon = -63.157088; frequencies = ( 21997.0, 17916.0, 13315.0, 11318.0, 8957.0, 6628.0, 4660.0 ); name = "Santa Cruz, Bolivia"; },
{ id = 14; lat = 56.152603; lon = 92.583337; frequencies = ( 21990.0, 17912.0, 13321.0, 10087.0, 8886.0, 6596.0, 5622.0 ); name = "Krasnoyarsk, Russia"; },
{ id = 15; lat = 26.308529; lon = 50.472318; frequencies = ( 21982.0, 17967.0, 13312.0, 10030.0, 8885.0, 6646.0, 5544.0, 2986.0 ); name = "Al Muharraq, Bahrain"; },
{ id = 16; lat = 13.488833; lon = 144.828233; frequencies = ( 21928.0, 17919.0, 13312.0, 11306.0, 8927.0, 6652.0, 5451.0 ); name = "Agana, Guam"; },
{ id = 17; lat = 27.960945; lon = -15.405608; frequencies = ( 21955.0, 17928.0, 13303.0, 11348.0, 8948.0, 6529.0 ); name = "Canarias, Spain"; }
);
```

## Useful links

- [dumpHFDL decoder](https://github.com/szpajder/dumphfdl) (szpajder)
- [xng decoder](https://github.com/airframesio/xng) (airframes.io)
- [Bare metal HFDL installation guide](https://github.com/rikgale/hfdl_install) (rikgale)
- [Docker HFDL installation guide](https://github.com/sdr-enthusiasts/docker-dumphfdl) (SDR-Enthusiasts)
- [Frequency selector for single SDR setups](https://github.com/wiedehopf/hfdlscript) (wiedehopf)
- [Band switcher for multi SDR setups - work in progress](https://github.com/rikgale/hfdl_band_Switch) (rikgale)
