# Writable parameters Altherma 3

On Daikin Altherma 3 systems parameters are communicated between the main controller and auxiliary controller in packet types 35, 36, and 3A. Packet types 35 and 3A are used to communicate 8-bit values and packet type 36 is used to communicate 16-bit values.

Some of these parameters can be changed by P1P2Monitor - when acting as an auxiliary controller (L1 mode) - using the P1P2Monitor command 'E'.

These parameters are different for different systems and/or different operation modes of the system. The best way to learn which parameter you need to set it so change a setting manually on the main controller while P1P2Monitor acts as auxiliary controller and data is logged via P1P2/R/#.  The main controller will then inform the P1P2Monitor of the new settings which you can then try to write to. Even better is to have another auxiliary controller write parameters and have P1P2Monitor eavesdrop the communication.

The E command format is "E <packet-type> <parameter-number> <new-value>", all values hexadecimal. If you hate spaces, you may concatenate these using a 2-char packet-type and 4-byte parameter number: "E35 2F 0" becomes "E35002F0"

Some example parameters and commands:

Parameter in packet type 35 for switching cooling/heating off
- 0x31 switches cooling/heating on/off in room temperature control mode (works on EHVX08S23D6V)
- 0x2F switches cooling/heating on/off in LWT control mode (works on EHYHBX08AAV3 and EHBH16CAV3)
- 0x2D (works on EHVX08S26CA9W and/or in certain operation modes?)

Commands to switch heating off and on on EHYHBX08AAV3 in LWT control mode:
- E 35 2F 0 (or E35002F0 or E35002F00)
- E 35 2F 1 (or E35002F1 or E35002F01)

Switching between heating, cooling, and automatic mode
- parameter nr 0x4E (works on EHYHBX08AAV3) (value 0=heating 1=cooling 2=auto)
- E 3A 4E 0 = set mode to heating
- E 3A 4E 1 = set mode to cooling
- E 3A 4E 2 = set mode to auto
Budulinek reports that parameter 0x3A this may not work correctly, and that parameter 0x4E in packet type 3A may have to be used instead.

Parameter in packet type 35 for switching DHW on/off
- 0x40 (works on EHVX08S23D6V and EHBH16CAV3) (and/or in certain DHW operating modes)
- 0x3E (works on EHVX08S26CA9W) (and/or in certain DHW operating modes)

Parameter in packet type 35 for switching DHW boost on/off
- 0x48 (may work on some models

Parameter in packet type 35 for switching DHWbooster on/off
- 0x48 (works on EHVX08S26CB9W)

Parameter in packet type 35 for selecting heating mode (ABS/AWT/ABS+dev/AWT+dev) (not always allowed!)
- 0x56 (works on EHYHBX08AAV3)

Parameter in packet type 35 for selecting silent mode
- 0x03 (value 0=off, 1=on)

Parameter in packet type 36 for setting target room temperature (only in room-thermostat mode)
- 0x00 (works on EHYHBX08AAV3)

Example commands to set room temperature setpoint
- E 36 0 BE sets room temperature setpoint to 0xBE = 190 = 19.0 C
- E 36 0 C8 sets room temperature setpoint to 0xC8 = 200 = 20.0 C

Parameter in packet type 36 for setting DHW setpoint
- 0x03 (works on EHYHBX08AAV3 and EHBH16CAV3)

Parameter in packet type 36 for setting heating temperature setpoint (only in fixed LWT mode)
- 0x06 (works on EHBH16CAV3 and EHYHBX08AAV3)

Example commands to set fixed LWT mode main zone temperature setpoint
- E36 6 015E sets LWT setpoint to 0x015E = 350 = 35.0 C
- E36 6 01C2 sets LWT setpoint to 0x01C2 = 450 = 45.0 C

Parameter in packet type 36 for setting main zone heating temperature deviation (only in weather-dependent LWT mode)
- 0x08 (works on EHYHBX08AAV3)

Example commands to set WD-LWT mode curve deviation
- E36 8 0 sets deviation to +0 C
- E36 8 1 sets deviation to +1 C
- E36 8 FFFF sets deviation to -1 C

Parameter in packet type 36 for setting main zone cooling temperature deviation (only in weather-dependent LWT mode)
- 0x09 (works on EHYHBX08AAV3)

Parameter in packet type 36 for setting additional zone heating temperature deviation in WD mode
- 0x0D (works on EHYHBX08AAV3)

Some other parameters:
- parameter 0x31 in packet type 3A is perhaps used to disable/enable holiday (to be confirmed)
- parameter 0x4B in packet type 3A is used to switch between 0=manual and 1=automatic DST mode
- parameter 0x5B in packet type 3A is used to switch holiday 0=off 1=on
- parameter 0x5E in packet type 3A is used to switch between heating schedules
- parameter 0x5F in packet type 3A is used to switch between cooling schedules
- parameter 0x64 in packet type 3A is used to switch between DHW schedules

Many thanks to Budulinek for finding some of these parameters. More writable parameters can be found in Budulinek's [documentation](https://github.com/budulinek/Daikin-P1P2---UDP-Gateway/blob/main/Payload-data-write.md).

# Writable parameters Altherma 2

TBD

# Writable parameters VRV / Sky air systems

TBD
