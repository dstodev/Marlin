# Resources

- [Changes for adding a BLTouch sensor](https://reprap.org/forum/read.php?415,880766)
- Always issue:
  ```
  M502 ; Factory reset
  M500 ; Save settings to EEPROM
  ```
  after flashing new firmware, especially if a tweaked configuration setting
  doesn't appear to have taken effect.

# Current tweaks

- Nozzle offsets
  - After auto-home, X=105 and Y=105
  - X. 105 - 149.8 (measured) = -44.8
  - Y. 105 - 110.2 (measured) = -5.2
  - Z. -2.92 (calibrated manually)

- E steps: 96

# Procedures

- Heat, home & center (useful for calibrating z-offset)
  ```
  ; Start tool heating jobs in parallel (temperatures in celsius)
  M104 S205 ; Hotend temperature
  M140 S60  ; Bed temperature

  ; Wait (only when heating) for both tools to reach temperature
  M109 S205 ; Hotend
  M190 S60  ; Bed

  G28 ; Auto-home
  G0 X105 Y105 Z1 ; Center with Z 1mm away from beds
  ```

- Turn things off
  ```
  M106 S0 ; Fan
  M104 S0 ; Hotend
  M140 S0 ; Bed
  ```

- Calculate nozzle X/Y  offset
  - [Advice](https://www.reddit.com/r/ender3/comments/bwbzbn/comment/epwjp6s/?utm_source=share&utm_medium=web2x&context=3)
  1. Auto-home & record X/Y coordinates from control panel:
     - X: 105
     - Y: 105
  2. Move Z as low to bed as possible
  3. Mark paper on bed with nozzle by gently pressing into paper
  4. Move so probe needle is as close to paper as possible without touching \([M401](https://marlinfw.org/docs/gcode/M401.html) to deploy probe needle\)
  5. Move X/Y from control panel until probe needle lines up with mark on paper
  6. Record new X/Y values:
     - X: 149.8
     - Y: 110.2

- [Tune PIDs](https://reprap.org/wiki/PID_Tuning)
  - [Advice](https://www.reddit.com/r/ender3/comments/mudger/the_benefits_of_pid_tuning_your_ender_3_v2/)
  - Autotune PIDs (outputs Kp Ki Kd values)
  - ```
    M303 S215 C10 ; Hotend @ 215c for 10 cycles
    M303 E-1 S60 C10 ; Bed @ 60c for 10 cycles
    ```

# TODO

- [X] Calibrate NOZZLE_TO_PROBE_OFFSET
  - [Advice](https://www.reddit.com/r/ender3/comments/bwbzbn/official_bltouch_kit_xyz_probe_offsets/)
  - [ ] Use babystepping method instead of Z-offset?

- Calibrate extruder (E) steps
  - Current calibration is likely inaccurate
  -[Guide](https://all3dp.com/2/extruder-calibration-6-easy-steps-2/)
