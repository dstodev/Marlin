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

- Z offset: -2.92
- E steps: 96

# Procedures
- Heat, home & center (for calibrating z-offset)
  ```
  ; Start both heating jobs in parallel
  M104 S205 ; Set hotend temperature to 205c
  M140 S60 ; Set bed temperature to 55c
  
  ; Wait (only when heating) for both tools to reach temperature
  M109 S205 ; Hotend
  M190 S60  ; Bed
  
  G28 ; Auto-home
  G0 X105 Y105 Z1 ; Center with Z 1mm away from bed
  ```

- Turn things off
  ```
  M106 S0 ; Fan
  M104 S0 ; Hotend
  M140 S0 ; Bed
  ```

- Calculate nozzle X/Y  offset
  - [Advice](https://www.reddit.com/r/ender3/comments/bwbzbn/comment/epwjp6s/?utm_source=share&utm_medium=web2x&context=3)
  1. Auto-home & record X/Y coordinates from control panel
  2. Move Z as low to bed as possible
  3. Mark paper on bed with nozzle by gently pressing into paper
  4. Move so probe needle is as close to paper as possible without touching \([M401](https://marlinfw.org/docs/gcode/M401.html) to deploy probe needle\)
  5. Move X/Y from control panel until probe needle lines up with mark on paper
  6. Record X/Y offset:
     - x: 105 (x after auto-home) - 149.8 = -44.8
     - y: 105 (y after auto-home) - 110.2 = -5.2

- [Tune PIDs](https://reprap.org/wiki/PID_Tuning)
  - [Advice](https://www.reddit.com/r/ender3/comments/mudger/the_benefits_of_pid_tuning_your_ender_3_v2/)
  - Hot end, target temp 215c, 10 cycles
    ```
    M303 S215 C10
    ```
    Bed, target temp 60c, 10 cycles
    ```
    M303 E-1 S60 C10
    ```

# TODO

- [X] Calibrate NOZZLE_TO_PROBE_OFFSET
  - [Advice](https://www.reddit.com/r/ender3/comments/bwbzbn/official_bltouch_kit_xyz_probe_offsets/)
  - [ ] Use babystepping method instead of Z-offset?

- Calibrate extruder (E) steps
  - Current calibration is likely inaccurate
  -[Guide](https://all3dp.com/2/extruder-calibration-6-easy-steps-2/)
