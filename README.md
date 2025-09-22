# a2-6502-analyzer
The A2-6502 is an adapter allowing [Dr Gusman's LogicAnalyzer](https://github.com/gusmanb/logicanalyzer) to capture all 6502 signal pins on an Apple II. This adapter is spefically designed for the Apple IIc, but work equally well in the Apple IIe. It will work in the older Apple II and II+, however extra spacers are required, as the expansion slots get in the way.

In the Apple IIc, the adapter fits into the motherboard's CPU socket, even with the motherboard still in the case. No other components are obstructed, giving the user complete access to all available signals on the board. In an Apple IIe, the adapter's layout also allows access to all signals on the system. It does however block the use of slots 3 and 4.

<img width="386" height="245" alt="image" src="https://github.com/user-attachments/assets/59300081-a10f-4d6c-a6ef-1137d4bd4383" />


The adapter board maps the Apple IIc 6502 signals to specific ports on the LogicAnalyzer pair. An additional 16 ports are available on an expansion header, allowing the user to not only capture cpu specific signals, but to also reach out to additional areas of the system to gather related information.

Dr Gusman's 6.5 release is recommended for this deployment. At this time, it is still in beta. This release provides profile support, and allows the user to import a port assignment set when using the a2-6502 adapter. A basic profile for this board is available [here](https://github.com/eositis/a2-6502-analyzer/tree/main/Gusmans-LogicAnalyzer).
1. profiles.json
   - copy the file to $HOME/Library/Application Support/LogicAnalyzer
   - if you already have a pofile created, you will need to copy the relevant data into your existing profile
2. cpSettingsMulti.json
   - TBD

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
   - Disconnect the USB cable from the LogicAnalyzer at J2 (rear)
   - Start the LogicAnalyzer software
   - Configure a MultiDevice scanner
   - Select the currently listed LogicAnalyzer as the Master
   - Connect the USB cable to the LogicAnalyzer in J2
   - Refresh the list of USB devices
   - Connect the second LogicAnalyzer board to Slave1
   - From the profiles menu, select the previously imported Apple II profile
6) Congratulations! Setup is complete!

## Channel assignments
<img width="359" height="635" alt="image" src="https://github.com/user-attachments/assets/c4f22d23-842a-4563-b957-6c1d2bad59de" />

## J3 header pin assignments
The Opt X.nn signals are routed to the J3 breakout header. The user can use standard DuPont cables and clips to reach out to other parts of the system for additional data.
The J3 header signals are ordered as follows:
![a2-6502-J3header](https://github.com/user-attachments/assets/1c61d933-2e05-4c63-9d15-c92ce294f0c8)

### Board View
![a2-6502-v1 5](https://github.com/user-attachments/assets/f045d332-7186-456d-840c-d61f90bf8f7c)

### Ready to collect data
![a2-6502-action-v1_4](https://github.com/user-attachments/assets/2841a7ba-cd46-487d-ad21-ee0a1624c94a)





