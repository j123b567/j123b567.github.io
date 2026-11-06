---
title: Open-Source SCPI / IEEE 488.2 Parser library
lang: en
date: 2012-11-18
excerpt_separator: <!--more-->
---

SCPI parser is a C library that adds [SCPI](https://en.wikipedia.org/wiki/Standard_Commands_for_Programmable_Instruments)
and IEEE 488.2 command handling to the **instrument side**: a power supply, a
multimeter or any other device you build yourself. You define each command by
its pattern, e.g. `MEASure:VOLTage[:DC]?`, and a callback. The library does the
parsing, parameter conversion, error queue and the mandatory commands.

<!--more-->

- **Documentation:** [www.jaybee.cz/scpi-parser](https://www.jaybee.cz/scpi-parser/) –
  [basic usage](https://www.jaybee.cz/scpi-parser/basic/),
  [API reference](https://www.jaybee.cz/scpi-parser/api/),
  [version history](https://www.jaybee.cz/scpi-parser/versions/)
- **Source code:** [github.com/j123b567/scpi-parser](https://github.com/j123b567/scpi-parser)
- **License:** BSD 2-Clause

## Why it exists

At the [Department of Measurement](https://meas.fel.cvut.cz/) (CTU in Prague), I supervised several bachelor and master
students. Many of them built an instrument and then needed SCPI support for it,
and each of them started to write their own parser from scratch. Nothing usable
existed at that time, so I wrote this library and gave it to them. They could
then work on their thesis and not on routine string parsing.

Since then, more than 20 people have contributed to the library.

## Features

- Based on [SCPI-99](https://www.ivifoundation.org/downloads/SCPI/scpi-99.pdf)
  and [IEEE 488.2-2004](https://doi.org/10.1109/IEEESTD.2004.95390), tries to
  be SCPI-99 compliant as much as possible.
- One line per command: pattern and callback, no duplicate information.
- Implementation of the IEEE 488.2 mandatory commands (`*CLS`, `*ESE`, `*IDN?`,
  `*OPC`, `*RST`, `*SRE`, `*STB?`, `*TST?`, `*WAI`, …) and of the SCPI mandatory
  commands (`SYSTem:ERRor[:NEXT]?`, `STATus:QUEStionable…`, …).
- Error queue, status registers and service request (SRQ) support.
- Units and special numbers (`MIN`, `MAX`, `DEF`, `INF`, …).
- Header tree traversal: `CONF:VOLT:DC 1; AC 2` works the same as
  `CONF:VOLT:DC 1; CONF:VOLT:AC 2`.
- Portable C with no OS dependency. It compiles as C89, C99 and C++ and runs
  from small MCUs to PCs. It is also available as a
  [PlatformIO](https://platformio.org/) library and a Zephyr module.
- Unit tests and integration tests cover more than 93 % of the core library.

### Command patterns

| Feature | Pattern example |
|---------|-----------------|
| Short and long form | `MEASure` means `MEAS` or `MEASURE` |
| Common command | `*CLS` |
| Compound command | `CONFigure:VOLTage` |
| Query command | `MEASure:VOLTage?`, `*IDN?` |
| Optional keywords | `MEASure:VOLTage[:DC]?` |
| Numeric keyword suffix (multiple identical capabilities) | `OUTput#:FREQuency` matches `OUT:FREQ`, `OUT2:FREQ`, … |

### Parameter types

| Type | Example |
|------|---------|
| Decimal | `10`, `10.5` |
| Decimal with suffix | `-5.5 V`, `1.5 KOHM` |
| Hexadecimal, octal, binary | `#HFF`, `#Q77`, `#B11` |
| String | `"text"`, `'text'` |
| Arbitrary block | `#12AB` |
| Program expression | `(1)` |
| Numeric list | `(1,2:50,80)` |
| Channel list | `(@1!2:3!4,5!6)` |
| Character data | `MINimum`, `DEFault`, `INFinity` |

## Example

Each command is a pattern and a callback. The callback reads parameters and
writes results:

```c
static scpi_result_t SRC_Voltage(scpi_t * context) {
    double value;

    /* mandatory parameter, error -109 "Missing parameter" if not present */
    if (!SCPI_ParamDouble(context, &value, TRUE)) {
        return SCPI_RES_ERR;
    }

    set_output_voltage(value);
    return SCPI_RES_OK;
}

static scpi_result_t SRC_VoltageQ(scpi_t * context) {
    SCPI_ResultDouble(context, get_output_voltage());
    return SCPI_RES_OK;
}

const scpi_command_t scpi_commands[] = {
    { .pattern = "*IDN?", .callback = SCPI_CoreIdnQ,},
    { .pattern = "*RST", .callback = SCPI_CoreRst,},
    { .pattern = "SYSTem:ERRor[:NEXT]?", .callback = SCPI_SystemErrorNextQ,},
    { .pattern = "SOURce:VOLTage[:LEVel]", .callback = SRC_Voltage,},
    { .pattern = "SOURce:VOLTage[:LEVel]?", .callback = SRC_VoltageQ,},
    SCPI_CMD_LIST_END
};
```

The application provides a `write` callback for the output, initializes the
context with [`SCPI_Init`](https://www.jaybee.cz/scpi-parser/api/SCPI_Init/)
and feeds received characters from UART, USB or TCP to
[`SCPI_Input`](https://www.jaybee.cz/scpi-parser/api/SCPI_Input/). The input
does not need to contain whole commands. The library buffers it and parses
each command when it is complete. The whole setup is described in
[Basic instrument](https://www.jaybee.cz/scpi-parser/basic/instrument/).

The repository also contains [examples](https://github.com/j123b567/scpi-parser/tree/master/examples):
an interactive command line demo, a TCP server on port 5025 with and without
SRQ, a VXI-11 server, an LwIP netconn example and a LabWindows/CVI example.

## History

- **v1.0** (2013): basic command pattern matching and basic data types.
- **v2.0** (2015): parser rewritten to be more compliant with SCPI-99, all
  parameter types from the specification, arbitrary block data, optional
  keywords, header tree traversal and multiple identical capabilities.
- **v2.1** (2015): full list of SCPI error messages, LabWindows/CVI example,
  support for more compilers.
- **v2.2** (2018): bug fixes and improvements.
- **v2.3** (2024): builds as C89, C99 and C++, PlatformIO library, CI with
  GitHub Actions.

More details are in the [version history](https://www.jaybee.cz/scpi-parser/versions/)
and in the [migration guide from v1 to v2](https://www.jaybee.cz/scpi-parser/basic/migration/).
