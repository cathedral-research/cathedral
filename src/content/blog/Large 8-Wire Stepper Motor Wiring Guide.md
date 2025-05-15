---
title: 'Large 8-Wire Stepper Motor Wiring Guide'
description: 'A short guide to wiring and controlling an 8-wire stepper motor'
authors: ['Jay Wilkerson']
pubDate: 'May 15 2025'
heroImage: '/blog-placeholder-3.jpg'
---

<img src="/src/content/images/tuchito.jpeg" alt="tuchito" width="200"/>

In my most recent project, I used an 8-wire stepper motor. When I went online to find out how to wire it up, there seemed to be a surprising lack of documentation. I decided to write up this quick explanation as a guide on how to wire and control an 8-wire stepper motor.

The equipment you will need for this are the following:
8-Wire Stepper Motor
Compatible Stepper Motor Driver
Microntoller (or other controlling method)

First, you must find the "loops" of wire pairs. If your motor comes with documentation, it will likely describe which wires pair together. Otherwise, there is a method for finding the pairs. This is done by measuring the resistance between wires with a multimeter. If the reading of the resistance is low (near zero), those two wires are a pair. With 8 wires, there are four pairs in total. Luckily for me, the wires for my stepper motor were colored in pairs (black and a black with white stripe, red and red with white stripe, etc.), so it was obvious which wires were pairs. Still, it was verified to make sure.

Second, you must choose the wiring configuration. There are three types - bipolar parallel, bipolar series, and unipolar (shown in Figure 1 below).


Figure 1: Stepper Motor Wiring Diagrams [1]

Bipolar parallel produces a high torque at high speeds. It requires higher current. Bipolar series produces a high torque at low speeds. From my searching, unipolar should be avoided, because it is outdated. It produces a lower torque and worse efficiency. For this project, the bipolar series was the best choice. For most applications, the bipolar series is best. The specific wiring is explained in a further section.

When it comes to controlling the motor, one thing is needed - a driver. The driver used for this project is the TB6600 Stepper Motor Driver. The driver needs to be chosen to match the specifications on the stepper motor, especially the current. A microcontroller will make it easier to communicate with the motor (through the driver), but it is not necessary. A wiring diagram of the motor, driver, and microcontroller is shown in Figure 2 below.


Figure 2: Stepper Motor Wiring Diagram with Driver and Microcontroller [2]

As shown in the Figure, there are two sets of pins on the driver. The top set is the signal. This is how the microcontroller (or whatever input system is used) communicates with the driver. Pins 1 and 2 (starting from the top) are the enable pins. These should be grounded. If powered, they actually disable the signal. Pins 3 and 4 are the direction pins. One of these is grounded while the other is powered. This indicates the direction, based on which is powered/grounded. Pins 5 and 6 are the pulse pins. This communicates how many pulses (or steps) the stepper motor should do.

The bottom set of pins are connected to the stepper motor. Pins 7 through 10 (labeled B-, B+, A-, A+) are where the wires from the stepper motor are connected. This is explained further in the next section. FInally, pins 11 and 12 are the power/ground pins. As indicated on the driver, it requires 9-40VDC. I used 24V and 2A for my setup, which seemed to have worked. There are a few switches on the top side of the driver. These are used to set the specifications for the driver. The first three switches are used to set the pulses and microsteps ratio. Any of these can be chosen, but you must make sure that your code matches what you choose. The second three switches control the current. This should match your input current and the current your stepper motor requires.
For bipolar series wiring (suggested), you must bring back your wire pairs (or loops). Take two pairs and connect one wire from each together. This is now your A loop. In Figure 3 below, look at the top four wires. The orange/white and black/white wires are connected together, while the orange and black wires are connected to the A+ and A- terminal. Repeat this process for the other two wires for the B loop.


Figure 3: Bipolar Series Wiring Diagram

Now the stepper motor will function as a normal 4-wire stepper motor. The four input pins (direction+, direction-, pulse+, pulse-) can all be controlled with a microcontroller.



References
[1]	LulzBot, "ht17-275 8 lead stepper motor wiring help," LulzBot, May 06, 2014. https://forum.lulzbot.com/t/ht17-275-8-lead-stepper-motor-wiring-help/587 (accessed May 15, 2025).
[2]	"3 PCS of TB6600 Stepper Motor Driver, ABuff 5A 9-40V Nema 17 Stepper Motor Driver CNC Controller Single Axes Hybrid Stepperr Motorr Controls - Amazon.com," Amazon.com, 2025. https://www.amazon.com/TB6600-Stepper-Driver-Controller-Controls/dp/B07GVFTHPT (accessed May 15, 2025).
