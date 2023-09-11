---
layout:     post
title:      "Colpitts oscillator"
description: "A 2.4GHz Colpitts oscillator with FBAR resonator."
date:       2023-05-12 09:00:00
author:     "Jin Wook Lee"
header-img: assets/img/FBARoscillator1.png
---

# The Colpitts oscillator

The second Integrated Circuit Design project involved designing a 2.4GHz oscillator using a piezoelectric resonator called the FBAR (thin-film bulk acoustic resonator). The circuit diagram was provided to us, as shown below. We needed to find the optimal component values to minimize phase noise and power consumption to target specifications.

<p align="center">
    <img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/FBARoscillator2.png" width="60%">
</p>

To approach this project, I began by making calculations for approximate device sizes. I first determined the resistance and reactance of the FBAR model, and only examined a single-ended half of the oscillator. After determining the small-signal model and making assumptions of transistor transconductance, I found a relationship between the two external capacitors and single resistor. Setting one of the capacitors to a reasonable size allowed me to get an approximate for the size of the second capacitor.

Through Cadence simulations, I then experimented with various transistor sizes and numbers of fingers. I also experimented with various capacitor values around the calculated values to determine the affect on phase noise. The difficult task was balancing loop gain maximization with phase noise minimization, but the best approach turned out to be altering the external resistor's value and consequently reducing transistor sizes to draw less power consumption.

Even with a given circuit diagram, it was difficult to juggle external component values, as well as the transistor sizes to find the sweet-spot for operation. The process went through iterations: I first looked at the circuit through a lens focused on loop-gain, then a lens focused on power-consumption, and then a lens focused on phase noise... etc. I also learned that the theoretical calculations from circuit analysis differs from simulations using with idealized components; moreover, these simulations with idealized components differ from those with real industry-provided component models as well. (In fact, it's not just a matter of slight performance differences, but the entire circuit's region of operation going into saturation!) I also completed a post-design layout... I'm extremely curious to see how different layout geometries further affect performance as well. How far away will the actual performance of the physical circuit be? There's so much more to experiment.