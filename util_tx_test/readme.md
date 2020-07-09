	 / _____)             _              | |    
	( (____  _____ ____ _| |_ _____  ____| |__  
	 \____ \| ___ |    (_   _) ___ |/ ___)  _ \ 
	 _____) ) ____| | | || |_| ____( (___| | | |
	(______/|_____)_|_|_| \__)_____)\____)_| |_|
	  (C)2013 Semtech-Cycleo

LoRa concentrator packet sender
================================

1. Introduction
----------------

This software is used to send test packets with a LoRa concentrator. The packets
contain little information, on no protocol (ie. MAC address) information but
can be used to assess the functionality of a gateway downlink using other
gateways as receivers.

2. Dependencies
----------------

This program is a typical example of LoRa concentrator HAL usage for sending
packets.

Only high-level functions are used (the ones contained in loragw_hal) so there
is no hardware dependencies assuming the HAL is matched with the proper version
of the hardware.
Data structures of the sent packets are accessed by name (ie. not at a
binary level) so new functionalities can be added to the API without affecting
that program at all.

3. Usage
---------

The application runs until the specified number of packets have been sent.
Press Ctrl+C to stop the application before that.

Use the -h to get help and details about available options.

The payload content is:
[T][E][S][T][packet counter MSB][packet counter LSB] followed by ASCII padding.

All LoRa data is scrambled and whitened, so the padding has no influence
whatsoever on the packet error rate.

```   
util_tx_test -h
 -h                 print this help
 -r         <int>   radio type (SX1255:1255, SX1257:1257)
 -n         <uint>  TX notch filter frequency in kHz [126..250]
 -f         <float> target frequency in MHz
 -k         <uint>  concentrator clock source (0:Radio A, 1:Radio B)
 -m         <str>   modulation type ['LORA', 'FSK']
 -b         <uint>  LoRa bandwidth in kHz [125, 250, 500]
 -s         <uint>  LoRa Spreading Factor [7-12]
 -c         <uint>  LoRa Coding Rate [1-4]
 -d         <uint>  FSK frequency deviation in kHz [1:250]
 -q         <float> FSK bitrate in kbps [0.5:250]
 -p         <int>   RF power (dBm) [ 0dBm 10dBm 14dBm 20dBm 27dBm ]
 -l         <uint>  LoRa preamble length (symbols)
 -z         <uint>  payload size (bytes, <256)
 -i                 send packet using inverted modulation polarity
 -t         <uint>  pause between packets (ms)
 -x         <int>   nb of times the sequence is repeated (-1 loop until stopped)
 --lbt-freq         <float> lbt first channel frequency in MHz
 --lbt-nbch         <uint>  lbt number of channels [1..8]
 --lbt-sctm         <uint>  lbt scan time in usec to be applied to all channels [128, 5000]
 --lbt-rssi         <int>   lbt rssi target in dBm [-128..0]
 --lbt-rssi-offset  <int>   rssi offset in dB to be applied to SX127x RSSI [-128..127]
'''   
   
'''   
util_tx_test -r 1257 -f 866.5 --lbt-freq 866.5
util_tx_test -r 1257 -f 866.5 -k 0 -m LORA
  
util_tx_test -r 1257 -f 915  -m LORA
util_tx_test -r 1257 -f 915 --lbt-freq 915 -m LORA

util_tx_test -r 1257 -f 923.3  -m LORA
util_tx_test -r 1257 -f 923.3 --lbt-freq 915 -m LORA
```   

4. License
-----------

Copyright (c) 2013, SEMTECH S.A.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright
  notice, this list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright
  notice, this list of conditions and the following disclaimer in the
  documentation and/or other materials provided with the distribution.
* Neither the name of the Semtech corporation nor the
  names of its contributors may be used to endorse or promote products
  derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL SEMTECH S.A. BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

*EOF*
