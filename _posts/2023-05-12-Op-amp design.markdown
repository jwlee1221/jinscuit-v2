---
layout:     post
title:      "Operational amplifier"
description: "A 2-stage operational amplifier design and layout simulation."
date:       2023-05-12 09:00:00
author:     "Jin Wook Lee"
header-img: assets/img/opamp1.png
---

# The operational amplifier

In this Integrated Circuit Design project, we were tasked with designing an operational amplifier for an RF mixer. This theoretical op-amp would then be used to amplify the local oscillator output.

I designed my op-amp using a two-stage structure: a telescopic differential first-stage, followed by a common-source second stage. The device also incorporates common-mode feedback in the form of passive resistors between the output and current source of the second stage. Finally, all DC biasing is implemented by using two ideal reference current sources, which are used for two separate current mirror branches to set desired DC voltages.

<p align="center">
    <img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/opamp3.png" width="60%">
</p>

The process involved a lot of trial-and-error, and it took a long time to develop some sense of intuition for the circuit behavior. However, it was really rewarding to see my final design reach the desired specifications: low-frequency voltage gain, frequency at unity voltage gain, phase margin, power consumption, and output peak-to-peak voltage swing. For example, I also tried to use two stages of differential amplifiers, followed by a third common-source stage, to achieve the desired gain with extremely low power consumption. (While all other specifications were met with a power consumption below 1mW, the phase margin was awful; using multiple stages meant that there were more poles, making the phase response drop well below -180° at even moderate frequencies. Perhaps I could have tuned the poles to align such that the phase response of each pole would overlap... but this idea was abandoned for simplicity.)