<!-- BEGIN GENERATED — apkaudio-komand build-trees -->

# LCR/4263A — command tree

Generated from the `.komand` table by `apkaudio-komand build-trees`. Edit the table, not this file.

**84 commands** — SET 52 · RIG 6 · NAB 20 · DO 6 · 66 unverified (78%)

`SET` one argument · `RIG` several applied together · `NAB` a query · `DO` a parameterless action. **†** marks a command swept out of a manual and never sent to the instrument.

## Compound commands

Several statements in one message, so they hang off no single branch. Every statement after the first carries a leading colon — without it the parser reads it relative to the previous header's path and the instrument answers `-113`.

- **NAB** `Nab_All_C` · → status, cp, d · †<br>One C reading on the rigged setup: triggers and reads status, cp, d.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_G` · → status, g, b · †<br>One G reading on the rigged setup: triggers and reads status, g, b.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_L` · → status, ls, q · †<br>One L reading on the rigged setup: triggers and reads status, ls, q.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_R` · → status, r, x · †<br>One R reading on the rigged setup: triggers and reads status, r, x.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_S` · → status, y, theta · †<br>One S reading on the rigged setup: triggers and reads status, y, theta.
  - `*TRG;*WAI;:FETCh?`
- **NAB** `Nab_All_Z` · → status, z, theta · †<br>One Z reading on the rigged setup: triggers and reads status, z, theta.
  - `*TRG;*WAI;:FETCh?`
- **RIG** `Rig_All_C` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure capacitance (parallel C and its D): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FADM";:TRIGger:SOURce BUS;:CALCulate1:FORMat CP;:CALCulate2:FORMat D;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_G` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure conductance (G and its susceptance B): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FADM";:TRIGger:SOURce BUS;:CALCulate1:FORMat REAL;:CALCulate2:FORMat IMAG;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_L` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure inductance (series L and its Q): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FIMP";:TRIGger:SOURce BUS;:CALCulate1:FORMat LS;:CALCulate2:FORMat Q;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_R` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure resistance (R and its reactance X): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FIMP";:TRIGger:SOURce BUS;:CALCulate1:FORMat REAL;:CALCulate2:FORMat IMAG;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_S` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure admittance in siemens (|Y| and its phase θ): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FADM";:TRIGger:SOURce BUS;:CALCulate1:FORMat MLIN;:CALCulate2:FORMat PHAS;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **RIG** `Rig_All_Z` · args: `freq`, `level` · numeric · †<br>Sets the meter up to measure impedance (|Z| and its phase θ): bus trigger, test frequency (100, 120, 1k, 10k, 100k Hz) and level (V).
  - `:SENSe:FUNCtion "FIMP";:TRIGger:SOURce BUS;:CALCulate1:FORMat MLIN;:CALCulate2:FORMat PHAS;:SOURce:FREQuency <freq>;:SOURce:VOLTage <level>`
- **NAB** `lcr_reading` · → function, measurement<br>What the meter is measuring, and its last measurement, together.
  - `:SENSe:FUNCtion?;:FETCh?`

## Tree

- `FETCh?` — **NAB** `Fetch_Existing` · → status, primary, secondary<br>Retrieves the most recent measurement data.
- `TRIGger` — **DO** `Trigger_Immediate`<br>Manually triggers a measurement.
- **`CALCulate1`**
  - `FORMat` — **SET** `Primary_Parameter` · `<param>` · args: `param` · enum: `CP` | `CS` | `LP` | `LS` | `REAL` | `MLIN` · †<br>Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_CP` · `CP` · †<br>Primary_Parameter → CP (parallel capacitance). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_CS` · `CS` · †<br>Primary_Parameter → CS (series capacitance). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_LP` · `LP` · †<br>Primary_Parameter → LP (parallel inductance). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_LS` · `LS` · †<br>Primary_Parameter → LS (series inductance). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_MLIN` · `MLIN` · †<br>Primary_Parameter → MLIN (|Z| under FIMP, |Y| under FADM). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat` — **SET** `Primary_Parameter_REAL` · `REAL` · †<br>Primary_Parameter → REAL (R under impedance FIMP, G under admittance FADM). Selects the primary measurement parameter (Cp, Cs, Lp, Ls, R/G, |Z|/|Y|).
  - `FORMat?` — **NAB** `Get_Primary_Parameter` · → CRD<br>Reads the primary measurement parameter.
  - **`LIMit`**
    - `LOWer` — **SET** `Limit_Lower` · `<limit>` · args: `limit` · numeric · †<br>Sets the lower limit for the comparator.
    - `STATe` — **SET** `Limit_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables the comparator function.
    - `STATe` — **SET** `Limit_State_OFF` · `OFF` · †<br>Limit_State → OFF. Enables or disables the comparator function.
    - `STATe` — **SET** `Limit_State_ON` · `ON` · †<br>Limit_State → ON. Enables or disables the comparator function.
    - `UPPer` — **SET** `Limit_Upper` · `<limit>` · args: `limit` · numeric · †<br>Sets the higher limit for the comparator.
- **`CALCulate2`**
  - `FORMat` — **SET** `Secondary_Parameter` · `<param>` · args: `param` · enum: `IMAG` | `PHAS` | `D` | `Q` | `REAL` | `LP` | `RP` · †<br>Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_D` · `D` · †<br>Secondary_Parameter → D (dissipation factor). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_IMAG` · `IMAG` · †<br>Secondary_Parameter → IMAG (X under FIMP, B under FADM). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_LP` · `LP` · †<br>Secondary_Parameter → LP (Lp). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_PHAS` · `PHAS` · †<br>Secondary_Parameter → PHAS (θ). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_Q` · `Q` · †<br>Secondary_Parameter → Q (quality factor). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_REAL` · `REAL` · †<br>Secondary_Parameter → REAL (Rs/G). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat` — **SET** `Secondary_Parameter_RP` · `RP` · †<br>Secondary_Parameter → RP (Rp). Selects the secondary measurement parameter (e.g. D, Q, X, theta).
  - `FORMat?` — **NAB** `Get_Secondary_Parameter` · → CRD<br>Reads the secondary measurement parameter.
- **`DISPlay`**
  - `STATe` — **SET** `Display_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the display ON or OFF.
  - `STATe` — **SET** `Display_State_OFF` · `OFF` · †<br>Display_State → OFF. Turns the display ON or OFF.
  - `STATe` — **SET** `Display_State_ON` · `ON` · †<br>Display_State → ON. Turns the display ON or OFF.
- **`INITiate`**
  - `CONTinuous` — **SET** `Init_Continuous` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Enables or disables continuous triggering.
  - `CONTinuous` — **SET** `Init_Continuous_OFF` · `OFF` · †<br>Init_Continuous → OFF. Enables or disables continuous triggering.
  - `CONTinuous` — **SET** `Init_Continuous_ON` · `ON` · †<br>Init_Continuous → ON. Enables or disables continuous triggering.
  - `CONTinuous?` — **NAB** `Get_Init_Continuous` · → NR1<br>Reads whether continuous triggering is on.
- **`SENSe`**
  - `FUNCtion` — **SET** `Measurement_Function` · `<function>` · args: `function` · enum: `"FIMP"` | `"FADM"` · †<br>Selects the measurement: impedance (FIMP) or admittance (FADM).
  - `FUNCtion` — **SET** `Measurement_Function_FADM` · `"FADM"` · †<br>Measurement_Function → "FADM" (admittance). Selects the measurement: impedance (FIMP) or admittance (FADM).
  - `FUNCtion` — **SET** `Measurement_Function_FIMP` · `"FIMP"` · †<br>Measurement_Function → "FIMP" (impedance). Selects the measurement: impedance (FIMP) or admittance (FADM).
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
      - `AUTO` — **SET** `Voltage_Range_Auto_OFF` · `OFF` · †<br>Voltage_Range_Auto → OFF. Turns impedance auto-ranging ON or OFF (OFF = hold range); the name is kept for the panels that bind it.
      - `AUTO` — **SET** `Voltage_Range_Auto_ON` · `ON` · †<br>Voltage_Range_Auto → ON. Turns impedance auto-ranging ON or OFF (OFF = hold range); the name is kept for the panels that bind it.
- **`SOURce`**
  - `FREQuency` — **SET** `Set_Test_Frequency` · `<freq>` · args: `freq` · numeric (Hz) · †<br>Sets the test signal frequency (100, 120, 1k, 10k, 100k Hz).
  - `VOLTage` — **SET** `Set_Test_Level` · `<level>` · args: `level` · numeric (V) · †<br>Sets the test signal level (e.g., 100m, 500m, 1V).
  - `FREQuency?` — **NAB** `Get_Test_Frequency` · → NR3 Hz<br>Reads the test signal frequency.
  - `VOLTage?` — **NAB** `Get_Test_Level` · → NR3 V<br>Reads the test signal voltage level.
  - **`VOLTage`**
    - `OFFSet` — **SET** `Set_Bias_Voltage` · `<volt>` · args: `volt` · numeric (V) · †<br>Sets the internal DC bias voltage level.
    - **`OFFSet`**
      - `STATe` — **SET** `Set_Bias_State` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the DC bias ON or OFF.
      - `STATe` — **SET** `Set_Bias_State_OFF` · `OFF` · †<br>Set_Bias_State → OFF. Turns the DC bias ON or OFF.
      - `STATe` — **SET** `Set_Bias_State_ON` · `ON` · †<br>Set_Bias_State → ON. Turns the DC bias ON or OFF.
- **`SYSTem`**
  - `KLOCk` — **SET** `Key_Lock` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Locks or unlocks the front-panel keys.
  - `KLOCk` — **SET** `Key_Lock_OFF` · `OFF` · †<br>Key_Lock → OFF. Locks or unlocks the front-panel keys.
  - `KLOCk` — **SET** `Key_Lock_ON` · `ON` · †<br>Key_Lock → ON. Locks or unlocks the front-panel keys.
  - `ERRor?` — **NAB** `Get_Error_Queue` · → ERROR<br>Queries the next entry in the error queue.
  - **`BEEPer`**
    - `STATe` — **SET** `Set_Beeper` · `<state>` · args: `state` · bool: `OFF` | `ON` · †<br>Turns the front-panel beeper ON or OFF.
    - `STATe` — **SET** `Set_Beeper_OFF` · `OFF` · †<br>Set_Beeper → OFF. Turns the front-panel beeper ON or OFF.
    - `STATe` — **SET** `Set_Beeper_ON` · `ON` · †<br>Set_Beeper → ON. Turns the front-panel beeper ON or OFF.
- **`TRIGger`**
  - `DELay` — **SET** `Trigger_Delay` · `<seconds>` · args: `seconds` · numeric (s) · †<br>Sets the delay time before measurement starts.
  - `SOURce` — **SET** `Trigger_Source` · `<source>` · args: `source` · enum: `BUS` | `EXT` | `MAN` | `INT` · †<br>Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce` — **SET** `Trigger_Source_BUS` · `BUS` · †<br>Trigger_Source → BUS (*TRG / GET). Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce` — **SET** `Trigger_Source_EXT` · `EXT` · †<br>Trigger_Source → EXT (rear trigger input). Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce` — **SET** `Trigger_Source_INT` · `INT` · †<br>Trigger_Source → INT (free run). Selects trigger source (INT, MAN, EXT, or BUS).
  - `SOURce` — **SET** `Trigger_Source_MAN` · `MAN` · †<br>Trigger_Source → MAN (front-panel key). Selects trigger source (INT, MAN, EXT, or BUS).
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
