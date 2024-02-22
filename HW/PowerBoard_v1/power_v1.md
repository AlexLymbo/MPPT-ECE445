# Wheel v8.1
**Board Requirements**


## Overview and Description
- This board is the steering wheel on the car including most of the I/O from/to the driver. 
- This replaces Wheel v7 as it is a new mechanical design and adds more input functionality.
- Most of the functionality will be combined into one PCB:
	- The wheel bridge board has the major power protection circuitry on it.
- Other board integration
	- Dash (CAN)
	- MCC (CAN)
	- BMS (CAN)
	- PDS (CAN)
	- PTT Radio (Hard wire)
- Wiki page: [Wheel v8](https://wiki.illinisolarcar.com/w/index.php/Wheel_v8)

## High-Level Requirements
- Microcontroller
	- [LPC1549](https://www.nxp.com/docs/en/data-sheet/LPC15XX.pdf)
	- Integrated CAN
	- JTAG Programming
	- Reset buttons
- Driver Controls
	- Turn Signals
		- A three position switch for right, left, and no turn options
	- Push To Talk
		- Comply with ASC/WSC hands free rules
		- Work independently of car
	- Horn
	- Accelerator
		- Analog input, at least 120 values within movement range of encoder
	- Regen
		- Analog input, at least 120 values within movement range of encoder
	- Cruise mode enable
	- Coast button
	- Reset
	- OK/Flag Button
		- To allow driver to flag abnormalities and menu interaction
	- Directional button
		- For menu interaction
- Informational Displays
	- OLED 
		- Powered and controlled by the steering wheel, also mounted to steering wheel
		- Provides real-time telemetry data to driver from all CANBUS-connected PCBs
		- Driver can customize what telemetry is visible on the screen
		- Driver must control from steering wheel
	- 7 Segment Displays
		- Display speed independent of what the driver is doing on the menu
- LED Indicators
	- Indicate status of turn signal/hazard lights, parking lights, and head lights / DRLs
		- Must comply with pilot light size requirements
- External Connections
	- Can only use 12, all via quick disconnect hub
- Mechanical Design
	- Except for the display, everything should be on one PCB or panel mounted to the wheel itself. 
	- All components will be on one side except those with cutouts to the front and items ?mm(unknown at this point) in height in other areas
	- Care must be taken not to interfere with usage of the disconnect hub	


## Communication Protocols
- CAN Bus
	- Used to receive all needed data and send driver commands
	- Termination will be available on the steering wheel
	- CAN Planes will be isolated from main wheel power planes
- SPI
	- Used with encoder, 7-seg, and OLED

## Connectors
- 12 Pin Quick Disconnect hub
    - 5 Wire CAN
	- 1 Wire +24V Critical
	- 1 Wire GND Critical
	- 1 Wire Connection Sense
	- 2 PTT Wires
	- 2 Free (any cool ideas?)
- Low profile connectors should be used to prevent the anything from getting knocked loose in normal use
- Using microclasp connectors

## ICs
- X,Y axis accelerometer to detect wheel turning

## Buttons/Switches
- Buttons are described in high level requirements
- Non-SMD or THT buttons will have connectors next to them
- All buttons will go to GPIO pins
- Buttons should be panel mount
- Menu button should be a 1-axis toggle

## Power System
- +24V
	- Input power from LV Bus
	- Must be 24V through wheel connector due to wire ratings/limits
	- Power protection will occur on the wheel bridge
- +3.3V
	- DC-DC converter on the wheel will provide 24V -> 3.3V
	     - Alternatively 3.3V may be powered via USB for re-programming
	- Used to power everything on the board and all peripherals
- USB Power
    - +5V via micro-usb, regulated to 3.3V as secondary 3.3V supply
- CAN Power
    - Input from 5-Wire CAN Connections
	- Fused On Board
	- Should be ~+12V
- +5V CAN
    - Regulated from CAN Power
	- Power Isolated CAN Side of CAN Transciever

## Test Points
- +24V
- +SuperCap Power
- +3.3V
- I2C SCL & SDA
- SPI CLK/MOSI/MISO1/MISO2/Chip Selects
- Connection Sense
- SuperCap Power Sense
- GND where needed as Reference
- CAN +/- & H/L

## LED Indicators
- Onboard LEDs:
	- Heartbeat
	- CAN Receive
	- CAN Send
	- Displays functionality
	- CAN Termination
