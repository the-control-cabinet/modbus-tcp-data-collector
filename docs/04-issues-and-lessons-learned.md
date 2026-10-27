# 04 · Issues and Lessons Learned

[← Back to README](../README.md)

Each issue is written up as symptom → cause → fix → lesson.

### 1. Connection timeouts
- **Symptom:** "timeout" in Node-RED and in the client.
- **Cause:** wrong port, simulator not yet running, or local firewall.
- **Fix:** start diagslave first and use port **1502** during development.
- **Lesson:** check that something is actually listening before debugging the master.

### 2. Unit ID mismatch
- **Symptom:** connected, but no data or an exception.
- **Cause:** master set to Unit ID 0 or 2 while the slave was 1.
- **Fix:** Unit ID 1 on both sides.
- **Lesson:** this is the most common reason a "working" link returns nothing. On Modbus TCP the Unit ID still matters, especially behind gateways.

### 3. Simulator not listening
- **Symptom:** immediate timeout.
- **Fix:** launch with `diagslave -m tcp -a 1 -p 1502` and confirm that its console logs the connection.

### 4. Inject didn't drive the read
- **Symptom:** pressing inject made no difference to the polled values.
- **Cause:** the `modbus-read` node polls on its own timer, so it doesn't need or use an inject. Message-driven reads need a getter-type node.
- **Fix:** keep the timed read for polling and use inject only on the write path.
- **Lesson:** know which nodes are timer-driven and which are message-driven before wiring.

### 5. Local binding / firewall
- **Symptom:** intermittent failures.
- **Fix:** connect to 127.0.0.1 explicitly.

### 6. Raw numbers with no meaning
- **Symptom:** 500, 1405 and 225 on screen.
- **Fix:** a scaling function (÷10) plus a documented points list.
- **Lesson:** scaling is part of the integration, and it belongs in the register map, not in someone's head.

## Transferable field lessons

- Most Modbus faults are configuration: IP or port, Unit ID, addressing offset, baud and parity on RTU, word order on 32-bit values. Broken hardware is rarer.
- Always verify with a **second, independent client** before blaming the BMS or the device.
- Record the register map, scaling and numbering convention before leaving the bench.
