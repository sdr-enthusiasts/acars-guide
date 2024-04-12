# HFDL

## Introduction
High Frequency Data Link (HFDL) is a data link in the high frequency range (3 - 30MHz) with virtually global coverage. HFDL is used to convey short data messages over long distances, bi-directonally between ground stations and aircraft using the [propagation effect](https://en.wikipedia.org/wiki/High_frequency) of high frequency radio waves.

16 ground stations provide redundant global coverage. There are 12 bands/groups of frequencies in the HFDL range (2 - 21MHz), and these are covered in more detail in the Frequenices section below

## Hardware

For a basic set up covering a couple of adjacent bands you can get up and running with a Raspberry Pi4, RTL-SDR v4 and a suitable HF antenna (e.g. MLA-30+). For more complete setups covering all bands all of the time a lot of CPU and USB bus bandwidth is required and a Raspberry Pi4/5 will not be sufficient in some usecases. (To be discussed futher - WORK IN PROGRESS)

## Software

- [dumpHFDL](https://github.com/szpajder/dumphfdl) - a mature HFDL decoder. Installation instructions are found on the readme of the [dumpHFDL](https://github.com/szpajder/dumphfdl) github repo. There is also a step-by-step guide to installing SoapySDR for SDRPlay and RTL-SDR devices with instrctions on installing dumpHFDL and setting up system services for auto start etc., which can be found [here](https://github.com/rikgale/hfdl_install).
- [xng](https://github.com/airframesio/xng) - a next-generation multi-decoder client for SDRs, written in Rust for Linux, Windows, MacOS.

## Frequencies

#### 12 Frequency bands.
Not all bands are active all the time and not all frequencies are in use. Consult the latest system table for current frequencies (WORK IN PROGRESS)

## Useful links
- [dumpHFDL decoder](https://github.com/szpajder/dumphfdl) (szpajder)
- [xng decoder](https://github.com/airframesio/xng) (airframes.io)
- [Baremetal HFDL installation guide](https://github.com/rikgale/hfdl_install) (rikgale)
- [Docker HFDL installation guide](https://github.com/sdr-enthusiasts/docker-dumphfdl) (SDR-Enthusiasts)
