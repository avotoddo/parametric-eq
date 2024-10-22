## Single Band Active EQ

Huge win! I found a great resource on YouTube while learning about op-amp Gyrators. This guy made a [video](https://www.youtube.com/watch?v=z35qaXGchjE&ab_channel=ElectronicswithProfessorFiore) about what I am trying to do yesterday! This is all HEAVILY based on his lesson, so thanks a ton and check out his [channel](https://www.youtube.com/@ElectronicswithProfessorFiore)

This single band parametric EQ circuit is based on a 4 op-amp state variable band pass filter. He also made a [video](https://www.youtube.com/watch?v=esKrrjFJyuk&ab_channel=ElectronicswithProfessorFiore) about this topic, which details how to calculate component values.

Each state variable band pass filter will require 5 op amps, 2 dual potentiometers, and one single poteniometer. I will likely need a dual op-amp to buffer the input and the output as well.

___

### 4 Op-Amp State Variable BP Filter

Let's start with a 4 op-amp state variable band pass filter. The schematic is shown below. Choosing R1 = R6 will set unity gain, while the value of R6 will determine the quality factor of the filter. The rest of the resistors will have the same value as each other. Our two capacitors will have the same value as well.

<div style="text-align: center;">
    <img src = "/single band active eq/figure/State Variable Schematic.jpg" alt = "State variable Band Pass Schematic" style="width:500px;"/>
</div>

To solve for capacitor and resistor values, we need to know the cutoff frequency ($F_0$) and the quality factor ($Q$) of our desired filter. This is easy to do by first solving for $R_1$ and $R_6$, which are equal to $Q$.

$$R_1=R_6=Q=\frac{F_0}{BW}$$

If we want a filter with cutoff frequenct 1 kHz and bandwidth 200 Hz, the quality factor can be solved using the equation above. We can then put resistors of that value in the circuit! 

$$R_1=R_6=Q=\frac{1 kHz}{200 Hz} = 5$$

To change the quality factor of the filter while maintaining unity gain, we just need to adjust these two resistors.

Next, let's set our filters cutoff frequency $F_0$ by choosing capacitors and resistors and the following equation:


$$F_0 = \frac{1}{2\pi RC}$$

Assume that $R=1\ \Omega$ and solve for $C$. This yields:

$$C=\frac{1}{2\pi F_0}=\frac{1}{2\pi *1\ kHz} = 1.6 \ \mu F$$

This circuit would work just fine with $R1$ and $R6$ = $5 \ \Omega$, all other all other $R=1\ \Omega$, and $C= 1.6 \ \mu F$. Currents in this circuit would likely be quite high, which isn't ideal. We can scale the impedance of the circuit by choosing a higher $R$ value and calculating the other values based on $F_0 = \frac{1}{2\pi RC}$

If we make $R=10 \ k\Omega$, then we need to scale $C$ by a factor of $10^{-5}$, giving a $16\ pF$ capacitor, so our cutoff frequency stays the same . We can scale $R1$ and $R6$ the same way as $R$ and make them $50\ k\Omega$.

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

The circuit we have currently just acts as a band pass filter. What we want is a circuit that either cuts or boost a band, rather than just passing a band. In order to do this, we need to add another op amp stage and one more potentiometer.

<div style="text-align: center;">
    <img src = "/single band active eq/figure/CutBoostStage.png" alt = "State variable Band Pass Schematic" style="width:500px;"/>
</div> 

Our op amp will be configured as an inverting, summing amplifer, as shown above. The op amp inverting input sums the input signal with unity gain ($R11=R9$), and the output of our state variable filter with gain set by restistor RBCMAX.

Our potentiometer will allow us to choose if we are boosting or cutting the desired band. When the wiper arm is fully to the left, the state variable filter will see our input signal at it's input. This gets summed back in with out original signal, giving us a boost. If the wiper arm is fully to the right, the state variable filter will see the output of our summing amplifier. The result of this is adding an inverted copy of our filtered signal to the original signal. This means a band cut! We will use a 10k potentiometer since we are using mostly 10k resistors elsewhere in the circuit.

___

### Choosing Components

My plan is to build this single band parametric EQ on a breadboard so I can play around with it before adding more bands and designing PCBs. In order to do that though, I need to choose component values!

I am most interested in a mid frequency control because I feel like I understand the least about what mid frequencies sound like in a guitar signal. The Empress ParaEQ mid band ranges between 250 Hz and 5 kHz, with a max boost/cut of 15 dB.

The frequency control is fairly straight forward to calculate using the equation $F_0 = \frac{1}{2\pi RC}$ from above.

We can solve for the component values at the top of our desired frequency range, since this is when resistance will be the smallest.

$$R = 1 \Omega, F_0 = 5000\ Hz, C = \frac{1}{2\pi * 5000\ Hz} =31.8 \mu F$$

Let's scale our resistor to 10k like we did in the previous example. We will need to scale our capacitor inversely to keep our cutoff frequency the same.

$$\frac{C}{10000} = \frac{31.8 \mu F}{10000} = 3.18\ nF$$

We can use a standard 3300 pF capacitor, which will be super close enough for our circuit.

Next, we can solve for what we want the resistance value to be for the bottom end of our frequency range, using the capacitor we just solved for.

$$250\ Hz = \frac{1}{2\pi * R * 3300 pF}$$

$$R = \frac{1}{2\pi * 250 * 3300 pF} = 193k\Omega $$

To achieve this frequency range, we can use a 10k resistor and something like a 200k potentiometer. This would make our bottom frequency 230 Hz, which isn't necessarily a bad thing and makes my life a lot easier with sourcing parts!

We can get about 14 dB of gain or cut with a 5:1 gain ratio with our summing amplifier. This just means that RCBMAX needs to be 1/4 the value of R9 and R11. If I chose 10k resistors for those two, a 2.5K resistor would give me the desired level of boost or cut. Easy!

### Biasing

I will be using a single voltage supply for this circuit, so I will have to bias the op amps where needed. My reference voltage is half of my supply voltage. Luckily, for inverting op amps, this is as easy as pretending VREF is ground and connecting my VREF to the non-inverting side of the op amp.
