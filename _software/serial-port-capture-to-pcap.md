---
title: Serial port PCAP capture tool not just for Modbus/RTU
lang: en
date: 2017-03-24
---

This tool can capture serial port traffic and store all data in PCAP format.
It is later possible to open it in Wireshark and analyze it.

This tool was created to capture Modbus/RTU on RS-485, but it can be used for
any other similar traffic.

It is available on my GitHub: [https://github.com/j123b567/SerialPCAP](https://github.com/j123b567/SerialPCAP)

A tutorial on using this tool is on YouTube: [https://www.youtube.com/watch?v=YtudbhexPv8](https://www.youtube.com/watch?v=YtudbhexPv8)

The tool is command-line only: `usage: serialpcap <portName> [<baudRate> [<frameGapMs>]]`

 - `portName` is the name of the port, e.g. COM1, /dev/ttyUSB0, …
 - `baudRate` is the speed of the serial port (default 9600)
 - `frameGapMs` is the gap between frames in ms (default 10)

It is possible to run this tool using Mono on Linux or using the .NET Framework
on Windows.