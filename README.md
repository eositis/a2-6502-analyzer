# a2-6502-analyzer
The A2-6502 is an adapter allowing [Dr Gusman's LogicAnalyzer](https://github.com/gusmanb/logicanalyzer) to capture all 6502 signal pins on an Apple II. This adapter is spefically designed for the Apple IIc, but work equally well in the Apple IIe. It will work in the older Apple II and II+, however extra spacers are required, as the expansion slots get in the way.

In the Apple IIc, the adapter fits into the motherboard's CPU socket, even with the motherboard still in the case. No other components are obstructed, giving the user complete access to all available signals on the board. In an Apple IIe, the adapter's layout also allows access to all signals on the system. It does however block the use of slots 3 and 4.

<img width="772" height="490" alt="image" src="https://github.com/user-attachments/assets/59300081-a10f-4d6c-a6ef-1137d4bd4383" />


The adapter board maps the Apple IIc 6502 signals to specific ports on the LogicAnalyzer pair. An additional 16 ports are available on an expansion header, allowing the user to not only capture cpu specific signals, but to also reach out to additional areas of the system to gather related information.

Dr Gusman's 6.5 release is recommended for this deployment. At this time, it is still in beta. This release provides profile support, and allows the user to import a port assignment set when using the a2-6502 adapter. A basic profile for this board is available [here](https://github.com/eositis/a2-6502-analyzer/tree/main/Gusmans-LogicAnalyzer).
1. profiles.json
   - copy the file to $HOME/Library/Application Support/LogicAnalyzer
   - Windoze users copy the file to %userprofile%/appdata/roaming/logicanalyzer
   - if you already have a pofile created, you will need to copy the relevant data into your existing profile

## Initial Setup
1) Install firmware to LogicAnalyzer
2) Install two LogicAnalyzer boards to the adapter with the component side facing the cpu
3) Using three DuPont cables, connect the linking headers between the two boards. Does not matter which ports combination is used, as long as top is to top, middle to middle and bottom to bottom.
   - LogicAnalyzers purchased from me will be configured to snap together, eliminating this step.
4) Remve the cpu from the system board, and install it in the provided space on the adapter board. Be sure to maintain the correct notch orientation.
   - Optionally, install a spare CPU in the adapter board, leaving it there permanently. Set aside the system's CPU for the duration of the tests.
6) Carefully plug the adapter board into the cpu socket on the mother board - once again, take care to maintain correct notch orientation. Make sure the adapter is fully seated in the socket.
   - Some older sockets may not have sufficiently large holes for the logic analyzer's pins. If this is the case, install a doublewipe cpu socket to the motherboard and plug the logic analyzer adapter board into the doublewipe socket.
8) Download and configure the LogicAnalyzer software
   - Stable release here: https://github.com/gusmanb/logicanalyzer/releases
   - 6.5 beta realease information is here: https://github.com/gusmanb/logicanalyzer/discussions/277
10) follow install and operation guidelines in the [LogicAnalyzer wiki](https://github.com/gusmanb/logicanalyzer/wiki/06---The-LogicAnalyzer-program)

### Setup LogicAnalyzer boards using USB
1) Two USB cables will be needed
2) On the adapter board, set the jumper/switch to USB mode.
   - WiFi mode should only be used when the LogicAnalyzer has been configured for Network operation running in full wireless mode.
3) On each LogicAnalyzer board is a switch to set reference voltage
   - Typically should be set to EXT mode. This will use the Apple II system's 5v rail as a reference
   - The 5V reference can also be used. This mode can be used if testing Apple II power-on procedures. Testers have suggested that the LogicAnalyzer should start up faster than the Apple II, however this has not been confirmed.
4) Install firmware
   - extract the firmware appropriate for the Pico board installed on the LogicAnalyzers. This firmware is a part of the comprehensive download performed in an earlier step
   - each Pico board has a small reset button. Hold down this button wile plugging in one of the USB cables. Repeat for the other board.
   - on your computer, two new USB volumes will appear. Copy the appropriate firmware to the storage volume. Immediately once the copy completes, the volume will disconnect from your computer and the LogicAnalyzer will reset and boot the new firmware.
5) Configure for use
   - Start the LogicAnalyzer software
   - connect USB cables to each of the logic analyzers
   - Configure a MultiDevice scanner
   - Click 'open device'
   - Select one of the LogicAnalyzer boards as master
   - Add the second one as slave, Accept
   - Execute a data capture from an Apple II machine, do add signals via the J3 port at this time
   - Channels up to  32 should have data. Channels 33-48 should be blank lines. If this is not the case, close the device and recreate it, placing the other LogicAnalyzer as master.
   - From the profiles menu, select the previously imported Apple II profile
6) Congratulations! Setup is complete!

## Channel assignments
| J1-Analyzer1 | Signal | Pin | J2-Analyzer2 | Signal |
|-------------:|--------|---|-------------:|--------|
| CH-1 | RDY | 1 | CH-25 | A8 |
| CH-2 | IRQ\ | 2 | CH-26 | A9 |
| CH-3 | NMI\ | 3 | CH-27 | A10 |
| CH-4 | R/W\ | 4 | CH-28 | A11 |
| CH-5 | PHASE0 | 5 | CH-29 | A12 |
| CH-6 | RES\ | 6 | CH-30 | A13 |
| CH-7 | D0 | 7 | CH-31 | A14 |
| CH-8 | D1 | 8 | CH-32 | A15 |
| CH-9 | D2 | 9 | CH-33 | J3-1 |
| CH-10 | D3 | 10 | CH-34 | J3-2 |
| CH-11 | D4 | 11 | CH-35 | J3-3 |
| CH-12 | D5 | 12 | CH-36 | J3-4 |
| CH-13 | D6 | 21 | CH-37 | J3-5 |
| CH-14 | D7 | 22 | CH-38 | J3-6 |
| CH-15 | A1 | 23 | CH-39 | J3-7 |
| CH-16 | A2 | 24 | CH-40 | J3-8 |
| CH-17 | A3 | 25 | CH-41 | J3-9 |
| CH-18 | A4 | 26 | CH-42 | J3-10 |
| CH-19 | A5 | 27 | CH-43 | J3-11 |
| CH-20 | A6 | 28 | CH-44 | J3-12 |
| CH-21 | A7 | 29 | CH-45 | J3-13 |
| CH-22 | A8 | 30 | CH-46 | J3-14 |
| CH-23 | Phase1 | 32 | CH-47 | J3-15 |
| CH-24 | SYNC | 32 | CH-48 | J3-16 |

## J3 header pin assignments
The Opt X.nn signals are routed to the J3 breakout header. The user can use standard DuPont cables and clips to reach out to other parts of the system for additional data.
The J3 header signals are ordered as follows:

| PIN-1 | PIN-3 | PIN-5 | PIN-7 | PIN-9 | PIN-11 | PIN-13 | PIN-15 |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| CH-33 | CH-35 | CH-37 | CH-39 | CH-41 | CH-43 | CH-45 | CH-47 |
| CH-34 | CH-36 | CH-38 | CH-40 | CH-42 | CH-44 | CH-46 | CH-48 |
| PIN-2 | PIN-4 | PIN-6 | PIN-8 | PIN-10 | PIN-12 | PIN-14 | PIN-16 |

## Schematics
Production v1.5 schematic: https://github.com/eositis/a2-6502-analyzer/blob/main/kicad/v1.5/6502-interposer-schematic-1_5.pdf

### Board View
![a2-6502-v1 5](https://github.com/eositis/a2-6502-analyzer/blob/main/misc/a2-6502-3dview-v1_5.jpg)

### Ready to collect data
![a2-6502-action-v1_4](https://github.com/user-attachments/assets/2841a7ba-cd46-487d-ad21-ee0a1624c94a)





