# Custom Open Joystick Display Theme Tutorial

Note that the official [theme development docs on the Open Joystick Display repository](https://github.com/KernelZechs/open-joystick-display/blob/master/docs/theme-development.md) go into much greater detail than this document, and are a fantastic reference. The goal of this doc is to get you started with a minimal setup quickly so that you learn the basics. Once you're comfortable with setting up a basic theme, I highly recommend checking out the OJD documentation.

This document will help you get set up with a minimal SNES-style controller input display custom theme. Note that this description will be based on a Windows OS, but I believe the steps would be similar for Mac or Linux as well.

## Required Software

- [Open Joystick Display](http://kernelzechs.com/open-joystick-display/)
- A vector graphics program - [Inkscape](https://inkscape.org/) is free and excellent
- A plaintext editor - I prefer [Notepad++](https://notepad-plus-plus.org/downloads/) or [Sublime](https://www.sublimetext.com/). Note that word processors like Microsoft Word will _not_ work for this.

## Steps

1. From the Open Joystick Display link above, go to the 'Binary Downloads' link for your operating system, and download the zip file for v2.8.0 (the 64 bit Windows link is [here](http://kernelzechs.com/downloads/open-joystick-display/client/windows/stable/x64/open-joystick-display-2.8.0-x64-windows.zip)).

2. Unzip the directory wherever you'd like, then within the unzipped directory create a new directory `themes`. For example if your unzipped directory is `C:\Users\DrMario\Documents\Streaming\open-joystick-display-2.8.0-x64-windows\` you'll want to create `C:\Users\DrMario\Documents\Streaming\open-joystick-display-2.8.0-x64-windows\themes\`

3. Within the `themes` directory, create another directory that will contain your theme. For now call this `myTheme` (so eg: `C:\Users\DrMario\Documents\Streaming\open-joystick-display-2.8.0-x64-windows\themes\myTheme`). You can change this name later when you understand how the pieces fit together.

4. Download and save the following files into your `myTheme` directory:
    - [theme.json](https://raw.githubusercontent.com/drx-mario/openJoystickDisplayTutorial/main/theme.json)
    - [theme.html](https://raw.githubusercontent.com/drx-mario/openJoystickDisplayTutorial/main/theme.html)
    - [theme.css](https://raw.githubusercontent.com/drx-mario/openJoystickDisplayTutorial/main/theme.css)
    - [basicController.svg](https://raw.githubusercontent.com/drx-mario/openJoystickDisplayTutorial/main/basicController.svg)

5. Launch `Open Joystick Display.exe` from the directory you unzipped it into. Once OJD loads, click the 'Select Folder' button in the 'Profile Theme' section on the left side of the window, then select the `themes` folder you created earlier (NOT the `myTheme` folder).

6. Click on the 'Theme:' drop-down menu on the left side of the window and scroll down to the bottom of the list. You should see 'User Themes:' and then 'My First Theme'. Click on this, and you should see the grey controller template image load.

7. The next step will vary depending on what controller mapping you're using, but you'll need to find your correct controller in the drop down under 'Profile Mapping'. Many common controllers (PS4, iBuffalo, XBox 360) have pre-assigned button mappings you can choose from this list. If you need to customize your button mappings, please consult the Open Joystick Display docs.

8. Once you've selected your controller, press a few directions on the D-pad. You should see the corresponding buttons light up on the display. 

9. Now try pressing some of the buttons. Nothing's happening, why not? Well, we need to tell OJD which parts of the image to light up when buttons are pressed. 
    - Press the button on your controller you'd like to map to the bottom left position of the image (eg: Y on SNES, Square on PS4, etc). Notice what happens in the 'Input Tester' section of OJD (bottom center). One of the numbered circles should light up in the 'Buttons' section. Now look on the right side of the window and see where the number of that button is, and what the value in the "Label" column next to that button's number is. For example you might see the button "2" light up, and next to "2" on the right side of the window you might see "Y" in the "Label" column. Remember this 'Label' value!
    - Open up the basicController.svg file in your text editor, like notepad++. Now search for "id="yBtn". You should find the following code:
    ```
     <circle
       style="fill:#999999;fill-opacity:1;stroke:#cccccc;stroke-width:1.58258593;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1"
       ojd-button=""
       class="snes-button"
       id="yBtn"
       cx="343.15158"
       cy="-117.33107"
       r="35.890789"
       transform="matrix(0.72014014,0.69382863,-0.72014014,0.69382863,0,0)"
       inkscape:label="yBtn" />
    ```
    This code defines a circle that's being associated with the 'Y' button on a SNES controller. The line that reads `ojd-button=""` is what makes the connection between the image and the controller for OJD. In between the double quotes, you should type the "Label" value of the button that you noticed in the "Input Tester" section. The list of possible button names is: A, B, C, X, Y, Z, CROSS, CIRCLE, SQUARE, TRIANGLE, L, L2, L3, R, R2, R3, START, SELECT, ACTION, PS, XBOX, CAPTURE, RUN, PLUS, MINUS, HOME, UP, DOWN, LEFT, RIGHT, CUP, CDOWN, CLEFT, CRIGHT, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20.
    For example if 'Y' was the label, this section should now look like:
    ```
     <circle
       style="fill:#999999;fill-opacity:1;stroke:#cccccc;stroke-width:1.58258593;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1"
       ojd-button="Y"
       class="snes-button"
       id="yBtn"
       cx="343.15158"
       cy="-117.33107"
       r="35.890789"
       transform="matrix(0.72014014,0.69382863,-0.72014014,0.69382863,0,0)"
       inkscape:label="yBtn" />
    ```
    Once you've made the change, save the file and click 'Reload' in the top left of the OJD window. Now when you press the button you remapped, you should see it light up on the controller image!
    
9. So how did we know to look for `id="yBtn"` in the .svg file? To answer that, let's open up the basicController.svg file in Inkscape. Left click on one of the buttons in the image to select it, then right click and select "Object Properties..."

10. You should see a panel show up that has a field labeled "ID:" with a value like "xBtn", "aBtn", etc. This is what creates the `id="yBtn"` line in the file that we use to figure out where the buttons we want to map are. 
    - **NB** - if you change this ID, be sure to click the 'Set' button below the field then save the file, or else the ID won't be stored!

11. By now you should have all of the tools you need to experiment! Try dragging the buttons in the image around, changing their colors, or deleting them and making new shapes. As long as you give them an ID that you can remember, you can save the file, open it up in a text editor, and look for that ID. Just make sure that in the same section (ie: in between the angle brackets in the code above) you have lines that say:
`ojd-button="YOUR_BUTTON_LABEL_FROM_OJD"`
`class="snes-button"`.
    - For example if you made a brown rectangle and gave it the ID "myNewRectangleButton", you might see:
    ```
    <rect
       style="opacity:0.71199999;fill:#784421;fill-opacity:1;stroke:#cccccc;stroke-width:2.5;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1"
       id="myNewRectangleButton"
       width="64.649765"
       height="54.548237"
       x="238.39603"
       y="24.531998"
       ry="0"
       inkscape:label="myNewRectangleButton" />
    ```
    
    To map this to your X button, you could then update this to look like:
     ```
    <rect
       style="opacity:0.71199999;fill:#784421;fill-opacity:1;stroke:#cccccc;stroke-width:2.5;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1"
       id="myNewRectangleButton"
       width="64.649765"
       height="54.548237"
       ojd-button="X"
       class="snes-button"
       x="238.39603"
       y="24.531998"
       ry="0"
       inkscape:label="myNewRectangleButton" />
    ```

12. Explore, try new things, and have fun! There are a ton of great Inkscape tutorials out there, and a bunch more useful information about OJD themes at [the official OJD github](https://github.com/KernelZechs/open-joystick-display/blob/master/docs/theme-development.md). Enjoy!

