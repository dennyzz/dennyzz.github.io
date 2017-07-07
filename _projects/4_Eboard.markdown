---
layout: post
title: Electric Longboard
description: an Electric Longboard Build
imgroot: /images/projects/eboard
img: /temp.jpg
---

# Work In Progress
Follow along as this build progresses
<div>
	<img class="col three" src="{{ site.asseturl }}{{ page.imgroot }}/temp.jpg" alt="Initial testing" title="Initial testing"/>
</div>
<!-- <div class="col three caption">

</div>
 -->
## Project Goal
Design a fully functional and customizable electric longboard. Using BMS and systems design knowledge gained from SolarCar work, create a custom pack and charging solution, as well as a custom remote control and UI. 

### Design Goals
[//]: # (Maybe put down almost a to-do list of goals to meet and keep up as this progresses)
 * ~~Build out a test battery pack (no BMS)~~
 * ~~Build out a VESC motor controller~~ the build failed, still parts for a second attempt, bought one instead
 * Build Drivetrain: Motor, Mounts, Pulleys, Wiring
 * ~~Preliminary tests with VESC + Nyko Kama~~
 * CAD modeling the final battery pack design
 * Internal Charger and BMS design
 * External "Fast Charger" design
 * Build the Battery Electronics

### Design Ideas/Process
To get started with this build, it is best to start simple and plan for increasing features as progress is made. In this way, I can start with the minimum viable product and build upon it as having a functional project is much easier to test with. This brings us to our core components
 * Deck + Trucks + Wheels
 * Motor + Motor Mounts + Gearing
 * Motor Controller + controller
 * Power Source

For further development, I can use my SolarCar experience to work on the rest of the systems. Battery Management Systems are a "core competency" so that can be personally designed, and maybe just for fun, a simple MPPT solar charger system can be added to make it similar to a solar car.

### Prototyping

The current functional prototype is mostly with off the shelf components so that I could have everything up and running to get some practice learning how to ride a longboard. I went ahead and bought a used longboard for cheap to have some base to start with which happened to be a Sector9 Blue Wave Lookout board. After a failed attempt at making the VESC PCB by hand, I went ahead and bought an assembled VESC and most of the other necessary mounting components. 
Right now the parts list stands at:
 * Sector 9 Blue Wave Lookout deck
 * Test 1S10P 18650B cell battery pack
 * VESC motor controller (TorqueBoards)
 * Emax 5335 BLDC motor (Feeling cheated because it is actually a 63mm diametermotor)
 * Nyko Kama controller for a quick controller
 * Misc connectors and wiring

The setup is currently functional but is restricted by the batteries which are only designed for 6.7A discharge. The longboard is also problematic because it is designed with drop through truck mounts, so those all have to be flipped to give enough room under the board for the drivetrain.

## Github Repository 
[//]: # (The repository will probably contain the custom stmf4 BMS firmware as well as PCB design and BOM lists)
Not yet setup, still working on initial HW design

## Other Sources
[//]: # (To link to sources for outside HW designs, other github repos, purchased parts can be put in the BOM )
* [VESC BLDC Controller HW](https://github.com/vedderb/bldc-hardware)
* [VESC BLDC Controller FW](https://github.com/vedderb/bldc)

## BOM

## Hardware Architecture

### Motor Controller

### Motors

### Motor Mounts

### Deck Selection

## Software Overview
