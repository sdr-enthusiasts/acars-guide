# VDL-M2

## Introduction

VDL-M2 is a digital data link protocol used for communication between aircraft and ground stations. It is the most common format for VHF ACARS messages. It was developed in the 1990s and is used by many airlines around the world. VDL-M2 is used for a variety of purposes, including sending messages to and from aircraft, sending weather information, Controller Pilot Data Link Connection (CPDLC) and sending flight plans. VDL-M2 messages are sent over VHF radio frequencies, and can be received by anyone with the right equipment.

## Hardware

* SDR. Any SDR that can receive VHF frequencies will work. The RTL-SDR is a popular choice.
* Antenna. A VHF antenna is required to receive ACARS messages.

## Software

* `vdlm2dec`. `vdlm2dec` is an older VDL-M2 decoder that can be used to decode VDL-M2 messages. It is available for Linux, MacOS, and Windows. Depending on your choice of operating system you may need to compile it yourself. If you prefer the "easy button" there is an available [Docker image](http://github.com/sdr-enthusiasts/docker-vdlm2dec) that you can use. One of the main limitations of using `vdlm2dec` is that certain message types, such as CPDLC, may not include all of the information that is available in the message.

* `dumpvdl2`. `dumpvdl2` is a newer VDL-M2 decoder that can be used to decode VDL-M2 messages. It is available for Linux, MacOS, and Windows. Depending on your choice of operating system you may need to compile it yourself. If you prefer the "easy button" there is an available [Docker image](http://github.com/sdr-enthusiasts/docker-dumpvdl2) that you can use. `dumpvdl2` is a more modern decoder than `vdlm2dec` and is able to decode more message types, such as CPDLC.

## Frequencies
