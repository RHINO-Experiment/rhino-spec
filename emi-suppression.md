# EMI suppression
_Devices and strategies used to filter EMI, common mode and other interference_

Last updated: 2026-06-26

## Ferrites

We have some clip-on ferrite chokes that can be placed around coaxial cables to 
choke off high-frequency signals in the coaxial shield. The filtering 
performance depends on the ferrite mix used -- it seems that we want Mix 31, 
which is most effective at 1 - 300 MHz.

It would also be possible to build a balun/unun by wrapping coaxial cable around 
a suitable toroidal ferrite core, but we have not noticed much difference when 
trying this briefly.

There is a useful resource on [ferrite cores and beads here](https://palomar-engineers.com/ferrite-cores-for-rfi-emi-noise-suppression-mix-31-43-61-75-palomar-engineers).

## Cable routing

TBC
