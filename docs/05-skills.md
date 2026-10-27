# 05 · Skills Demonstrated

[← Back to README](../README.md)

| BMS / controls skill | How this project shows it |
|---|---|
| Modbus TCP integration | Node-RED master with a polled FC03 read and an FC06 write |
| Register maps and addressing | Points list, 0-based vs 40001 vs "from 1" explained |
| Engineering units | Documented ÷10 scaling into °C and V |
| Independent verification | Second client polling the same slave: 2,072 Tx / 2,072 Rx / 0 errors |
| Fault finding | Port, Unit ID, listener and node-trigger faults |
| Safe practice | Simulator first; no live plant written to |
| Handover documentation | Points list, commissioning record and issues log in BMS handover style |
