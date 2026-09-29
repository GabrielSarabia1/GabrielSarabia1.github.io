---
title: "Multi-material Pliers"
excerpt: "Designed and fabricated multi-material 3D-printed needle-nose pliers capable of gripping and picking up through-hole resistors, incorporating a flexible TPU spring for controlled opening and closing."
header:
  image: /assets/img/Engineering_Services_Banner.jpg
  teaser: /assets/img/IMG_0059.jpeg
gallery:
  - url: /assets/img/Cyber-Scooter-1.jpg
    image_path: assets/img/Cyber-Scooter-1.jpg
    alt: "placeholder image 1"
  - url: /assets/img/Cyber-Scooter-2.jpg
    image_path: assets/img/Cyber-Scooter-2.jpg
    alt: "placeholder image 2"
  - url: /assets/img/Cyber-Scooter-3.jpg
    image_path: assets/img/Cyber-Scooter-3.jpg
    alt: "placeholder image 3"
---
# Project Overview

This project focused on designing and fabricating a set of multi-material 3D-printed needle-nose pliers designed to grip and pick up through-hole resistors. The pliers use two rigid handles and a flexible TPU spring that allows the jaws to open and close during use. Print-in-place designs are 3D-printed parts that come off the printer already assembled and functional, without requiring post-processing or additional assembly. They rely on carefully designed clearances between moving components to allow joints and mechanisms to move freely. For print-in-place designs, PLA and PETG work well for rigid parts because they are easy to print and can produce accurate dimensions and clearances. TPU is useful when the design needs flexibility, such as a spring or flexible hinge. For multi-material designs like these pliers, combining a rigid material such as PLA or PETG with 95A TPU allows the rigid components to maintain their shape while the TPU provides the necessary flexibility.

The main challenge during the design process was developing a reliable way to connect the tweezers and handles while maintaining proper movement. My first iteration was smaller than the final design, which led me to increase the overall size of the 3D model. With additional time, I would have tested more size variations and further refined the CAD model. However, the printers were also being shared among the rest of the class, which limited printing availability and added to the time constraints of the project.

For this project, we used SuperSlicer to prepare the models for printing and experimented with the print settings to improve the flexibility of the spring. One of the main changes was setting the top and bottom layers to zero, leaving the spring without solid top or bottom layers. We also printed the spring at four different infill densities to compare their flexibility and determine which setting provided the best balance between movement and durability.

# Features

* Combines rigid handles with a flexible TPU spring.
* Designed for gripping small through-hole resistors.
* Three components can be hand-pressed together without tools.
* TPU spring returns the pliers to the open position.
* Designed specifically for additive manufacturing and minimal post-processing.

# CAD Model

<iframe src="https://a360.co/4iUl9uK" width="800" height="600" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true" frameborder="0"></iframe>

{% include gallery caption="Iterations and final multi-material pliers." %}

# Pliers In-Action and Disassembled

![Pliers in action](/assets/img/Adobe Express - IMG_0060.gif)
