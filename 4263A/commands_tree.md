<!-- BEGIN GENERATED — apkaudio-komand build-trees -->

# LCR/4263A — command tree

Generated from the `.komand` table by `apkaudio-komand build-trees`. Edit the table, not this file.

**45 commands** — SET 19 · RIG 3 · NAB 17 · DO 6 · 27 unverified (60%)

`SET` one argument · `RIG` several applied together · `NAB` a query · `DO` a parameterless action. **†** marks a command swept out of a manual and never sent to the instrument.

## Compound commands

Several statements in one message, so they hang off no single branch. Every statement after the first carries a leading colon — without it the parser reads it relative to the previous header's path and the instrument answers `-113`.

- **NAB** `Nab_All_C` · → status, cp, d · †<br>One C reading on the rigged setup: triggers and reads status, CP, D.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_L` · → status, ls, q · †<br>One L reading on the rigged setup: triggers and reads status, LS, Q.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_R` · → status, r, x · †<br>One R reading on the rigged setup: triggers and reads status, REAL, IMAG.
  - `*TRG;*WAI;:FETCh?`
- **RIG** `Rig_All_C` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure capacitance (parallel C and its D): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:TRIGger:SOURce BUS;:CALCulate1:FORMat CP;:CALCulate2:FORMat D;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_L` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure inductance (series L and its Q): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:TRIGger:SOURce BUS;:CALCulate1:FORMat LS;:CALCulate2:FORMat Q;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_R` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure resistance (R and its reactance X): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:TRIGger:SOURce BUS;:CALCulate1:FORMat REAL;:CALCulate2:FORMat IMAG;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **NAB** `lcr_reading` · → function, measurement<br>What the meter is measuring, and its last measurement, together.
  - `:SENSe:FUNCtion?;:FETCh?`

## Tree

- `FETCh?` — **NAB** `Fetch_Existing` · → status, primary, secondary<br>Retrieves the most recent measurement data.
- `TRIGger` — **DO** `Trigger_Immediate`<br>Manually triggers a measurement.
- **`CALCulate1`**
  - `FORMat` — **SET** `Primary_Parameter` · `<param>` · args: `param` · enum · †<br>Selects the primary measurement parameter (e.g. CP, CS, LP, LS, R, Z).
  - `FORMat?` — **NAB** `Get_Primary_Parameter` · → CRD<br>Reads the primary measurement parameter.
  - **`LIMit`**
    - `LOWer` — **SET** `Limit_Lower` · `<limit>` · args: `limit` · numeric · †<br>Sets the lower limit for the comparator.
    - `STATe` — **SET** `Limit_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables the comparator function.
    - `UPPer` — **SET** `Limit_Upper` · `<limit>` · args: `limit` · numeric · †<br>Sets the higher limit for the comparator.
- **`CALCulate2`**
  - `FORMat` — **SET** `Secondary_Parameter` · `<param>` · args: `param` · enum · †<br>Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat?` — **NAB** `Get_Secondary_Parameter` · → CRD<br>Reads the secondary measurement parameter.
- **`DISPlay`**
  - `STATe` — **SET** `Display_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the display ON or OFF.
- **`INITiate`**
  - `CONTinuous` — **SET** `Init_Continuous` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables continuous triggering.
  - `CONTinuous?` — **NAB** `Get_Init_Continuous` · → NR1<br>Reads whether continuous triggering is on.
- **`SENSe`**
  - `FUNCtion` — **SET** `Measurement_Function` · `<function>` · args: `function` · enum · †<br>Selects measurement parameters (e.g., CP-D, LS-Q).
  - `FUNCtion?` — **NAB** `Get_Measurement_Function` · → CRD<br>Reads what the meter is measuring.
  - **`AVERage`**
    - `COUNt` — **SET** `Average_Count` · `<count>` · args: `count` · integer · †<br>Sets the number of measurement averages (1 to 256).
  - **`CORRection`**
    - `COLLect` — **DO** `Correction_Open` · `STANdard1` · †<br>Executes the OPEN correction.
    - `COLLect` — **DO** `Correction_Short` · `STANdard2` · †<br>Executes the SHORT correction.
  - **`FIMPedance`**
    - **`RANGe`**
      - `UPPer` — **SET** `Current_Range` · `<range>` · args: `range` · numeric · †<br>Sets the impedance measurement range in ohms (0.1 to 1M, or UP/DOWN); the name is kept for the panels that bind it.
      - `AUTO` — **SET** `Voltage_Range_Auto` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns impedance auto-ranging ON or OFF (OFF = hold range); the name is kept for the panels that bind it.
- **`SOURce`**
  - `FREQuency` — **SET** `Set_Test_Frequency` · `<freq>` · args: `freq` · numeric (Hz) · †<br>Sets the test signal frequency (100, 120, 1k, 10k, 100k Hz).
  - `VOLTage` — **SET** `Set_Test_Level` · `<level>` · args: `level` · numeric (V) · †<br>Sets the test signal level (e.g., 100m, 500m, 1V).
  - `FREQuency?` — **NAB** `Get_Test_Frequency` · → NR3 Hz<br>Reads the test signal frequency.
  - `VOLTage?` — **NAB** `Get_Test_Level` · → NR3 V<br>Reads the test signal voltage level.
  - **`VOLTage`**
    - `OFFSet` — **SET** `Set_Bias_Voltage` · `<volt>` · args: `volt` · numeric (V) · †<br>Sets the internal DC bias voltage level.
    - **`OFFSet`**
      - `STATe` — **SET** `Set_Bias_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the DC bias ON or OFF.
- **`SYSTem`**
  - `KLOCk` — **SET** `Key_Lock` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Locks or unlocks the front-panel keys.
  - `ERRor?` — **NAB** `Get_Error_Queue` · → ERROR<br>Queries the next entry in the error queue.
  - **`BEEPer`**
    - `STATe` — **SET** `Set_Beeper` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the front-panel beeper ON or OFF.
- **`TRIGger`**
  - `DELay` — **SET** `Trigger_Delay` · `<seconds>` · args: `seconds` · numeric (s) · †<br>Sets the delay time before measurement starts.
  - `SOURce` — **SET** `Trigger_Source` · `<source>` · args: `source` · enum · †<br>Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce?` — **NAB** `Get_Trigger_Source` · → CRD<br>Reads the trigger source.

## Common commands (IEEE 488.2)

- `*CLS` — **DO** `Clear_Status`<br>Clears the status byte and error queue.
- `*OPC?` — **NAB** `Get_Operation_Complete` · → NR1<br>Returns '1' once all pending operations are completed.
- `*LRN?` — **NAB** `Learn_Settings` · → AARD<br>Reads the learn string: every current setting in one reply.
- `*IDN?` — **NAB** `Read_IDN` · → AARD<br>Queries the instrument identification (Manufacturer, Model, Serial, Firmware).
- `*RST` — **DO** `Reset_Device`<br>Resets the unit to its factory default settings.
- `*TST?` — **NAB** `Self_Test` · → NR1<br>Runs the internal self-test; 0 = pass, else an error code.
- `*TRG` — **DO** `Trigger_Bus`<br>Triggers the unit (equivalent to the Bus trigger).

<!-- END GENERATED -->
