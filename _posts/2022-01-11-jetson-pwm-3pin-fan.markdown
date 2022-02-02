---
layout: post
title: "jetson pwm a 3 pin fan"
date: 2022-01-11 23:30:00 +0200
categories: python
---

How to PWM a 3 pin fan

I got a cheap 3 pin fan for my nvidia jetson. However it was really anoying that the fan was on all the time, even with the board turned off. I didn't want to spend 16 eur for a PWM fan with 4 pins and thought about using some transistors and doing the PWM part DIY-style.

Instead of starting from scratch I found this really useful instruction:
<https://www.baldengineer.com/pwm-3-pin-pc-fan-arduino.html>

I went ahead with the identical schematic for the driving of the fan.
Here are some pictures of the assembled parts:

<img src="/docs/assets/images/front.jpg" alt="Front of the pcb">
<img src="/docs/assets/images/mounted.jpg" alt="PCB mounted between jetson and the fan">

I tested the fan with 'jtop', selecting the fan speed manually. For some reason for my fan only values between 50% and 100% were working. Below 50% the fan would just stop spinning. Anyway, it works.