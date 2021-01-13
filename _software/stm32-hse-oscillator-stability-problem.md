---
title: STM32 HSE oscillator stability problem
date: 2017-05-02
---

I have implemented support for Precise Time Protocol in STM32 and it still
performed bad. After some investigation, I have descovered stability problems
of HSE.

I have reported these problems to the ST, they have confirmed this behavior
but unfortunately, it does not appear in any errata of SMT32 line. The problem
was discovered on STM32F107 and later confirmed on STM32F207 and STM32F407.

<figure>
  <img src="/images/stm32-xtal/stm32-xtal-test.svg" alt="" />
  <figcaption>STM32 HSE test connection</figcaption>
</figure>

I used several evaluation boards with ST's MCU. I did just internal
connection of HSE directly to MCO output of the microcontroller so no PLL was
used. The program in the MCU performs just infinite loop after configuring the
MCO. Using MCO also enables measurement of other clock sources and I was able
to connect frequency counter directly to the microcontroller.

I was measuring frequency every second and storing it using GPIB and SCPI to
the PC. After some minutes there ware enough data. The base frequency of the
oscillator was <em>24999407,7 Hz</em>, but it was not stable! I assumed, thet
there would be visible just temperature drift but it was not true. Measured
frequency was hopping within several Hz. Depending on X-tal, these spikes ware
from 2 Hz to 8 Hz.

<figure>
  <img src="/images/stm32-xtal/stm32freq.svg" alt="" />
  <figcaption>STM32 HSE instability<br />(base frequency 24999407,7 Hz)</figcaption>
</figure>

I did't perform any tests of HSI, but for precise time, RC oscillator was
no-go anyway for me.

Only solution for this was to use complete external oscillator at 25 MHz
that was stable enough. With external oscillator, I was able to reach expected
performance of the Precise Time Protocol.

Also others confirmed this behaviour [https://blog.dan.drown.org/gps-module-measurements/](https://blog.dan.drown.org/gps-module-measurements/)
