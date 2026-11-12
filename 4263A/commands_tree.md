<!-- BEGIN GENERATED — apkaudio-komand build-trees -->

# LCR/4263A — command tree

Generated from the `.komand` table by `apkaudio-komand build-trees`. Edit the table, not this file.

**59 commands** — SET 34 · RIG 0 · NAB 19 · DO 6 · 59 unverified (100%)

`SET` one argument · `RIG` several applied together · `NAB` a query · `DO` a parameterless action. **†** marks a command swept out of a manual and never sent to the instrument.

## Compound commands

Several statements in one message, so they hang off no single branch. Every statement after the first carries a leading colon — without it the parser reads it relative to the previous header's path and the instrument answers `-113`.

- **NAB** `lcr_reading` · → function, measurement · †<br>What the meter is measuring, and its last measurement, together.
  - `:SENSe:FUNCtion?;:FETCh?`

## Tree

- `CURR` — **SET** `Set_Curr` · `<value>` · numeric (A) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- `INP` — **SET** `Set_Inp` · `<state>` · bool: `OFF` | `ON` · per-instance: `state` · †<br>Authored from a panel literal in LCR.json; never executed before.
- `MODE` — **SET** `Set_Mode` · `<value>` · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- `RES` — **SET** `Set_Res` · `<value>` · numeric (Ohm) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- `VOLT` — **SET** `Set_Volt` · `<value>` · numeric (V) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- `FETCh?` — **NAB** `Fetch_Existing` · → 1 value · †<br>Retrieves the most recent measurement data.
- `READ?` — **NAB** `Read_Measurement` · → 1 value · †<br>Triggers a measurement and retrieves the results.
- `TRIGger` — **DO** `Trigger_Immediate` · †<br>Manually triggers a measurement.
- **`CALCulate`**
  - **`LIMit`**
    - `LOWer` — **SET** `Limit_Lower` · `<limit>` · args: `limit` · numeric · †<br>Sets the lower limit for the comparator.
    - `STATe` — **SET** `Limit_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables the comparator function.
    - `UPPer` — **SET** `Limit_Upper` · `<limit>` · args: `limit` · numeric · †<br>Sets the higher limit for the comparator.
- **`CALCulate1`**
  - `FORMat` — **SET** `Primary_Parameter` · `<param>` · args: `param` · enum · †<br>Selects the primary measurement parameter (e.g. CP, CS, LP, LS, R, Z).
  - `FORMat?` — **NAB** `Get_Primary_Parameter` · → CRD · †<br>Reads the primary measurement parameter.
- **`CALCulate2`**
  - `FORMat` — **SET** `Secondary_Parameter` · `<param>` · args: `param` · enum · †<br>Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat?` — **NAB** `Get_Secondary_Parameter` · → CRD · †<br>Reads the secondary measurement parameter.
- **`CURR`**
  - `LEV` — **SET** `Set_Curr_Lev` · `<value>` · numeric (A) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
  - `SLEW` — **SET** `Set_Curr_Slew` · `<value>` · numeric (A/s) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
  - `TLEV` — **SET** `Set_Curr_Tlev` · `<value>` · numeric (A) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- **`DISPlay`**
  - `STATe` — **SET** `Display_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the display ON or OFF.
- **`INITiate`**
  - `CONTinuous` — **SET** `Init_Continuous` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables continuous triggering.
  - `CONTinuous?` — **NAB** `Get_Init_Continuous` · → NR1 · †<br>Reads whether continuous triggering is on.
- **`SENSe`**
  - `FUNCtion` — **SET** `Measurement_Function` · `<function>` · args: `function` · enum · †<br>Selects measurement parameters (e.g., CP-D, LS-Q).
  - `FUNCtion?` — **NAB** `Get_Measurement_Function` · → CRD · †<br>Reads what the meter is measuring.
  - **`AVERage`**
    - `COUNt` — **SET** `Average_Count` · `<count>` · args: `count` · integer · †<br>Sets the number of measurement averages (1 to 256).
  - **`CORRection`**
    - `OPEN` — **DO** `Correction_Open` · †<br>Executes the OPEN correction.
    - `SHORt` — **DO** `Correction_Short` · †<br>Executes the SHORT correction.
    - **`OPEN`**
      - `STATe` — **SET** `Correction_Open_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the OPEN fixture compensation ON or OFF.
      - `STATe?` — **NAB** `Get_Correction_Open_State` · → NR1 · †<br>Reads whether OPEN compensation is on.
    - **`SHORt`**
      - `STATe` — **SET** `Correction_Short_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the SHORT fixture compensation ON or OFF.
      - `STATe?` — **NAB** `Get_Correction_Short_State` · → NR1 · †<br>Reads whether SHORT compensation is on.
  - **`CURRent`**
    - `RANGe` — **SET** `Current_Range` · `<range>` · args: `range` · numeric · †<br>Sets the current measurement range.
  - **`FUNCtion`**
    - **`IMPedance`**
      - `TYPE` — **SET** `Impedance_Type` · `<type>` · args: `type` · enum: `RX` | `ZTD` | `CPQ` | `CSQ` | `CSD` | `LPQ` | `LSQ` | `LSD` · †<br>Selects the measurement parameter pair.
      - `TYPE?` — **NAB** `Get_Impedance_Type` · → CRD · †<br>Reads the measurement parameter pair.
  - **`VOLTage`**
    - **`RANGe`**
      - `AUTO` — **SET** `Voltage_Range_Auto` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables auto-ranging.
- **`SOURce`**
  - `CURRent` — **SET** `Set_Test_Current` · `<level>` · args: `level` · numeric (A) · †<br>Sets the test signal level as a current.
  - `FREQuency` — **SET** `Set_Test_Frequency` · `<freq>` · args: `freq` · numeric (Hz) · †<br>Sets the test signal frequency (100, 120, 1k, 10k, 100k Hz).
  - `VOLTage` — **SET** `Set_Test_Level` · `<level>` · args: `level` · numeric (V) · †<br>Sets the test signal level (e.g., 100m, 500m, 1V).
  - `CURRent?` — **NAB** `Get_Test_Current` · → NR3 A · †<br>Reads the test signal current level.
  - `FREQuency?` — **NAB** `Get_Test_Frequency` · → NR3 Hz · †<br>Reads the test signal frequency.
  - `VOLTage?` — **NAB** `Get_Test_Level` · → NR3 V · †<br>Reads the test signal voltage level.
  - **`BIAS`**
    - `STATe` — **SET** `Set_Bias_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the DC bias ON or OFF.
    - `VOLTage` — **SET** `Set_Bias_Voltage` · `<volt>` · args: `volt` · numeric (V) · †<br>Sets the internal DC bias voltage level.
- **`SYSTem`**
  - `KLOCk` — **SET** `Key_Lock` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Locks or unlocks the front-panel keys.
  - `ERRor?` — **NAB** `Get_Error_Queue` · → ERROR · †<br>Queries the next entry in the error queue.
  - **`BEEPer`**
    - `STATe` — **SET** `Set_Beeper` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the front-panel beeper ON or OFF.
- **`TRAN`**
  - `DCYC` — **SET** `Set_Tran_Dcyc` · `<value>` · numeric (%) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
  - `FREQ` — **SET** `Set_Tran_Freq` · `<value>` · numeric (Hz) · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
  - `STAT` — **SET** `Set_Tran_Stat` · `<value>` · bool: `OFF` | `ON` · per-instance: `value` · †<br>Authored from a panel literal in LCR.json; never executed before.
- **`TRIGger`**
  - `DELay` — **SET** `Trigger_Delay` · `<seconds>` · args: `seconds` · numeric (s) · †<br>Sets the delay time before measurement starts.
  - `SOURce` — **SET** `Trigger_Source` · `<source>` · args: `source` · enum · †<br>Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce?` — **NAB** `Get_Trigger_Source` · → CRD · †<br>Reads the trigger source.

## Common commands (IEEE 488.2)

- `*CLS` — **DO** `Clear_Status` · †<br>Clears the status byte and error queue.
- `*OPC?` — **NAB** `Get_Operation_Complete` · → NR1 · †<br>Returns '1' once all pending operations are completed.
- `*LRN?` — **NAB** `Learn_Settings` · → AARD · †<br>Reads the learn string: every current setting in one reply.
- `*IDN?` — **NAB** `Read_IDN` · → AARD · †<br>Queries the instrument identification (Manufacturer, Model, Serial, Firmware).
- `*RST` — **DO** `Reset_Device` · †<br>Resets the unit to its factory default settings.
- `*TST?` — **NAB** `Self_Test` · → NR1 · †<br>Runs the internal self-test; 0 = pass, else an error code.
- `*TRG` — **DO** `Trigger_Bus` · †<br>Triggers the unit (equivalent to the Bus trigger).

<!-- END GENERATED -->
