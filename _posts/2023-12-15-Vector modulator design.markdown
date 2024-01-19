---
layout:     post
title:      "Vector Modulator Design"
description: "A project in designing a 16-QAM vector modulator at 5.4GHz."
date:       2023-12-15 09:00:00
author:     "Jin Wook Lee"
header-img: assets/img/MVM 1.png
---

# A project in designing a 16-QAM vector modulator at 5.4GHz.

<p align="center">
    <img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/akrf2.png" width="30%">
</p>

After struggling through the magical realm of microwave engineering, we completed a design project through Keysight's PathWave ADS program.

The 16-QAM vector modulator was designed to operate at 5.4GHz, supporting a minimum symbol rate of 810Msps, while meeting phase accuracy, amplitude accuracy, insertion loss, and power constraints. Specifications are shown below:

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/MVM 6.png" width="50%">
</p>

The functional blocks we used included an in-phase and quadrature divider (6-finger Lange coupler), a switching mechanism (SPDT with PIN diodes), phase shifter (using band-pass filters), attenautor (modified T-resistive attenuator), and power combiner (Wilkinson combiner). The best approach, as it turns out, was to design each block such that it uses as little distributive elements as possible to maintain performance across the desired device bandwidth.

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/MVM 2.png" width="50%">
</p>

For example, here is the detailed schematic view of the phase shifter:

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/MVM 3.png" width="50%">
</p>

And here is the attenuator:

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/MVM 4.png" width="50%">
</p>

Lastly, the beautiful output constellation!

<p align="center">
<img src="https://raw.githubusercontent.com/jwlee1221/jinscuit-v2/master/assets/img/MVM 5.png" width="50%">
</p>

Not only were we tasked to meet the target specifcations, but also we were tasked to use real components with performances outlined in real datasheets. It turns out, datasheets are suggestions. We can make do with whatever information the manufacturers give us. Using real components lead to its own complications. The biggest learnings were on the approach to ideal vs. specification-fitted designs...

The process of designing the vector modulator necessitated an approach to each functional block in isolation, considering the interaction between these blocks. Ideally, each block should alter the signal only through the desired parameter (e.g., the phase response of S21 for the phase modulator while maintaining the magnitude of S21). However, real devices do not perform ideally; we must consider changes in the phase and magnitude of the preceding blocks of the signal paths, in cascade, when designing subsequent blocks.

The seemingly obvious approach to designing each block would be to achieve behavior as close to this ideal as possible. For example, considering the magnitude response of the device: due to a maximum insertion loss target, the quadrature divider, switching mechanism, and phase modulator should be designed to introduce as little attenuation as possible. More importantly, the lower-attenuation path of the phase-invariant attenuator should ideally have 0dB insertion loss by using an ideal lossless transmission line. However, a transmission line is not simply used due to two reasons:

1. Maintaining symmetry between the lower-attenuation and greater-attenuation paths within the attenuator is desired, so all constellations maintain a similar phase-shift throughout all blocks and paths.
2. Maintaining lumped-element behavior of the attenuator is preferred, ensuring the performance of the attenuator across the target bandwidth is consistent with the phase response of the entire device.

Instead, the insertion loss target was initially approached by assessing the headroom on the attenuator block, considering additional loss from all other blocks. Recognizing that the phase attenuator had approximately 6dB of headroom (against the target specifications), the T-junction for each attenuation path was first designed to match this value. Fitted to a 6dB insertion loss, the smallest series resistor needed was 0.887 Ohms. Attempts to reduce insertion loss further would require even smaller resistor values, which were determined to be unrealistic in implementation.

After completing other designs, including the subsequent Wilkinson power combiner, attention was returned to the attenuator. The constraining factor in the T-junction structure was the sizes of the series resistors. By applying wye-delta transformations and adding a resistor in parallel with the T-junction structure using larger resistors, we addressed this constraint. Only at this stage (with the larger resistance headroom) was the focus returned to the ideal performances, and the resistance of the series resistor was further reduced to obtain the 0.5dB and 10.00dB IL, with the minimum series resistance at a relatively reasonable 0.5 Ohms.

In this manner, approaching a design to perform ideally from the start may lead to unreasonable designs. A better strategy may be to begin with the bare minimum target specifications in mind, complete other blocks, and finally return to the design in question for further iteration—slowly creeping up to the ideal performance values!
