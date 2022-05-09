# Resources

- [Changes for adding a BLTouch sensor](https://reprap.org/forum/read.php?415,880766)
- Always issue:
  ```
  M502 ; Factory reset
  M500 ; Save settings to EEPROM
  ```
  after flashing new firmware, especially if a tweaked configuration setting
  doesn't appear to have taken effect.

# TODO

- [X] Calibrate NOZZLE_TO_PROBE_OFFSET
  - [Advice](https://www.reddit.com/r/ender3/comments/bwbzbn/official_bltouch_kit_xyz_probe_offsets/)
  - [ ] Use babystepping method instead of Z-offset?

- [ ] [Tune PIDs](https://reprap.org/wiki/PID_Tuning)
- [Advice](https://www.reddit.com/r/ender3/comments/mudger/the_benefits_of_pid_tuning_your_ender_3_v2/)
