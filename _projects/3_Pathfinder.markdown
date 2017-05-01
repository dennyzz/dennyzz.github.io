---
layout: post
title: Project Pathfinder
description: An Autonomous Lane Tracking RC vehicle
imgroot: /images/projects/pathfinder
img: /thumbs/cover.jpg
---
# Work In Progress
<div>
	<img class="col three" src="{{ site.asseturl }}{{ page.imgroot }}/thumbs/pathfinder.jpg" alt="The Pathfinder Vehicle" title="The Pathfinder Vehicle"/>
</div>
<div class="col three caption">
	The Pathfinder vehicle almost fully assembled
</div>
Project Pathfinder was completed for EECS452 (Digital Signal Processing) over the course of 3 months

*Much of the material here will be pulled from the various reports done in class.*

## Project Goal
Design a system that can accomplish some features of autonomous driving. The main features explored are lane tracking and following, as well as a simple collision detection and avoidance feature. The end demo will have the vehicle be able to traverse a simple oval track with limited to no human intervention. This is mostly done for educational purposes and to satisfy some curiosity as to how these technologies work. 

## Github Repository 
[Github](https://github.com/{{ site.profiles.github }}/452-Pathfinder)

## Hardware Architecture
The hardware is based around a heavily modified 1/24 scale RC car bought online with the computation occurring on a Raspberry Pi 3
- RC Car Chassis 
- Raspberry Pi 3
- VL53L0X breakout module
- Pi Camera 2.1
- SG90 Servomotor
- High Torque 130-sized Hobby Motor
- 3x 18650GA batteries
- Custom Chassis Controller

The hardware runs around 3 main components. the Raspberry Pi, the Car Chassis, and the VL53L0X module

### Raspberry Pi
The Raspberry Pi is mounted under the roof of the RC car with some screws and standoffs to hold it in place. The Pi camera is attached with a custom mount to the top of the roof which allows us to set a camera angle. This higher position emulates the view of a windshield mounted camera for a slightly larger vehicle, but simplifies the mechanical fitting of the camera. Having a higher camera mount with extra clearance also allows us to tilt downwards more and have a clearer view of tighter turns, which helps us get around the usual problem where one forwards-facing camera is only useful for highway driving with its wide-sweeping curves, since it can't see the lines if the turn gets too tight.

### VL53L0X Module 
For the distance sensor, we wanted to simplify our problem to split the lane detection algorithm which runs on the camera and the collision detection sensing, to make sure we would be able to implement them within the deadline. Our board is bought from Pololu and has the basic breakout and mounting holes. There are many other options that could have been chosen, but to modularize our design, we opted for a distance sensor that could communicate directly with the Raspberry Pi. It also had to have a small size so that the sensor could be mounted inconspicuously and not be in the view of the camera. 

### Car Chassis
We were told repeatedly by our TAs not to use a cheap RC car as the body of the vehicle. The main problem being the difficulty of precisely controlling the speed and steering angle. This was an obvious drawback for the vehicle. The onboard bang-bang steering in the RC car did not sit well with precisely controlling our angle to match the curvature of the track. And so armed with a pair of pliers, some glue, and an SG90 micro servomotor, some chassis surgery was completed that replaced the original motor with the servo and granted us precision control of the steering angle from full left to full right. The second modification as to the center of the chassis. Since we no longer needed the remote control functionality in the RC car, and I wanted longer lasting batteries than 3xAA, the entire middle section was gutted. The only thing left over was the flat plastic base of the vehicle which included a now glued on battery door. The last shortcoming was with the drive motor. The motor in the car did not have enough torque to allow the car to drive slowly, it would only go fast or not at all. This proved rather difficult with developing the algorithms as testing at slower speeds is much easier to start with. Thus the final modification was to replace the drive motor with a similarly shaped motor with higher torque. This simple swap solved the our slow speed driving and kept the rear section of the car relatively unchanged. The few finishing touches were to replace the car lights with LEDs for bright white headlights and nice red brake lights, as well as the addition of an small character LCD screen to display the IP address of the raspberry pi. 
<div>
	<img class="col two" src="{{ site.asseturl }}{{ page.imgroot }}/thumbs/servosteer.jpg" alt="Servo Steering" title="Servo Steering Mechanism"/>
	<img class="col one" src="{{ site.asseturl }}{{ page.imgroot }}/thumbs/servosteer.jpg" alt="Servo Steering" title="Servo Steering Mechanism"/>
</div>
<div class="col two caption">
	The servo steering mechanism
</div>

## Software Overview
The software makes use of OpenCV python and numpy+scipy. The implemented lane tracking algorithm was largely based upon a paper found on the web titled "Extended-Search, Bézier Curve-Based Lane Detection And Reconstruction System For An Intelligent Vehicle." Some modifications and omissions were made to speed up development time. 

There are 3 distinct steps to the algorithm which will be explained in order. First is Lane Detection; there needs to be some component in the algorithm that can easily detect and identify the lane lines to provide some information as to where they exist in the image. Second is Lane Reconstruction; given a bunch of coordinates that exist on the lane edge that we are interested in, create a model that represents the lane in a simplified fashion. Third is parameter extraction. Now that we have a model for the lane line, we can extract useful parameters from the model to determine where we are relative to the lines, and how to best drive to stay inside the track.

### Lane Detection
The first step in creating a model of the track ahead of the vehicle is to somehow detect the lane lines. Shown below is a sample view from the camera perspective. From this sample, we can see that a small section from the image extracted near the edge of the line will appear as a darker triangle above a lighter triangle. This can be generalized to real asphalt roads, with the lighter triangle above, and darker triangle below. By changing the orientation of these triangles, we can selectively choose our background and foreground colors or which side of the line to detect. Taking the simple idea of looking for a triangle shape into real code, can be done simply by using correlation. First, we create a simple image that will represent the feature we are looking for. These shapes or masks, are shown in Figure 6. We can see that the mask is just looking for a diagonal edge where one side is darker and one side is lighter. With the masks created, we can correlate it with the image, but that would cost too much computation time. To reduce the amount of computation, we can use our prior knowledge about where the lane lines will likely begin and use that as a starting point. To represent this selection, two long strips are selected from the image near the vehicle on the left and right sides. These strips are shown in Figure 7. Now that a strip of the image containing a lane edge has been extracted, it is necessary to use correlation to ascertain the actual location of the edge. The process is shown in Figure 8. Once the correlation is completed, the lane edge location can be extracted by finding the location of the maximum value and checking to see that it passes a set threshold value. Once the first lane edge location is found, the search size can be reduced because the rest of the lane line should continue upwards from the initial point. When the search algorithm is finished iterating upwards, we will have a series of points that we are confident exist on each lane line.

Figure 5: Extracting Lane Edge Pixels


Figure 6: One image mask, B = -1/20 and W = 1/20


Figure 7: Initial locations for lane edge search


Figure 8: Correlating the mask with an image strip and the result


Figure 9: Iterating upwards. Red are left lane points, Blue are right lane points

### Lane Reconstruction
Using the extracted data points, we can move on to the next step in the algorithm: lane reconstruction. A set of coordinates for the lane edge is not the most useful format, so the data needs further processing. The simplest method for reconstructing a curve that matches the track is to fit a quadratic function onto the known edge points. Luckily this process is relatively light in terms of computation time, and is much simpler than other methods. The fit does a decent job at approximating the curvature of the lane, but does not extrapolate beyond the given points very well. However, the drawback does not affect the system very much because we will not use much information beyond the detected points. A visualization of the curve fitting is shown in Figure 10.

Figure 10: Fitting a quadratic curve to each lane line

### Parameter Extraction
Once the lane is reconstructed in an accessible manner, some parameters can be extracted and fed into a control loop to keep the vehicle driving within the lane. For our implementation of the algorithm, two values are extracted and fed into the motor control loop. The first value is a lane offset error. A location on the image can be found for the current location of lane center by taking a point on each of the lines close to the vehicle. Then the midpoint is found and set as the current lane center. By assuming that the center of the image lines up with the center of the vehicle, we can compute an error value for this lane offset by finding the distance between the location of the midpoint and the center of the image. The other value that extracted from the lane lines is a future lane angle. By having a forward-facing camera, we have some ability to see the upcoming lane, which helps greatly with turns. To find an angle measurement, we take a point on both lanes farther away from the vehicle, and use the slope of the quadratic curve to compute an angle. An average of the left and right angles is taken to model the angle of the track itself. This gives us some representation of the lane curvature ahead of the vehicle and makes taking curves much smoother. A visual representation of this process is shown in Figure 11.







[1] Huang, Xiaoyun et al. "Extended-Search, Bézier Curve-Based Lane Detection And Reconstruction System For An Intelligent Vehicle". International Journal of Advanced Robotic Systems 12.9 (2015): 132. Web. 30 Apr. 2017.