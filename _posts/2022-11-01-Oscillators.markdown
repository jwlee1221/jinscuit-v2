---
layout:     post
title:      "Oscillators"
description: "A 20kHz Phase-shift oscillator, and a 40MHz Colpitts oscillator."
date:       2022-11-01 09:00:00
author:     "Jin Wook Lee"
header-img: assets/img/oscillator1.png
---

# The Oscillators

In Junior labs, we were tasked to design a 20kHz oscillator on a breadboard.

I designed an RC phase-shift oscillator that reached 22kHz at an 8V peak-to-peak amplitude. It was driven by a 20V power supply and consumed 72mW of RMS power. The design consisted of a single-stage common-emitter amplifier with a passive RC feedback network. The internal noise from these analog components would kick-start a signal into the amplifier, and the feedback network would selectively pass the target frequency.

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/oscillator3.png" width="100%">

A key problem that I encoutered was that the oscillation amplitude would consistently decay. After many attempts to debug the amplifier and feedback blocks, I found that the low-impedance biasing circuit components had consumed a lot of the feedback signal. The larger these imedances, the closer the biasing circuit would approach an ideal infinite impedance. I learned to start off the design process with the most straightforward components (such as high-impedance components used in biasing, which reduces power consumption) and make improvements through iterations.

Afterwards, I improved the design by replacing the RC feedback network with an LC tank. Not only is an LC tank more stable and power-efficient at higher frequencies, but it is also able to provide peak-to-peak voltage swings that theoretically exceed the limitations of the power supply.

With this change, my LC Colpitts oscillator reached 41MHz with a 7.3V peak-to-peak amplitude, and consumed 75mW from a 17V power supply.

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/oscillator4.png" width="100%">
</p>