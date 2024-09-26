## Single Band Active EQ

Huge win! I found a great resource on YouTube while learning about op-amp Gyrators. This guy made a [video](https://www.youtube.com/watch?v=z35qaXGchjE&ab_channel=ElectronicswithProfessorFiore) about what I am trying to do yesterday! This is all HEAVILY based on his lesson, so thanks a ton and check out his [channel](https://www.youtube.com/@ElectronicswithProfessorFiore)

This single band parametric EQ circuit is based on a 4 op-amp state variable band pass filter. He also made a [video](https://www.youtube.com/watch?v=esKrrjFJyuk&ab_channel=ElectronicswithProfessorFiore) about this topic, which details how to calculate component values.

Each state variable band pass filter will require 5 op amps, 2 dual-gang potentiometers, and one single gang poteniometer. I will likely need a dual op-amp to buffer the input and the output as well.

___

### 4 Op-Amp State Variable BP Filter

Let's start with a 4 op-amp state variable band pass filter. The schematic is shown below. Choosing R1 = R6 will set unity gain, while the value of R6 will determine the quality factor of the filter. The rest of the resistors will have the same value as each other. Our two capacitors will have the same value as well.

<div style="text-align: center;">
    <img src = "/single band active eq/figure/State Variable Schematic.jpg" alt = "State variable Band Pass Schematic" style="width:500px;"/>
</div>

To solve for capacitor and resistor values, we need to know the cutoff frequency ($F_0$) and the quality factor ($Q$) of our desired filter. This is easy to do by first solving for $R_1$ and $R_6$, which are equal to $Q$.

$$R_1=R_6=Q=\frac{F_0}{BW}$$

If we want a filter with cutoff frequenct 1 kHz and bandwidth 200 Hz, the quality factor can be solved using the equation above. We can then put resistors of that value in the circuit! 

$$R_1=R_6=Q=\frac{1 kHz}{200 Hz} = 5

To change the quality factor of the filter while maintaining unity gain, we just need to adjust these two resistors.

Next, let's set our filters cutoff frequency $F_0$ by choosing capacitors and resistors and the following equation:


$$F_0 = \frac{1}{2\pi RC}$$

Assume that $R=1\ \Omega$ and solve for $C$. This yields:

$$C=\frac{1}{2\pi F_0}=\frac{1}{2\pi *1\ kHz} = 1.6 \ \mu F$$

This circuit would work just fine with $R1$ and $R6$ = $5 \ \Omega$, all other all other $R=1\ \Omega$, and $C= 1.6 \ \mu F$. Currents in this circuit would likely be quite high, which isn't ideal. We can scale the impedance of the circuit by choosing a higher $R$ value and calculating the other values based on $F_0 = \frac{1}{2\pi RC}$

If we make $R=10 \ k\Omega$, then we need to scale $C$ by a factor of $10^{-5}$ so our cutoff frequency stays the same. We can scale $R1$ and $R6$ the same way as $R$ and make them $50\ k\Omega$.

___

### Making it Adjustable

Our quality factor and cutoff frequencies are each dependant on two resistors. We can replace each pair of resistor with a dual potentiometer and a resistor so we can change the cutoff frequency on the fly.

In the below schematic, you can see I have added two dual potentiometers, RV1 and RV2, so we can adjust our filter.

Now all we have to do is make it cut or boost!

<div style="text-align: center;">
    <img src = "/single band active eq/figure/AdjustableSVF.jpg" alt = "State variable Band Pass Schematic" style="width:500px;"/>
</div>

___

### Adjusting the Gain