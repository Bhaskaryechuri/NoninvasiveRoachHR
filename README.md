_Author: [Bhaskar Yechuri](bhaskar.yechuri@gmail.com), Engineering Technician & Research Assistant at the [Phil Matthews Lab](http://www.matthewslab.zoology.ubc.ca/index.html), University of British Columbia - Vancouver (Last Updated: June 2021)_

# Non-Invasive Cockroach Heart Rate Monitor
A device &amp; method developed to non-invasively measure cockroach heart rate of a free-roaming cockroach.

# Summary

This photoplethysmographic device, inspired by the methods of [this paper](https://aslopubs.onlinelibrary.wiley.com/doi/abs/10.4319/lom.2013.11.91) and mounted directly onto the roach's sclerites, uses infrared LEDs and two phototransistors (i.e. IR sensors) to noninvasively monitor cockroach heart rate in real-time. [Here is a video of it in action](https://drive.google.com/file/d/15U84yjhjsBKMVfOA489h0GwnW5KllRH3/view?usp=sharing).

The system consists of the following components:
* [3D-Printed Mount](https://github.com/Bhaskaryechuri/NoninvasiveRoachHR/tree/main/mechanical): A plastic structure attached to the roach's back along the midline using melted bikini wax. This structure firmly holds the mini-PCB's LEDs & sensors close to the roach's sclerites.
* [mini-PCB](https://github.com/Bhaskaryechuri/NoninvasiveRoachHR/tree/main/circuit): Placed on the roach via the 3D-printed mount. Contains the LEDs and sensors that allow for heart rate sensing, and a symmetrical 5-pin header which can be used to conduct sensor signals out of the board and power in (GND-Signal1-5V-Signal2-GND)
* Auxiliary Board: A simple circuit connecting to the mini-PCB via a 5-pin ribbon cable, routing the outgoing signals to two independent BNC outputs and connecting the 5V power supply terminals to the mini-PCB

# Fabrication & Assembly

This section contains information on how to assemble the device from scratch.

_NOTE: If you are working with an already-fabricated device, you can skip this step._  
  

**Mini-PCB**:

1. From the `circuit` folder in this repository, download the ".SCH" and ".BRD files" and open them in [AutoCAD EAGLE](https://www.autodesk.ca/en/products/eagle/free-download)
2. Navigate to the board-view and click "ratsnest", which will create the ground plane
3. The simplest way to create the PCB would be to order it from a third-party PCB manufacturer (e.g. PCBWay, JLPCB, etc.), which are cheap, have a relatively short turnaround time, and minimize human error when compared to milling it using the CNC. To do this, each manufacturer requires a set of auto-generated outputs from EAGLE. If you get the PCBs manufactured externally, skip to Step 6
4. Export the .GBR and .XLN files and use those along with [FlatCAM](http://flatcam.org/) (only works on Windows) to generate CNC gcode files
5. Use the gcode files to mill out PCBs using the Carbide CNC machine
    1. It is recommended to try a few test runs on the CNC machine with used/scrap PCBs
6. Once the PCBs are ready, solder on the components according to the schematic & layout seen in the EAGLE files
7. Use heatshrink tubing to neatly seal the area around the LEDs to prevent light leaking out from the sides and into the adjacent sensors. Snip off the top of the tubing to ensure that only the sides of the LEDs are obscured, not the tops

**3D-printed mount**:

1. From the `mechanical` folder in this repository, download the ".STL" file and open it in [Ultimaker Cura](https://ultimaker.com/software/ultimaker-cura)
2. Align the flat surface of the mount to the build plate in Ultimaker Cura, choose the appropriate printer type, and set the infill to 100% with the ABS material
3. Click the "Slice" button and look at the "Preview" tab to ensure that the smaller features of the mount will be printed. If not, modify the print settings
4. Finally, save the gcode produced by the Ultimaker Cura to a flash drive and plug the drive into the lab 3D printer. Ensure that the material installed is ABS and print the file

**Auxiliary Board**:

1. Solder another 5-pin female header into a proto-board and connect additional jumpers to route the outer pins to their appropriate connections    
    1. (1 and 5) to GND, 
    2. the center pin (3) to 5V, and 
    3. the middle pins (2 and 4) to independent BNC outputs (i.e. signal1 and signal2)
1. During experiments, connect the BNC cables to this auxiliary board and the power supply terminals to the appropriate locations on the board. Do not leave the power supply connected when not in use.


# Usage Instructions

Once you have an assembled device ready to use, follow these steps to successfully read a heart rate signal from a cockroach:
1. First, test the electrical parts by connecting the mini-PCB and auxiliary board with the 5-pin ribbon cable. Connect the BNC outputs to a data logging program (e.g. LabChart + PowerLab), and connect the 5V power supply to the auxiliary board
    1. To test whether the sensors and LEDs are working as expected, place a sheet of paper in front of the LEDs and sensors to see whether the sensor voltage decreases on your computer screen. This shows that the LEDs are shining light outward, which then is reflecting back onto the sensors, resulting in the sensor voltage reacting accordingly. Make sure to unplug the power supply when you are done testing!
1. Attach the mini-PCB onto the mount in a secure but reversible way. A small amount of transparent, residue-free tape works well
2. Next, narcotize the cockroach using CO2 for ~30s. This will immobilize it for a few minutes to allow for easy mounting of the mount and board
3. Microwave bikini wax until it has the consistency of honey (but ensure it is not hot enough to burn your skin or the cockroach) and use it to attach the 3D printed mount onto the third sclerite of the cockroach. Use the "wings" of the mount as the wax attachment surfaces, to ensure that the sensors and LEDs are not obscured by wax and to make them fit flush with the surface of the sclerite. Ensure that the sensors and LEDs are aligned with the midline of the roach, on the roach's 3rd sclerite
4. Once the mount and mini-PCB are attached firmly to the roach, connect the mini-PCB to the auxiliary board using the 5-pin ribbon cable. Finally, connect the auxiliary board to the power supply. As the cockroach slowly wakes up from being narcotized, the two signals should slowly become visible on your computer screen. It helps to manually rescale the axes on the screen to zoom into the heart rate signals being produced. Signals will typically range from 2-20mV in amplitude (peak-to-peak), depending on how closely your sensors and LEDs are to the surface of the roach  
