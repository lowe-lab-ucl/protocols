# Incubator Microscope "KRAKEN" Protocol - work in progress!

Author: Nathan J. Day

Date: October 2020

### This protocol shows how to initiate a time-lapse acquisition on the Lowe Lab's KRAKEN incubator-microscope. 

Contents: 

- Microscope layout
- Microscope infrastructure 
- Step-by-step usage instructions
- Notes

## Microscope Layout

The microscope is located inside a standard cell culture incubator, with an added water pump to maintain humidity. The incubator microscope is located to the right of the desktop computer used to control it, in front of the incubator CO<sub>2</sub> supply cylinder. 

"Control 2" - stage controller. On/off switch located at the back of the box. Top left button for the Z position. 

"Niji blue box" - LED controller. On/off switch located at the back left side (also has a power pack to the left, generally always on). 

"Thorlabs" - precision stage control. On/off switch at the back left side. 

**_Insert labelled picture of microscope here_** 

## Microscope Infrastructure

The CO<sub>2</sub> cylinder requires replacing approximately every 1.5-2 months. This replacement is done by BOC (contact SMB orders). 
**_Insert contact details here_** 

Once the water pump tank has less than 10cm depth of water it will require refilling with approximately 800mL-1L of distilled water (available from the LCN).

## Step-by-step usage instructions

1. Set parameters

    - In order to start an imaging, the acquisition parameters must be set in the following file:
        `C:\User\Microscope\Docs\Octopus_lite\Params.json` **_check path is correct, add example file_**
    **_clarify the following parameters in the example params.json shown above_**
    - In this file you can specify the acquisition channels as `BF, GFP, RFP, iRFP`
    - Other parameters include: 
        Do not change channel/filter wheel. Check hard drive space. Number of images is set at 1200 for a typical cell competition assay. Delay/frame rate. Date folder/output- be sure to finish with a "/". Name position list i.e. microplate 1. 
    - Once the relevant paramters have been defined, be sure to save the `Params.json` file. 


2. Start Micromanager Gamma

    - Preexisting configurations should suffice
    - 2x2 binning needs to be set as default is "OFF". 
    - Exposure option here is for live feed of microscope field of view, the exposure set in `Params.json` will overide this during the time-lapse acquisition. 
    **_tidy this section up a bit_**
    
    
3. Store image positions for future time-lapse acquisition

    - `Stage` button opens the position list
    - `LIVE image acquisition` button to show current field of view
    - Save positions of interest **_forgot what precise button to do this is called_**, path must match the path specified in the `Params.json` file
    
    
4. Start acquisition

    - Close Micromanager
    - ACQUIRE shortcut in Start menu **_needs clarification_**
    
5. Checking the acqusition 

    - Open ImageJ
    - Navigate to ouput path and open as virtual stack (to conserve memory)
    
    
6. Stopping the acquistition 

    - **CAUTION** Wait until acqusition loop is finished before closing the terminal to end acquisition. 
    

## Notes

#### Cell Culture 

24-well glass bottom plates recommended for use. 35mm Mattek dishes require the use of a metal bracket which can result in an uneven Z plane or damage of the lens if not very careful. 

#### Stage Z position

The stage should be left at the -8000μm Z position when finished.

-6000μm is a good starting position for 24-well plates. -6200μm is an approximate focal plane for 24-well plates. -0μm to -1000μm is the focal plane  **_-clarify which is the actual approx. focal plane_** 

#### Error messages

The Thorlabs precision stage controller is sometimes problematic: an error will arise that states `Java.sc unresponsive`. To circumvent this error shutdown micromanager, reboot the Thorlabs controller and restart micromanager. 
