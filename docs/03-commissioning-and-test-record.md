# 03 · Commissioning and Test Record

[← Back to README](../README.md)

**System:** Modbus TCP lab · **Slave:** diagslave, Unit 1, 127.0.0.1:1502 · **Masters:** Node-RED (`node-red-contrib-modbus`) and an independent Modbus client · **Date:** 30 June 2026

| # | Test | Method | Expected | Result | Pass |
|---|---|---|---|---|---|
| 1 | Slave listening | Start diagslave, then connect a master | Console logs the connection | `accepting connection from 127.0.0.1` | ✅ |
| 2 | Independent read | Client: FC03, start 0, qty 10, poll 1 s | 10 values, no errors | R0 500, R1 1405, R2 225, R3-9 0 | ✅ |
| 3 | Comms reliability | Client counters during continuous polling | Rx = Tx, 0 errors | **Tx 2,072 / Rx 2,072 / Err 0** | ✅ |
| 4 | Node-RED read | `modbus-read` 0-9 every 1,000 ms | Node shows active; debug payload every second | `active (1000 msec.)`; payload each second | ✅ |
| 5 | Scaling | Compare debug output with raw values | 500 → 50.0; 1405 → 140.5 | temperature 50, voltage 140.5, sensor3 225 | ✅ |
| 6 | Write and read back | Client: FC06, register 0 = 500 | Node-RED shows 50.0 on the next poll | temperature 50 | ✅ |
| 7 | Shared register image | Both masters on the same slave | Identical raw values | Client table = Node-RED `raw` | ✅ |
| 8 | Fault: wrong port | Change the master port | Timeout; recovers when corrected | Timeout → recovered | ✅ |
| 9 | Fault: wrong Unit ID | Change the master Unit ID | No response; recovers when corrected | No data → recovered | ✅ |

**Evidence:** tests 1-7 are visible in [images/project-1-screenshot.png](../images/project-1-screenshot.png), which shows the flow, the debug sidebar, the diagslave console and the client's table and counters in one capture. Close-ups are in [images/](../images/). Tests 8-9 were done during the build and have no screenshot.

**Sign-off notes:** values are simulator test data. No real plant was connected or written to.
