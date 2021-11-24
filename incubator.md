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

The microscope is located inside a standard cell culture incubator, with an added water pump to maintain humidity. The incubator microscope is located to the right of the desktop computer used to control it, in front of the incubator CO<sub>2</sub> supply cylinder. On/off switch located just above the front left foot of the incubator.

"Control 2" - stage controller. On/off switch located at the back of the box. Top left button for the Z position. 

"Niji blue box" - LED controller. On/off switch located at the back left side (also has a power pack to the left, generally always on). 

"Thorlabs" - precision stage control. On/off switch at the back left side. 

![Kraken_labelled](https://user-images.githubusercontent.com/16838461/111985628-be135480-8b04-11eb-8765-0c87603f3bde.png)


## Microscope Infrastructure

The CO<sub>2</sub> cylinder requires replacing approximately every 1.5-2 months. This replacement is done by BOC (contact SMB orders: `smb-orders@live.ucl.ac.uk` asking for a BOC 40-B CO<sub>2</sub> cylinder replacement to Darwin B.03A/B. You may need to supply a grant code and contact telephone number). 

Once the water pump tank has less than 10cm depth of water it will require refilling with approximately 800mL-1000mL of distilled water (available from the LCN).

## Step-by-step usage instructions

1. Turn the system on 

    - Follow the microscope layout section above and turn on all the necessary components. 

2. Start Micromanager Gamma

    - Preexisting configurations should suffice
    - 2x2 binning needs to be set, as default is "OFF"
    - Exposure option here is for live feed of microscope field of view, the exposure set later in `Params.json` will overide this during the time-lapse acquisition
    - Select channel for live-view browsing (sometimes need to toggle filter wheel option from 0 to 1).
    
3. Store image positions for future time-lapse acquisition

    - `Stage` button opens the position list
    - `LIVE image acquisition` button to show current field of view 
    - Mark positions of interest using `MARK` button
        - When focusing the Z position, it is advisable to use similar power and exposure settings to what you will later define for the time lapse exposure, in the parameters "Params.json" file. It is also advisable to view the live image with contrast limits that are as wide as possible to gauge a better view of how in focus the whole image pixel range is. Narrowing the contrast limits may cause one to focus on the wrong features, for example a irrelevant bright spot of fluorescence
    - Save positions of interest using `Save As...`, path must match the new experiment directory path specified later in the `Params.json` file
        - When selecting the number of positions, bear in mind the number of image acquisitions for each channel that will need to be completed within the defined frame rate. For example, the microscope will struggle to complete more than 12, 4-colour positions within a 4 minute time period. It is advised that at least 30 seconds is left for the microscope to return to the origin position between frame acquisitions.
    - Leave cell sample for >2 hours to allow for it to equilibrate with incubator environment
        - Do not open the incubator in this time period. Try not to disturb the incubator at all after the initial positions are set
    - Update the focus on all positions and resave position list

4. Set parameters

    - In order to start imaging, the acquisition parameters must be set in the following file:
        `C:\User\Microscope\Docs\Octopus_lite_v2\Params.json`
        or 
        `C:\User\Microscope\Docs\Octopus_lite_v2\Params_[username].json`
    - You can find an example of this file in this repository, it is advised to not change any parameters you are uncertain of. 
    - In this file you can specify the acquisition channels as `BF, GFP, RFP, iRFP`
        - If using the iRFP channel, a Z-position offset needs to be defined. It is advised that this is manually calculated for your sample by viewing the focal depth difference in the live view. A previous value that has been used for 24-well plates is -3.4μm. 
    - Before setting the number of channels and the `num_images`, try to ensure that there is enough hard drive space to finish the entire acquisition. A 4-channel, 24 position, 1200 frame acquisition can be up to appoximately 350GB.
    - The most important aspect of the parameters file is to define the path to the previously saved position list (`stage_positions`) and the path to the output data folder, where the images will be saved
    - Once the relevant paramters have been defined, be sure to save the `Params_[username].json` file in the `User\Microscope\Documents\Octopus_lite_v2` directory, with your username added to the filename if you have changed any of the parameters
    
5. Start acquisition

    - Close Micromanager
    - Click the ACQUIRE shortcut on the desktop
        - If this does not work then open Anaconda Prompt from the start menu, navigate to Octopus_lite_v2 directory using bash commands (`cd User\Microscope\Documents\Octopus_lite_v2` and enter the command `python run.py`
    - Select the params file you just saved out using the numbered index shown in the Anaconda Prompt terminal
    - The acquisition should then begin to run, printing out the progress in the terminal window
    
6. Checking the acqusition 

    - Open ImageJ
    - Navigate to ouput path and open as virtual stack
    
7. Stopping the acquistition 

    - **CAUTION** Wait until acqusition loop is finished before closing the terminal to end acquisition. 
    

## Notes

#### Storage

Clear your data off the local hard drive as it has limited space. Move to server ASAP please. 

#### Cell Culture 

24-well glass bottom plates recommended for use. 35mm Mattek dishes require the use of a metal bracket which can result in an uneven Z plane or damage of the lens if not very careful. 

#### Stage Z position

The stage should be left at the -8000μm Z position when finished.

-6000μm is a good starting position for 24-well plates. -6200μm is an approximate focal plane for 24-well plates. 

#### Error messages

The Thorlabs precision stage controller is sometimes problematic: an error will arise that states `Java.sc unresponsive`. To circumvent this error shutdown micromanager, reboot the Thorlabs controller and restart micromanager.

**_Are you having a live-view problem?_** The filter wheel doesn't always go back to the correct starting position after using the iRFP channel. If this is the case then toggle the filter wheel option from 0 to 1
