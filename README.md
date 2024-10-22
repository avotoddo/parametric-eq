# Parametric EQ
I want to build a parametric EQ guitar pedal. Seems like a solid way to familiarize myself with analog filtering, active EQ, and power circuitry!

---
### Why do I want to do this?
I have been playing a lot of guitar and have gotten a little annoyed by how expensive some of the pedals I want are. The guitar I play is also extremely bright, and I often wish that the pickups produce a little less high end. Yeah, I could just roll my tone knob back, but I want more control and consistency.


I was considering buying the [Empress ParaEQ MKII Deluxe](https://empresseffects.com/products/paraeq-mkii-deluxe), which is a three-band active EQ pedal with lots of fancy features. Each filter band lets you select the center frequency, the quality factor of the filter, and the gain. On top of this, it features global low and high pass filters with adjustable cutoff frequency, and Baxandall filters with adjustable gain.

<div style="text-align: center;">
    <img src = "/figure/ParaEQMKIIDeluxe-top-transparent.webp" alt = "empress ParaEQ MKII Deluxe" style="width:350px;"/>
</div>
This pedal also operates at 27V internally, but is supplied by a standard 9V power supply. This means more clean gain without clipping.

I think starting with normal 9V operation and implimenting just a single band active EQ circuit on a breadboard is a good way to start.

---
### Circuit Block Diagram

This circuit is a lot less intimidating when broken down into it's individual parts. A fairly high level block diagram is shown below.
<div style="text-align: center;">
    <img src = "/figure/Block Diagram.png" alt = "High Level Block Diagram" style="width:1000px;"/>
</div>

We will start by buffering our input signal so it will play well with other electronics. Next we will send the signal through three parametric equalizer bands. Each band then be summed together using an inverting summing amplifier. Next, our signal will be sent through a Baxandall filter which can cut or boost bass and treble frequencies. After that, it will be sent through passive high pass and low pass filters with adjustable cutoff frequency. Finally, there is a boost stage, which will allow us to set the overall output volume of the signal. We probably want to buffer the output as well.