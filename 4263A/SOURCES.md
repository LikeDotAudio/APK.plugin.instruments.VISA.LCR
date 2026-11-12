# Sources — 4263A.komand

Every change to this table that a vendor manual confirms, with where the manual says it (AUDIO.komand `check-tables --strict` research, 2026-10-31). A finding no manual confirmed is listed under *Not confirmed* with what was searched, and the table is left as it was.

## Not confirmed (left as is)

- `set/Set_Mode` — searched: HP 4263A LCR Meter operation/programming manual: searched xdevs.com, manualmachine, manualslib, Keysight; only the successor 4263B's documents were found (User's Guide at xdevs.com, Operation Manual at manualmachine), which are not the 4263A's. The MEAS:ALL?/CURR?/POW?/VOLT? entries were authored from a panel literal and look like electronic-load commands, not LCR ones — nothing confirms them
- `set/Measurement_Function` — searched: as above
- `set/Trigger_Source` — searched: as above
- `nab/Get_Meas_All` — searched: as above
- `nab/Get_Meas_Curr` — searched: as above
- `nab/Get_Meas_Pow` — searched: as above
- `nab/Get_Meas_Volt` — searched: as above

## Retired (owner decision, 2026-10-31)

The manual shows these commands do not exist. Each entry stays in the table with `"retired": true` and its citation in `retired_because`; KOMAND never sends it, check-tables skips it, and it still counts toward the commands floor.

- `nab/Get_Meas_All` — Owner decision 2026-10-31: no HP 4263A manual was obtainable, and MEAS:ALL?/CURR?/POW?/VOLT? are the electronic-load measurement set (Electronic Load Family Programming Manual 06060-90005 p. 51), authored here from a panel literal — an LCR meter measures impedance, not load current/power
- `nab/Get_Meas_Curr` — Owner decision 2026-10-31: no HP 4263A manual was obtainable, and MEAS:ALL?/CURR?/POW?/VOLT? are the electronic-load measurement set (Electronic Load Family Programming Manual 06060-90005 p. 51), authored here from a panel literal — an LCR meter measures impedance, not load current/power
- `nab/Get_Meas_Pow` — Owner decision 2026-10-31: no HP 4263A manual was obtainable, and MEAS:ALL?/CURR?/POW?/VOLT? are the electronic-load measurement set (Electronic Load Family Programming Manual 06060-90005 p. 51), authored here from a panel literal — an LCR meter measures impedance, not load current/power
- `nab/Get_Meas_Volt` — Owner decision 2026-10-31: no HP 4263A manual was obtainable, and MEAS:ALL?/CURR?/POW?/VOLT? are the electronic-load measurement set (Electronic Load Family Programming Manual 06060-90005 p. 51), authored here from a panel literal — an LCR meter measures impedance, not load current/power

## Retired on the bench (2026-11-07)

- `nab/Measure` — Bench 2026-11-07 03:13 UTC, HP 4263A 3145J01840 fw 02.00 on gpib7,11: `:MEASure?` answered -113,"Undefined header" then -420,"Query UNTERMINATED" — the unit has no bare MEASure query; read with `:READ?` (trigger + fetch) or `:FETCh?`

## SCPI paths — every header against the model's own tree (scpi_paths.py, 2026-11-11)

The tree: `4263A.scpi.json`, read off no 4263A manual obtainable (SOURCES.md); roots from the successor 4263B User's Guide 04263-90040, Chapter 8 SCPI Command Reference. Each entry's `notes` / `retired_because` carries the full reason and page; the 33220A's Certify of 2026-11-11 (199 tries) and the GUI-certificate book are the bench evidence. Nothing was sent to verify.

| Command | Change | Was |
|---|---|---|
| `set/Set_Curr` | left as is, unverified — unresolved |  |
| `set/Set_Curr_Lev` | left as is, unverified — unresolved |  |
| `set/Set_Curr_Slew` | left as is, unverified — unresolved |  |
| `set/Set_Curr_Tlev` | left as is, unverified — unresolved |  |
| `set/Set_Inp` | left as is, unverified — unresolved |  |
| `set/Set_Mode` | left as is, unverified — unresolved |  |
| `set/Set_Res` | left as is, unverified — unresolved |  |
| `set/Set_Tran_Dcyc` | left as is, unverified — unresolved |  |
| `set/Set_Tran_Freq` | left as is, unverified — unresolved |  |
| `set/Set_Tran_Stat` | left as is, unverified — unresolved |  |
| `set/Set_Volt` | left as is, unverified — unresolved |  |
