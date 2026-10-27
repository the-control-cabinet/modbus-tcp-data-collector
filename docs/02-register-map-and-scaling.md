# 02 · Register Map, Points List and Scaling

[← Back to README](../README.md) · Data: [`data/register-map.csv`](../data/register-map.csv)

## Points list

| Point | Register (0-based) | 4xxxx ref | FC | Type | Scale | Units | Access | Raw seen | Engineering value |
|---|---|---|---|---|---|---|---|---|---|
| Temperature | 0 | 40001 | 03 / 06 | UINT16 | ÷10 | °C | R/W | 500 (0x01F4) | 50.0 °C |
| Voltage | 1 | 40002 | 03 | UINT16 | ÷10 | V | R | 1405 (0x057D) | 140.5 V |
| Sensor 3 | 2 | 40003 | 03 | UINT16 | ×1 | raw | R | 225 (0x00E1) | 225 |
| Spare | 3-9 | 40004-40010 | 03 | UINT16 | n/a | n/a | R | 0 | n/a |

These are simulator test values, chosen to exercise scaling. They don't represent real plant.

## Why scaling is needed

A holding register is a single **16-bit integer** (0-65,535 unsigned). Devices send decimals by agreeing a fixed scale. For example, 22.5 °C is sent as 225, with "÷10" written in the device's register map. The integration engineer's job is to apply that agreed scale and record it, so the next person doesn't have to guess.

## Addressing: one register, three names

The same first holding register appeared under three different numbers in this lab:

| Where | It was called | Convention |
|---|---|---|
| Node-RED and the client's request | **0** | Protocol (PDU) address, 0-based |
| The client's "Alias" column | **400001** | Classic Modicon reference (4 = holding register, then 1-based) |
| diagslave console | **"from 1"** | 1-based register number |

On site, mixing these up gives a classic **off-by-one**. The values look plausible but come from the neighbouring register. The [water metering project](https://github.com/the-control-cabinet/mains-water-metering-modbus-rtu/blob/main/docs/06-issues-and-lessons-learned.md) hit exactly this on a real meter, where the manual numbered registers from 1. Always confirm which convention a register map uses.

## Function codes

| FC | Name | Used here |
|---|---|---|
| 03 | Read Holding Registers | ✅ polled read of 0-9 |
| 06 | Write Single Register | ✅ write to register 0 |
| 16 | Write Multiple Registers | Noted; on the roadmap |
| 04 | Read Input Registers | Not used (read-only measurement registers on many devices) |
