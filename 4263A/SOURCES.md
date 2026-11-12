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

## Owner's expected parameters (2026-11-11)

Added from the owner's pasted list of expected LCR commands and a pasted pyvisa nab script — neither is a manual, so every entry is `unverified` until the unit answers it alone (REMOTE first, one exchange in flight, `SYST:ERR?` after each). Nothing was sent.

| Command | Change | Source |
|---|---|---|
| `set/Set_Test_Frequency` | `:SENSe:FREQuency` → `:SOURce:FREQuency` | the test oscillator is a SOURce setting (4263B 04263-90040 ch. 8 `:SOURce:FREQuency[:CW]`, recalled) |
| `set/Primary_Parameter`, `set/Secondary_Parameter` + `Get_` twins | added `:CALCulate1/2:FORMat` | 4263B ch. 8, recalled, not confirmed |
| `set/Impedance_Type` + `nab/Get_Impedance_Type` | added `:SENSe:FUNCtion:IMPedance:TYPE` | owner's list — 4284A/E4980A-style, may answer -113 |
| `set/Set_Test_Current` + `Get_Test_Current` | added `:SOURce:CURRent` | owner's list |
| `set/Init_Continuous` + `Get_Init_Continuous` | added `:INITiate:CONTinuous` | owner's list |
| `set/Correction_Open_State`, `set/Correction_Short_State` + `Get_` twins | added `:SENSe:CORRection:OPEN/SHORt:STATe` | owner's list |
| `nab/Get_Measurement_Function`, `Get_Test_Frequency`, `Get_Test_Level`, `Get_Trigger_Source` | added readbacks of existing sets | owner's nab script |
| `nab/Learn_Settings` | added `*LRN?` | owner's nab script — if it answers alone it is the whole-state nab |
| `nab/Self_Test` | added `*TST?` | owner's list — runs a self-test; never stacked into a GRAB or asked on open |
| `nab/Measure_Impedance` | added **retired** `:MEASure:IMPedance?` | bench 2026-11-07: MEASure answers -113 and is no root in `4263A.scpi.json`; read with `:READ?` / `:FETCh?` |

Not added: `FUNCtion:IMPedance:AUTO` (no such header on either family; autorange is a RANGe:AUTO), bare `FREQ`/`VOLT` (ambiguous; the SOURce forms above). The panel's electronic-load bindings (`unresolved` in `4263A.scpi.json`) are untouched.

## Bench check (2026-11-12 03:07–03:08 UTC)

HP 4263A 3145J01840 fw 02.00 on gpib7,11. Each query asked alone through `/api/instrument/send` (the recorder's one-exchange gate), `SYST:ERR?` after each. Only queries were sent; no setting was changed.

| Query | Answer | Table |
|---|---|---|
| `:SENS:FUNC?` | `"FADM"` | `Get_Measurement_Function` verified |
| `:CALC1:FORM?` / `:CALC2:FORM?` | `CP` / `D` | `Get_Primary_Parameter` / `Get_Secondary_Parameter` verified |
| `:SOUR:FREQ?` | `+1.00000E+03` | `Get_Test_Frequency` verified (so the SOURce move was right) |
| `:SOUR:VOLT?` | `+1.00000E+00` | `Get_Test_Level` verified |
| `:TRIG:SOUR?` | `INT` | `Get_Trigger_Source` verified |
| `:INIT:CONT?` | `1` | `Get_Init_Continuous` verified |
| `*LRN?` | 18 settings, `;`-separated | `Learn_Settings` verified — the whole-state nab, never stacked |
| `*IDN?` | `HEWLETT-PACKARD,4263A,3145J01840,02.00` | `Read_IDN` verified (the Nabber had it refused: no answer ×3) |
| `:SENS:FUNC:IMP:TYPE?` | -113 / -420 | `Impedance_Type` + `Get_` retired |
| `:SOUR:CURR?` | -113 / -420 | `Set_Test_Current` + `Get_` retired |
| `:SENS:CORR:OPEN:STAT?`, `:SENS:CORR:SHOR:STAT?` | -113 / -420 | the two `Correction_*_State` + `Get_` retired |

The unit's own `*LRN?` (its settings as headers): `:FUNC:CONC 0;:FUNC "FADM";:CAL:CABL +0;:SOUR:FREQ +1.00000E+03;VOLT +1.00000E+00;VOLT:OFFS:STAT 0;:AVER 1;:AVER:COUN +1;:FIMP:APER +6.50000E-02;RANG:AUTO 1;:FIMP:CONT:VER 0;:TRIG:DEL +0.00000E+00;SOUR INT;:CALC1:FORM CP;:CALC2:FORM D;:CALC1:MATH:STAT 0;:CALC2:MATH:STAT 0;:CALC1:LIM:STAT 0`. Autorange is `:SENS:FIMP:RANG:AUTO`, so `Voltage_Range_Auto` (`:SENS:VOLT:RANG:AUTO`) is probably wrong — noted, not changed.

GRAB compiled from `4263A.qualified.json` (Nabber evidence + this probe): `:CALC1:FORM?;:CALC2:FORM?;:FETC?;:INIT:CONT?;:SENS:FUNC?;:SOUR:FREQ?;:SOUR:VOLT?;:TRIG:SOUR?;*IDN?` — `qualify_grab.py --model 4263A`: Dev711 9/9 ok.
