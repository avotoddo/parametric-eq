## Powering the Circuit
Guitar pedals are generally supplied with a single 9v DC input. We will be using a TON of op amps, so we need to at least split this supply. I also want the flexability to run this at higher internal voltage in the future. The Empress ParaEQ runs at 27v internally, meaning it has some DC/DC conversion going on. I will design this power section to take a variety of input voltages, so I can add this DC/DC conversion stage later without having to competely change my circuit.

___

### Getting a Reference Voltage

This is a pretty straight forward task! I can use a voltage divider and a decoupling capacitor to achieve this. The circuit is shown below:

<div style="text-align: center;">
    <img src = "/powering/figure/Supply Splitting.png" alt = "Supply Splitting Circuit Diagram" style="width:350px;"/>
</div>

This circuit will act as a highpass filter, so we want to make sure that the cutoff frequency is well below anything that might affect the sound of our circuit. The equation for cutoff frequency of this filter is $f_c = \frac{1}{2\pi \cdot (R_{10}||R_{12}) \cdot C_3}$. Since we want VREF to be half of VCC, $R_{10} = R_{12}$. Since we want our cutoff frequency to be very low, we can just pick very large values for $R_{10}$, $R_{12}$, and $C_3$. We also want to make sure $C_3$ has a suffiecient voltage rating for the potential ~15V it might see in the final version of this circuit.

___

### Charge Converter