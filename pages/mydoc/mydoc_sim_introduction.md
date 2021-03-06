---
title: Simulator Introduction
tags: [simulator, get_started]
keywords:
summary: "When developing for the SSS you will often not have the hardware available to modify or look at. Running the standalone_sim.py gives you a virtual SSS screen to develop and debug on."
sidebar: mydoc_sidebar
permalink: mydoc_sim_introduction.html
folder: mydoc
comments: false
---

## simulator.py

This file holds the class definitions to both the individually simulated digit and individually simulated panels. 

### Digit

This class controls drawing the individual lines and dot of a seven segment digit. The init parameters consists of a display object, and x and y coordinates. The display object is a pygame surface object. The x and y coordinates are the top left corner of the digit on the passed in pygame surface display object. There is one member function called update. This takes a value that corresponds to each of the seven segments and the dot. The bit order is DP-A-B-C-D-E-F-G. It only updates the values that need to change.

### Panel

This class is all about simulating a hardware panel. It is 16 digits across and 6 digits down. The init function parameters are start_x, start_y, and display. These are the same concept as the Digit class above. The display parameter is a pygame surface object. The start_x and start_y parameters are the x y coordinates of the upper left hand corner on the pygame surface display object. This class has three members to mimic the functionality of the hardware panels. The first is raw2. This function takes x, y, value, and flush parameters. The x and y parameters controls which digit to draw on. The value parameter is value to be written to digit. The bit order is stated above in the Digit class. The flush parameters controls if the change to the digit gets updated with this function call. The flush function will take all of the changes to the digits that haven’t been displayed yet and “flips” it to the screen. The clear function does just that, clears the panel

## Standalone_sim.py

ThIs file holds the Simulator class and instantiation. The Simulator class creates a stand alone simulator of the physical SSS. Many of the methods in the class are to only be used internally and wouldn’t be called outside of the class. The init function takes the width, height, and demo_dir parameters. The width and height parameters are the pixel width and height values of the display. These values are 48 and 48. The demo_dir is the directory of where the demos are. This value shouldn’t generally be changed from the inherent value unless your demos are put else where. The start the simulator, instantiate a Simulator object and call the start method. The start method has a pygame control loop that handles the display. The simulator will hot load all the demos in the demo_dir location. It will create a clickable list of demos on the left side of the screen. On the top of this list is a reload button. Demos can be changed while the simulator is running and be hot reloaded. Upon clicking reload, make sure to reclick the demo you want to run to ensure the changes are activated. There is a more button at the bottom of the list. This button will go to the next set of demos is the number of demos is greater than 13. Continue to click on more to cycle through each page of demos. On the bottom of the simulator there is a black box. It may be concerning to see your demo not go all the way to the bottom of the screen. Don’t panic, that is normal. This special area shows when LIVES and SCORE updates are published on the output of your demo. You can input left, right, up, down, and enter commands to your game by pressing the left, right, up, down, enter keys. When you press one of those keys it will send a press command. When that key is released, it will also send a release command. When designing games it is important to remember that these two types of commands get sent. For an example of processing these commands checkout the playable snake and breakout games.