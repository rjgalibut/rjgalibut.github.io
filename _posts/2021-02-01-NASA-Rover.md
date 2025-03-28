---
title: NASA Planetary Rover
layout: post
date_range: February 2021 - August 2021
post-image: "https://raw.githubusercontent.com/rgalibut/rgalibut.github.io/main/assets/images/NASA%20Rover/Rover%20Cover%20Image.jpg"
description: Remote-controlled rover prototype that collects visual and sensory data about environment. 

---

This project was completed for the Microcomputer and Robotics Internship hosted by NASA and the California Space Grant Consortium as part of their Community College Partnerships.

For this internship, the participating student body were asked to build a small-scale prototype of a planetary rover (inspired by Perseverance and Curiosity) that could be controlled remotely and collected visual and sensory data about its surroundings. We would then present our finished product, along with other schools, to the California Space Grant Consortium internship leaders.

As part of a group focused on camera control, we were also tasked with creating a program to control the camera mounted on the front of the rover in order to collect visual information. 

Together with the other groups, the goal of the project was to incorporate all groups into a larger embedded system that would include weather (temperature) reading and position information.

Due to the time constraint of the internship, our group and the remaining groups were unable to incorporate the entire system in time for the presentation. Given more time to complete the project, we would have liked to implement computer-vision guided obstacle avoidance as our contribution to the overall system.

<p style="text-align: center">
Jump to: 
<a href="#building">Building and Wiring</a> | <a href="#motor">Motor Control</a> | <a href="#camera">Visual Feedback</a> | <a href="#flask">Flask</a> | <a href="#videos">Videos</a> | <a href="#teamvideo">Team Video</a>
</p>

---

<h1 id="building">Building and Wiring</h1>
The first task of the project was to build the rover by wiring components to a breadboard connected to a Raspberry Pi. The logic rail of the breadboard was powered by a portable power bank, while the power rail of the breadboard pulled from a disposable battery pack. The wheels were connected to motors, which were soldered and wired to the power rail of the breadboard. Lastly, the camera was mounted to front of the rover, plugged into the Pi, and wired to the power rail.

<table width="100%">
  <tr>
    <th style="text-align: center">Materals (minus camera)</th>
    <th style="text-align: center">Final Assembly</th>
  </tr>
  <tr>
    <td style="text-align: center" width="50%"><img style="margin: 0 auto" src="https://raw.githubusercontent.com/rgalibut/rgalibut.github.io/main/assets/images/NASA%20Rover/Materials.jpg" alt="Materials"/></td>
    <td style="text-align: center" width="50%"><img style="margin: 0 auto" src="https://raw.githubusercontent.com/rgalibut/rgalibut.github.io/main/assets/images/NASA%20Rover/Assembled.png" alt="Assembled"/></td>
  </tr>
</table>

---

<h1 id="motor">Motor Control</h1>
To control all four wheels, we used a dual H-bridge motor driver connected to 4 DC gearbox motors. This was my first time working with a motor driver so I frequently referred to documentation and conducted research to troubleshoot issues.

The motor polarity was initially controlled using a computer keyboard (arrow keys) and the motor speed for each direction was preset through code. The area that the rover could travel was limited to the room that I was controlling it from, since I had to be able to see it visually and also control it from my computer.

<table width="100%">
  <tr>
    <th style="text-align: center">Wiring</th>
    <th style="text-align: center">Wiring (Dual H-Bridge)</th>
  </tr>
  <tr>
    <td style="text-align: center" width="50%"><img style="margin: 0 auto" src="https://raw.githubusercontent.com/rgalibut/rgalibut.github.io/main/assets/images/NASA%20Rover/Wiring1.jpg" alt="Wiring"/></td>
    <td style="text-align: center" width="50%"><img style="margin: 0 auto" src="https://raw.githubusercontent.com/rgalibut/rgalibut.github.io/main/assets/images/NASA%20Rover/Wiring2.jpg" alt="H-Bridge"/></td>
  </tr>
</table>

---

<h1 id="camera">Visual Feedback</h1>
The Pi Camera was mounted to the front of the rover using a pan-tilt assembly with 2 servo motors: one servo for left/right panning (yaw) and a second servo for up/down tilting (pitch). The camera has the standard 75-degree angle, with the ability to capture images and record video. The image quality was not the best but was sufficient to gather visual data needed for navigation.

After testing the maximum range of the camera in all directions, we decided to mount it to the front in such a way that the rover would not get in the way of the visual feed when pointed downward at its maximum angle. 

--- 

<h1 id="flask">Flask Website</h1>
With both the motor and camera implemented, it soon became messy to map all of their functions to the keyboard. I wanted to optimize this somehow and decided that controlling them via website would be a good compromise.

So I designed a website using the Python-based web framework, Flask. This site would allow any user connected to the same network as the rover to remotely control the direction of its 4-wheel drive (forward, reverse, left, right) and its velocity (stop, speed up, slow down). The site also allowed users to control the direction of the mounted Pi camera (tilt up, tilt down, pan left, pan right, reset) and record (picture, video).

The buttons on the site were mapped to specific Python functions that would then actuate their respective devices. For example, the camera position reset was defined as the middle position of both pan and tilt directions, actuated by the servo motors. Unfortunately I was not able to implement motor speed control or camera capture functions by the project's end. Motor speeds are preset through code and the camera moves but doesn't capture images or video. However, these functions can be added in future iterations.

I had no prior experience using or coding Flask so this was an area I heavily researched for this project. I had previous knowledge on website design using HTML and CSS, and writing functions in Python. However, incorporating markup language into Flask proved to be tricky and required many rounds of debugging before the final presentation.

---

<h1 id="videos">Test Videos</h1>
#### Motor Control
Testing forward, reverse and turning abilities.

Turns had to be adjusted so that the outer wheel moved faster than the inner wheel or vehicle would not turn at all. Motor speed was decreased for debugging purposes.

<div class="video-container">
  <iframe src="https://drive.google.com/file/d/1Oy4V4t_OurnBc5SSoQr02i5SIDcMhZnG/preview" width="640" height="480" allowfullscreen></iframe>
</div>

#### Camera and Motor Control
Initial test of Flask buttons to control motor and camera direction/speed.

<div class="video-container">
  <iframe src="https://drive.google.com/file/d/1knPpWj8HETYZ9V7VRa845SO89bCPfMmV/preview" width="640" height="480" allowfullscreen></iframe>
</div>

#### No Obstacles
Testing 360° rotation ability on tile floor and simple navigation.

<div class="video-container">
  <iframe src="https://drive.google.com/file/d/1ydmtgQlFw_EuCZHzTkEa5OLQGG42g3V7/preview" width="640" height="480" allowfullscreen></iframe>
</div>

#### Obstacle Navigation
Test of manual navigation around obstacles. As can be seen, rover can still bump into objects which may be improved using an ultrasonic distance sensor on the back of the rover.

Camera shakiness possibly due to the servo PWM signal changing while printing information to the terminal.

<div class="video-container">
  <iframe src="https://drive.google.com/file/d/1IbFQCn-PuSVpjNxVLcmYBihCq2y9bJk5/preview" width="640" height="480" allowfullscreen></iframe>
</div>

---

<h1 id="teamvideo">Camera Team Video</h1>

<div class="video-container">
  <iframe src="https://drive.google.com/file/d/1nwmznj4zyXLdDg1cqwvoWeR5b80En3WM/preview" width="640" height="480" allowfullscreen></iframe>
</div>

<div style="text-align: center">
  <a href="#top">Back to top</a>
</div>