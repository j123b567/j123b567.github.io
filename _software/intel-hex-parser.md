---
title: Intel HEX parser
date: 2012-09-16
---

Easy to use parser of [Intel HEX](http://en.wikipedia.org/wiki/Intel_HEX) files. Project is separated in two main files. The parser itself and
dataListener. DataListener's method data is called every time new line data
line is parsered. DataListener's method eof is called once at the end of
file. Only „Data record“, „End Of File record“ and „Extended Linear
Address Record“ are currently implemented.

Demo of DataListener is included. It converts file Application.hex to
Application.bin according to selected memory range.

License: BSD 2-Clause

Source: [https://github.com/j123b567/java-intelhex-parser](https://github.com/j123b567/java-intelhex-parser)
