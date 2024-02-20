---
title: Unmanned Surface Vehicle
summary: Motion control for underactuated USVs.
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

The motion control unmanned surface vehicle (USV)

## Trajectory Tracking Control for Differential-Driven USVs Considering Propeller Servo

Due to the fact that differential-driven USVs are underactuated and exhibit nonholonomic constraints, the tracking problem of underactuated USVs is particularly challenging. The adverse environment with unknown time-varying disturbances and model uncertainty add difficulty to controller design. However, current research mainly focuses on the design of outer loop controllers, namely speed and position control, while there is less research on the servo inner loop of propellera. The goal of most controllers is to design control laws with thrusts as the control input, without considering propeller control. This type of controller cannot be directly used because we cannot directly input given thrust values into the USV system, but instead use propellers to generate thrusts. In general, differential-driven USVs use electric motor as propellers, and the duty cycles of the motor serves as the direct control input for the system. Therefore, it is necessary to use differential equations to describe the dynamic process response of the motor from duty cycles to thrusts.

We propose a trajectory tracking controller for differential-driven USVs considering propeller servo control, which applies a system model with propeller motor duty cycles as the control input, allowing the controller to be directly applied to practical differential-driven USVs. The controller adopts the backstepping technique to process the third-order system, which includes an auxiliary dynamic system that handles input saturation for performance improvement of motor duty cycle input limitation. In addition, disturbance observers are established for external disturbances and unmodeled dynamics, and the estimated composite disturbances are used in the controller to compensate for the effects of uncertainties. In order to handle complex cascade functions, the Lipschitz continuity condition is introduced, and the relationship between thrust error and motor speed error is established. A rigorous proof is provided that the tracking error of the closed-loop system with the designed controller can be stable within a bounded region. The simulation and experimental results demonstrate the effectiveness of the proposed controller.

> **Z. Xu**, T. Han, W. Zhou, S. He and J. Xiang*, "Trajectory Tracking Control for Differential-Driven Unmanned Surface Vessels Considering Propeller Servo Loop," in *IEEE Transactions on Industrial Informatics*, doi: [10.1109/TII.2023.3316256](https://doi.org/10.1109/TII.2023.3316256).


## Path Following Control With Sideslip Reduction for Underactuated USVs

For underactuated USVs, due to the absence of force in the sway direction, the sway velocity cannot be actively controlled. The non-zero sway velocity naturally generated during turning can lead to the generation of the sideslip angle. For tasks that require a certain attitude of USVs, such as onboard photography and driving in narrow rivers, the sideslip issue is very detrimental to maintaining normal navigation posture. However, current research on the sideslip phenomenon mainly focuses on how to improve path tracking accuracy in the presence of sideslip angle, due to the position error it brings when using the line of sight (LOS) method for path following. There is a lack of research on how to reduce sideslip angle itself. Therefore, it is necessary to further explore the factors that affect the sideslip angle and find methods to suppress it.

We propose a path tracking controller for underactuated USVs with sideslip suppression, which can reduce the sideslip angle when tracking curved paths. This controller adopts a novel method that takes two points on the longitudinal axis of a USV as the control object, so that the position error of one point relative to the desired path converges to zero to ensure the accuracy of path tracking position, and the other pointcis as close as possible to the desired path to reduce the sideslip angle. Due to the fact that the path following task only occupies 1 degree of freedom (DoF), while underactuated USVs have 2 DoFs, this feature is utilized to simultaneously reduce the sideslip angle and allocate the desired surge speed with the redundant DoF. Therefore, the problem is transformed into a constrained optimization problem, with one point position error convergence as a constraint, and the optimization objective is for another point to be close to the expected path and the surge speed to be close to the target one. In addition, a surge speed regulator is designed to dynamically adjust the target surge speed based on the curvature of the desired path at the current position, in order to reduce the conflict between the two optimization objectives and achieve good effect of sideslip reduction. The simulation and experimental results show that the proposed method can significantly reduce the sideslip angle on the curved path.

> **Z. Xu**, S. He, W. Zhou, Y. Li and J. Xiang\*, "Path Following Control With Sideslip Reduction for Underactuated Unmanned Surface Vehicles," in *IEEE Transactions on Industrial Electronics*, doi: [10.1109/TIE.2023.3340191](https://doi.org/10.1109/TIE.2023.3340191).


## Experiment Platform Deisgn

A USV prototype is designed to perform experiments. The USV is differential-driven, with two aft propellers installed parallelly on the two sides. Electronic speed controllers are used for receiving PWM signals and driving propeller motors. The measurements of the USV prototype are listed in the following table.

| Items | Measurements |
|:-------:|:-------:|
| Length | 1.5 m |
| Width | 1.0 m |
| Height | 0.8 m |
| Draft depth | 0.1 m |
| Weight | 60 kg |

The USV is equipped with an STM32F407 32-bit micro controller unit (MCU) based on ARM Cortex-M4 core for motion control and gathering sensor data. An onboard computer with Intel J4125 CPU and 8 GB RAM is used for control scheme implementation. Robot operating system (ROS) Neotic is installed on the computer for processing sensor data and message transport. An inertial measuring unit (IMU) provides the MCU with angular velocity and acceleration information, and a global navigation satellite system (GNSS) module with real-time kinematic carrier phase differential technique (RTK) provides the onboard computer with position, speed, and attitude information. 
