# Quantitative Phase Microscope (SHARC) Protocol - work in progress!

Author: Nathan J. Day

Date: October 2020

## This protocol outlines how to initiate a time-lapse acquisition on the Lowe Lab's SHARC QPI microscope. 

Contents: 

- Microscope layout
- Microscope infrastructure 
- Step-by-step usage instructions
- Notes

## Microscope Layout

The microscope is located on an optical table with pneumatic stablisation. The computer is located adjacent to the optical table on a separate stand. This type of microscope is incredibly sensitive to vibration hence separate computer stand.

"Omega box" - imaging chamber heating device. On/off switch at back. **_check this_**

"Hammamatsu box" - camera. On/off switch at side  **_check this_**

"Thorlabs with LCD screen" - SLD controller. **_add switch location_**

"Full range" device - Acousto-optical tunable filter (AOTF).  **_add switch location_**

"Isotech" device - Spatial light modulator (SLM).  **_add switch location_**

Lasers power packs are located direclty above the optical table on the shelf. Power is controlled by a key at the back of the packs. Turn the key then press the power button at the front of the pack.  **_check this_**

**_Insert labelled picture of microscope here_** 

## Microscope Infrastructure

The microscope has fluorescence, quantitative phase and super-resolution capabilites (this guide does not include super-resolution operation instructions). The imaging chamber is heated by a kapton heater with PID controller. 

## Step-by-step usage instructions

1. Software set up

    - Navigate to the required program at `Start>Labview>Open Recent> Widefield Image Acquisition.vi>RUN`
    - LD output needs to be "ON"
    - SLD power set to 5
 
2. Focus the system

    - Focus step size: 1μm
    - Live mode (use `Get Phase Image` for final focus assessment)
    - Explore range of piezo manual control (1-100μm) for focal point
    - If focal point seems out of range (beyond 100μm), then bring to middle of range and manually reduce z-point of stage, using bottom left screw (turn anticlockwise). This bring the stage and objective closer together whilst also bringing the focal point into the range of the piezo. 
    
3. Phase alignment

    - Navigate to the required program at `Start>Thorlabs APT user`, then maximise the bottom right window, then `Load fine adjustment`. **IMPORTANT** Ensure that **fine** adjustment is loaded, **not** coarse. 
    - Open the shutter for the interference arm by pressing the `Open` button on the 640nm laser black box, located under the imaging chamber. 
    - Tweak alignment using tactile knob next to interference shutter. It is typical to adjust downwards due to addition of a sample with more liquid on than previously imaged. 
    - Aim for maximum range of pixel intensity values, displayed in the top right hand corner of the image field. An example of this is 12,000-1,000, but can vary according to sample. 
    - Adjust the vernier screw under the imaging chamber to tilt the mirror until a striped pattern appears. **_add example image_**
    - Adjust the position of the mirror using fine adjustment settings in the Thorlabs ATP user program until the stripes have even contrast across the whole field of view. A previous position of the fine adjustment has been 4.5482, but this is heavily dependent on sample. 
    
4. Fine focus

    - Turn laser key on
    - LD output off
    - Laser to 10-20% power
    - Exposure to 20-200ms
    - Shutter set to open. The shutter for the laser is on the 561 black box. **IMPORTANT** Ensure that the imaging chamber is not opened whilst the laser shutter is open. 
    - Fine focus can now be set to a graduation of 0.2μm and browsed until image is adequate. 
    
5. Image acquisition
    
    - Store position
    - Ensure all lasers and diodes are on and shutters are open. 
    - Start timelapse
    - Multiple positions: YES
    - Existing parameters: NO
    - Parameter definitions: 200ms, 240s, autofocus only for GFP (cannot handle RFP), 1 phase image per fluorescence
    - **IMPORTANT** Check the shutters are open before next step
    - Saving output folder (YYMMDD) will start the acquisition. **IMPORTANT** When clicking save, lift the mouse off the mousepad and click in mid-air. Yes, the microscope is that sensitive and if you do not do this the vibrations from your click will corrupt the first phase image. 

## Notes

#### Cell Culture 

35mm Mattek dishes recommended for use. Imaging chamber should be left to warm up for an hour or two before sample is placed in position. 

#### Potential errors

Check the shutters are open before acquisition. When using the mouse to acquire an image ensure that the mouse is not on the mousepad else the vibrations will corrupt the phase image. 
