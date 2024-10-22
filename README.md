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
<div style="text-align: center;">
    <img src = "/figure/Block Diagram.png" alt = "High Level Block Diagram" style="width:400px;"/>
</div>
