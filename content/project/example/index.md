---
title: Example Project
summary: An example of using the in-built project page.
tags:
  - Control
date: '2016-04-27T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
---

A unmanned surface vehicle (USV) prototype is designed to perform experiments. The USV is differential-driven, with two aft propellers installed parallelly on the two sides. Electronic speed controllers are used for receiving PWM signals and driving propeller motors. The measurements of the USV prototype are listed in the following table.

| Items | Measurements |
|:-------:|:-------:|
| Length | 1.5 m |
| Width | 1.0 m |
| Height | 0.8 m |
| Draft depth | 0.1 m |
| Weight | 60 kg |

The USV is equipped with an STM32F407 32-bit micro controller unit (MCU) based on ARM Cortex-M4 core for motion control and gathering sensor data. An onboard computer with Intel J4125 CPU and 8 GB RAM is used for control scheme implementation. Robot operating system (ROS) Neotic is installed on the computer for processing sensor data and message transport. An inertial measuring unit (IMU) provides the MCU with angular velocity and acceleration information, and a global navigation satellite system (GNSS) module with real-time kinematic carrier phase differential technique (RTK) provides the onboard computer with position, speed, and attitude information. 
