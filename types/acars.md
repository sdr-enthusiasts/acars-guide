# ACARS

## Introduction

ACARS is the oldest protocol for aircraft communications. It was developed in the 1970s and is still in use today. ACARS is used for a variety of purposes, including sending messages to and from aircraft, sending weather information, and sending flight plans. ACARS messages are sent over VHF radio frequencies, and can be received by anyone with the right equipment.

Typically, if you have limited SDRs available, you will want to focus on VDL-M2 as VDL-M2 is the newer protocol and is used by more airlines. Additionally, outside of the United States ACARS is typically much less used than VDL-M2.

## Hardware

* SDR. Any SDR that can receive VHF frequencies will work. The RTL-SDR is a popular choice.
* Antenna. A VHF antenna is required to receive ACARS messages.

## Software

* `acarsdec`. `acarsdec` is a popular ACARS decoder that can be used to decode ACARS messages. It is available for Linux, MacOS, and Windows. Depending on your choice of operating system you may need to compile it yourself. If you prefer the "easy button" there is an available [Docker image](https://github.com/sdr-enthusiasts/docker-acarsdec) that you can use.

## Frequencies
