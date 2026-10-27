# Changelog

## [1.1.0] - 2026-10-26
### Changed
- Documentation rebuilt from the captured evidence:
  - diagslave command corrected to `-m tcp -a 1 -p 1502`
  - register values corrected to the captured R0 500 / R1 1405 / R2 225
  - read node identified as `modbus-read`
  - client counters (2,072 / 2,072 / 0) and the write test recorded
### Added
- Points list, commissioning and test record, addressing note (0-based vs 40001 vs "from 1"), evidence close-ups, video section, portfolio links.
### Note
- `config/flows.json` is a placeholder until the real Node-RED export is added (see `config/README.md`).

## [1.0.0] - 2026-06-30
### Added
- Node-RED Modbus TCP flow: polled FC03 read of registers 0-9, FC06 write, scaling functions.
- diagslave simulator on port 1502, Unit ID 1.
- Cross-verification with an independent Modbus client.
### Fixed
- Connection timeouts (port, listener), Unit ID mismatch, node-trigger wiring, raw value interpretation.
