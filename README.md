# DAC8760 library for STM32

A modular **C driver for the Texas Instruments DAC8760**, designed for **STM32 microcontrollers** using the **STM32 HAL library**.

## Features

- Compatible with **STM32 HAL (SPI + GPIO)**
- 16-bit DAC control via SPI
- Support for **unipolar and bipolar output ranges**
- Software **reset** and **clear**
- Simple and portable API

## Hardware

- Texas Instruments **DAC8760**
- STM32 microcontroller
- SPI interface
- GPIOs:
  - `CS`
  - `LATCH`

## Configuration

### SPI Configuration

- Mode: **SPI Mode 0**
- Data size: **8-bit**
- Bit order: **MSB first**

## Overview

### Initialization

```c
void DAC8760_Init(DAC8760_t *dac,
                  uint16_t latch,
                  GPIO_TypeDef *port,
                  SPI_HandleTypeDef hspi);
```

### Voltage Output

```c
void DAC8760_WriteVoltage(DAC8760_t *dac, uint16_t value);
```

Register Access

```c
void DAC8760_WriteRegister(DAC8760_t *dac, uint8_t reg, uint16_t value);
uint16_t DAC8760_ReadRegister(DAC8760_t *dac, uint8_t reg);
```

### Latch Control

```c
void DAC8760_LATCH_LOW(DAC8760_t *dac);
void DAC8760_LATCH_HIGH(DAC8760_t *dac);
```

### Example Usage

```c
DAC8760_t dac;

DAC8760_Init(&dac, LATCH_Pin, LATCH_GPIO_Port, hspi1);

// Write mid-scale value
DAC8760_WriteVoltage(&dac, 0x8000);

// Toggle latch to update output
DAC8760_LATCH_LOW(&dac);
DAC8760_LATCH_HIGH(&dac);

while (1)
{
}
```

Author

Developed by Albert Kirchner
