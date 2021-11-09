# RE:Flex Dance I/O v2 PCB Design 

This repository contains source documents and manufacturing files for the RE:Flex Dance Pad's I/O Board. It was created using [KiCAD 5.1.4](https://kicad.org/).

The I/O Boards purpose is to provide an interface between a computer (using USB 2.0) and 4 'panel boards' (using RJ45) to:
- Receive panel board pressure sensor data, organize the data and send it to computer programs
- Receive LED data from computer programs, organize and send it to panel boards to display on RGB LED array

## Getting your own

The least-work way is to order the Printed Circuit board (PCB) assembled from JLCPCB. You can also order a bare board from any PCB prototyping place, and then source and solder all the components yourself.
Board: The JLCPCB assembled route
1. Grab the latest PCB manufacturing files

    Go to the Latest release and download `release-v2-RC2.zip`. This contains all the PCB fabrication outputs from KiCAD. Alternatively, clone or download this repository, open the project from the pcb/multi-midi folder in KiCad and export the gerber files yourself.
    
    If you want, you can generate the manufacture files yourself, but this is trickier than generating the gerber files since a 3rd party script needs to be installed, and output files manually edited to work with JLCPCB. Documentation: How to generate the BOM and Centroid file from KiCAD

2. Place the order with [JLCPCB](https://jlcpcb.com)
```
    Click "Add your gerber file", select the release-v2-RC2.zip file from the releases.
    Pick a board color or leave it at the default green. Last time I checked different colors only affect build time, not price.
    Pick a surface finish or leave it on the default. The default is cheapest, but contains lead. ENIG gives the pads a nice golden finish instead of silver.
    Leave all the other options as they are.
    Scroll down to "SMT Assembly" and switch it on
    Select "assemble top side"
    Pick a quantity; if you only want one, 2 will be the minimum here
    Click "Confirm".
    On the right side of the page, click "Next"
    Click "Add BOM File"; upload the *release/bom.csv* file
    Click "Add CPL File"; upload the the *release/io-board-top-pos.csv* file
    Click "Next"
    Review the specified parts; they should all be "confirmed" in the right column, so you can leave everything as it is.
    Click "Next"
    In the preview, some ICs might look like they're oriented wrong. This is a problem with their viewer; the files are correct. If it ends up wrong (not aligning with the pads), they'll either correct it or email you to find a solution.
    Click "Save to cart"
    Click "Check out Securely"
    Add your shipping and billing details
    Select a shipping method. Usually the DHL-based ones are fine. You can gamble on whether or not you want duty and customs paid up front (more expensive), or hope for the best with the cheaper option, in which case you might get a bill from the courier later.
    Click "Continue" when you're happy
    Click "submit order"
    Do what you need to do for payment
    Wait for your boards to get delivered
```

3. Order the remaining through-hole parts - A list of these parts can be seen at `release/unpopulated.csv`. Companies that sell parts like this include Mouser, Digikey, RS-Components and Farnell.

4. Solder the remaining parts onto the board. Fairly evident where each of them go, though a more detailed guide here could be helpful. Pull requests welcome. :-)

## Future Improvements
- Currently, there's a lot of connectors. We could daisy chain a number of boards if we utilized the correct UART transmission protocol. My hope is eventually to just have 3 RJ45 connectors, which can each address a maximum of 3 panels.
- We could also eliminate the need for all of the output DC power jacks by running power along the RJ45 cable, similar to 'Power over Ethernet'. This would probably depend on using lower-powered LEDs, which is already an improvement listed under the panel board.
- The RS-485 transceivers probably don't need direction-switching, and the transceiver is entirely deprecated connected to the USART clock lines. We could save some microcontroller pins by removing this. This'd also make firmware updates to panel boards over UART a lot easier.
- More output types! Currently we just have USB. In the future, we could connect to arcade machines, consoles, and other things. 
- More methods of panel addressing. Currently the RJ45 method is the only way. So any future panel boards would have to conform to that specification. Some people may just want a much easier method of addressing digital sensors or force sensitive resistors. This could be supported on the I/O board to reduce requirements for travel pads and the likes.
- Easier debugging. The status LEDs are ambiguous as to what they do. More status LEDs, more text indication on the board (e.g. 'Left Panel Unconnected' next to a status LED) could make things a lot easier for the end user.
- Future form factor updates. People might want to use these boards in an arcade pad. They may want to avoid the aluminium extrusion framework. Fitting this board for all sorts of different requirements will improve accessibility to the electronics.
- These boards could have through hole parts populated by a batch manufacturer, and be sold without the need for soldering. If you'd like to sell these boards, please get in touch, and we can help you source finished boards.

## Firmware

For the board to function, you will need to install the I/O board firmware to it. You can find this information within the repo for the IO-Firmware.

## License

For license details, see LICENSE file
