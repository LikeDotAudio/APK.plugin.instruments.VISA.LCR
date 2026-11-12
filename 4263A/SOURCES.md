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

## The owner's CERTIFY ALL (2026-11-12, instrument page)

From the page's certificate book on 3145J01840: `:READ?` **failed 3/3** with -113,"Undefined header" / -420 — `Read_Measurement` retired; read a measurement as `*TRG` (or `:TRIGger`) then `:FETCh?`. `:FETCh?` answers three values — status, primary, secondary (`+0,+1.01820E-11,+4.18142E-03`) — and its `returns` now says so. Verified by passing tries: `*OPC?` (1), `*TST?` (+0), `:FETCh?`, `lcr_reading`, `*RST`, `*CLS`, `*TRG`, `:TRIGger`. Pass 1 aborted at `Secondary_Parameter` when WEB.OsApi was rebuilt mid-run (HTTP 502) — not the unit's doing.

## Retired commands removed (owner, 2026-11-12)

Every `retired` entry left the table on the owner's word; the reasons stay above. Removed (15): set/Correction_Open_State `:SENSe:CORRection:OPEN:STATe <state>`, set/Correction_Short_State `:SENSe:CORRection:SHORt:STATe <state>`, set/Impedance_Type `:SENSe:FUNCtion:IMPedance:TYPE <type>`, set/Set_Test_Current `:SOURce:CURRent <level>`, nab/Get_Meas_All `MEAS:ALL?`, nab/Get_Meas_Curr `MEAS:CURR?`, nab/Get_Meas_Pow `MEAS:POW?`, nab/Get_Meas_Volt `MEAS:VOLT?`, nab/Measure_Impedance `:MEASure:IMPedance?`, nab/Measure `:MEASure?`, nab/Read_Measurement `:READ?`, nab/Get_Correction_Open_State `:SENSe:CORRection:OPEN:STATe?`, nab/Get_Correction_Short_State `:SENSe:CORRection:SHORt:STATe?`, nab/Get_Impedance_Type `:SENSe:FUNCtion:IMPedance:TYPE?`, nab/Get_Test_Current `:SOURce:CURRent?`. The family panel `gui/LCR.json` (its electronic-load `DC_Load_Station` block) still names `Get_Meas_Volt/Curr/Pow/All` — those meters now bind to nothing.

## All L / All C / All R (owner, 2026-11-12)

Friends, by name and group: `Rig_All_<X>` once at the beginning — `:TRIG:SOUR BUS;:CALC1:FORM <p>;:CALC2:FORM <s>;:SOUR:FREQ <freq>;:SOUR:VOLT <level>` — then `Nab_All_<X>` (`*TRG;*WAI;:FETC?`) over and over, each one reading (status, primary, secondary). Each rig also sets `:SENS:FUNC` — "FIMP" (impedance) or "FADM" (admittance; the unit's *LRN? shows it in FADM with CP/D). L = FIMP LS/Q, C = FADM CP/D, R = FIMP REAL/IMAG (R/X), Z = FIMP MLIN/PHAS (|Z|/θ), G = FADM REAL/IMAG (G/B), S = FADM MLIN/PHAS (|Y|/θ, siemens). FIMP and the REAL/IMAG/MLIN/PHAS spellings are recalled from the 4263B guide, unconfirmed. All unverified until Certify tries them.

## Paths against the 4263B Operation Manual (2026-11-11, nothing sent)

Source: Agilent 4263B LCR Meter Operation Manual (04263-90041), ch. 5 *GPIB Reference* — Subsystem Command List p. 5-2/5-3, Command Reference p. 5-8 on (xdevs.com copy). Cross-check: the unit's own `*LRN?` (2026-11-12 03:07 UTC, 3145J01840 fw 02.00) answers in exactly this tree — `:FUNC:CONC 0;:FUNC "FADM";:CAL:CABL +0;:SOUR:FREQ …;VOLT …;VOLT:OFFS:STAT 0;:AVER 1;:AVER:COUN +1;:FIMP:APER …;RANG:AUTO 1;:FIMP:CONT:VER 0;:TRIG:DEL …;SOUR INT;:CALC1:FORM CP;:CALC2:FORM D;…;:CALC1:LIM:STAT 0`. The tree has no READ, MEASure, MEMory, SOURce:BIAS, SOURce:CURRent, SENSe:CURRent, SENSe:VOLTage or CORRection:OPEN/SHORt nodes.

| Command | Was | Now | Manual |
|---|---|---|---|
| `set/Limit_Lower` | `:CALCulate:LIMit:LOWer` | `:CALCulate1:LIMit:LOWer` | p. 5-10 `:CALCulate{1\|2}:LIMit:LOWer[:DATA]`; suffix 1 written out (*LRN?: `:CALC1:LIM:STAT`) |
| `set/Limit_Upper` | `:CALCulate:LIMit:UPPer` | `:CALCulate1:LIMit:UPPer` | p. 5-11 |
| `set/Limit_State` | `:CALCulate:LIMit:STATe` | `:CALCulate1:LIMit:STATe` | p. 5-10 |
| `set/Current_Range` | `:SENSe:CURRent:RANGe` | `:SENSe:FIMPedance:RANGe:UPPer` | p. 5-27 — the one range is the impedance range, in ohms |
| `set/Voltage_Range_Auto` | `:SENSe:VOLTage:RANGe:AUTO` | `:SENSe:FIMPedance:RANGe:AUTO` | p. 5-26 |
| `set/Set_Bias_State` | `:SOURce:BIAS:STATe` | `:SOURce:VOLTage:OFFSet:STATe` | p. 5-30 — DC bias is the voltage offset |
| `set/Set_Bias_Voltage` | `:SOURce:BIAS:VOLTage` | `:SOURce:VOLTage:OFFSet` | p. 5-29 |
| `do/Correction_Open` | `:SENSe:CORRection:OPEN` | `:SENSe:CORRection:COLLect STANdard1` | p. 5-25, example p. 4-8 |
| `do/Correction_Short` | `:SENSe:CORRection:SHORt` | `:SENSe:CORRection:COLLect STANdard2` | p. 5-25 |
| `set/Display_State` | — | unchanged | p. 5-19 `:DISPlay[:WINDow][:STATe]`; Certify 03:02 UTC read OFF→0, ON→1 |
| `set/Init_Continuous`, `Average_Count`, `Measurement_Function`, `Set_Test_Frequency`, `Set_Test_Level`, `Set_Beeper`, `Key_Lock`, `Trigger_Delay`, `Trigger_Source`, `Primary/Secondary_Parameter` | — | unchanged | each in the list as written (`SOURce:FREQuency[:CW]`, `SOURce:VOLTage[:LEVel]…`, `[SENSe]:FUNCtion[:ON]` with `'FIMPedance'`/`'FADMittance'`, TRIGger:SOURce `BUS\|EXTernal\|MANual\|INTernal`); CALC1:FORMat `REAL\|MLINear\|CP\|CS\|LP\|LS`, CALC2:FORMat `IMAGinary\|PHASe\|D\|Q\|REAL\|LP\|RP\|INV` (p. 5-9) |

`4263A.scpi.json`: roots now the manual's list (CALibration added; MEMory and READ dropped); its 11 `unresolved` entries are gone with the commands.

**Electronic-load commands removed.** `set/Set_Curr`, `Set_Curr_Lev`, `Set_Curr_Slew`, `Set_Curr_Tlev`, `Set_Inp`, `Set_Mode`, `Set_Res`, `Set_Tran_Dcyc`, `Set_Tran_Freq`, `Set_Tran_Stat`, `Set_Volt` (`CURR…`, `INP`, `MODE`, `RES`, `TRAN:…`, bare `VOLT`) are the HP electronic-load set (06060-90005), none in the 4263B tree; the owner's Certify of 2026-11-12 02:46–03:01 UTC had every readback (`CURR?`, `CURR:LEV?`, `CURR:SLEW?`, `CURR:TLEV?`, `INP?`) answer -113 "Undefined header". They came from `gui/LCR.json`, whose `LCR_Instrument` bin was one block `DC_Load_Station` ("Energy Dissipation Interface": LOAD ACTIVE (SINKING) button, input-volts / sink-current / dissipation meters, Drain Timeline, operating mode, current/voltage/resistance knobs, pulse mode) — the electronic-load panel that `INSTRUMENT.Load/gui/Load.json` carries split over `Load_Instrument`/`Load_Settings`/`Pulse`, copied into the LCR family before the 2026-10-17 folder rename. That block is gone; the bin now holds `LCR_Measurement` (FETCH READING → `Fetch_Existing`, verified, with its readout).

**The leading colon is not the fault.** Every header the 4263A has answered with +0 starts with ':' (`:FETCh?`, `:CALCulate1:FORMat?`, `:CALCulate2:FORMat?`, `:INITiate:CONTinuous?`, `:SENSe:FUNCtion?`, `:SOURce:FREQuency?`, `:SOURce:VOLTage?`, `:TRIGger:SOURce?`, `:SYSTem:ERRor?`, `:DISPlay:STATe`), the unit's own `*LRN?` writes leading colons, and the colon-less load headers (`CURR?`, `INP?`, `MODE?`, `RES?`, `TRAN:…?`, `VOLT?`) fail exactly like the colon ones that do not exist (`:READ?`, `:MEASure?`): -113 then -420. The manual (p. 5-4) makes a leading ':' mean "start at the root". No per-model colon field is needed.

## Fetch_Existing retired and removed (owner, 2026-11-12)

The GUI certificate of 2026-11-12 04:54–04:56 on 3145J01840 fw 02.00 (gpib7,11): nab/Fetch_Existing `:FETCh?`, asked alone straight after `*TST?`, answered nothing for 30 s, then the queue said -230,"Data corrupt" | -420,"Query UNTERMINATED". A bare `:FETCh?` reads the last result without making one, so there is nothing to read after `*TST?`, after `*RST` or with the trigger idle. The owner retired it, and it left the table. The panel's FETCH READING button (`gui/LCR.json`) is now nab/Measure_Reading `*TRG;*WAI;:FETCh?`, the same stack as the Nab_All_* reads. It is unverified: under `TRIG:SOUR INT` the same certificate's Trigger_Bus drew -211 "Trigger ignored". `lcr_reading` (`:SENS:FUNC?;:FETCh?`, READ ALWAYS) is still an untriggered fetch, and `4263A.qualified.json` still lists `:FETC?`.

## Every command certified: the parameter pair, the rigs and the nabs (bench, 2026-11-12)

The owner asked that every command be tried ("let's be complete"). Bench work on 3145J01840 fw 02.00 (gpib7,11) through the instrument page's send, ~06:00 UTC:

- **The function decides the primary.** `:CALC1:FORM CS` and `LS` are taken only under `:SENS:FUNC "FIMP"`, `CP` and `LP` only under `"FADM"`. Otherwise the unit answers -141 "Invalid character data" and keeps the old value. `REAL` and `MLIN` are taken under either. That -141 failed Certify's Primary_Parameter (set CS under FADM). The selector now carries `arg.needs` (option → settings made first), and Certify puts the function back.
- **The pair is coupled.** `:CALC2:FORM IMAG` takes the primary to `REAL`, and `PHAS` takes it to `MLIN`. `D`, `Q` and `REAL` from a REAL/MLIN primary take it back to C or L of the function's kind. Both selectors carry `arg.couples` (the other header, held and put back).
- **Secondary `LP` and `RP` do not exist on this unit.** They drew -141 under every primary in both functions, so they were dropped from Secondary_Parameter's options along with their two individuals. The 4263B manual's list is wider than the 4263A's.
- **The function is string data.** `:SENS:FUNC FIMP` without quotes is -148 "Character data not allowed". Certify's put-back used to write it bare.
- **An idle trigger system answers nothing.** `*RST` leaves `:INIT:CONT 0`. Then `*TRG` is ignored (-211) and `:FETCh?` hangs 30 s (-230 | -420): this is what killed Fetch_Existing and failed Nab_All_C / Measure_Reading. With `:INIT:CONT ON` every rig + nab (C, G, L, R, S, Z) answered at once with the queue at 0. So every Rig_All_* now sets `:INITiate:CONTinuous ON` after `:TRIGger:SOURce BUS`. **`*TRG` answers by itself under BUS:** the unit puts the reading in its output buffer, so `*TRG;*WAI;:FETCh?` came back as two readings (Certify: "SDK says 3 values, the unit answered 2"). An unread one is the -410 "Query INTERRUPTED" the next query meets, which includes the panel's Trigger_Bus button under BUS. Every Nab_All_* and Measure_Reading are now `:TRIGger;*WAI;:FETCh?`, which gave one reading under BUS, under INT, and with INIT:CONT OFF. Certify's fresh sequence is `:INIT`, `:TRIG`, `*OPC?` for the same reason. Stacked as `:INIT;*TRG;*WAI;:FETC?` it hung under INT with INIT:CONT OFF: the fetch outran the measurement.
- **Still withheld by policy, not by fault:** `Key_Lock` (`:SYST:KLOCk`, the guard's KLOC/LOCK), and `Correction_Open` / `Correction_Short` (`:SENS:CORR:COLL STAN1/2`). The corrections overwrite the stored fixture correction and need the fixture open or shorted by hand, so a certificate never runs them.
