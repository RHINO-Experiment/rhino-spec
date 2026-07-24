# Temperature dependence

_2026-07-24_

## Thermal calibration load temperature dependence

For part of our calibration scheme, we are using the fact that the noise power of a thermal load scales linearly 
with physical temperature as $$P_{\rm load} = k_B T \Delta \nu$$. This allows us to link a measured noise power 
to a physical temperature. If the physical temperature is too low, however, the noise power could be below the 
radiometer noise of the receiver, and so the observed power, $$P_{\rm obs} = P_{\rm load} + P_{\rm noise}$$ 
(excluding reflection and gain terms), would be dominated by $$P_{\rm noise}$$ instead. This means that the 
observed power would not scale linearly with physical temperature, and so this calibration assumption would be 
broken.

In the case that $$P_{\rm noise} \gg P_{\rm load}$$ (and is approximately constant), but we erroneously assume 
that $$P_{\rm obs} \approx P_{\rm load} \propto T$$, at higher temperatures we would incorrectly infer a smaller 
gain factor and vice versa.

It is useful to test that the thermal calibration source power scales as expected with temperature. The 
following is a suggested test protocol to measure this experimentally:

1. Put the noise diode noise source in a temperature-stabilised enclosure (suggestion: a cooler filled with ice
   water, with noise diode in a waterproof bag)
2. Attach attenuators to the front of the noise source to improve matching (this should also be
   temperature-stabilised as attenuators add noise in a temperature-dependent way too) 
3. Set up the test thermal load with a thermometer/thermistor monitoring and place in an insulated box with a
   power resistor attached to a lab power supply or other variable voltage source.
4. Attach both sources to an SPDT switch and an SDR with constant gain setting, and switch between them rapidly
   (less than a few seconds switching cadence). Ideally this would be done inside a shielded box/room.
5. Assume that the noise source has constant output power and constant temperature. Drive the thermal load
   temperature up and then let it cool down while switching between the two sources. Measure the power ratio and
   plot against temperature.

If the thermal loads are behaving acceptably, there should be a good direct linear dependence on physical 
temperature. Deviations from the ideal may occur due to the receiver noise floor (measurable as a constant offset), 
variability in the noise source output, lags/differences between the measured and true physical temperature of 
the load, and neglected additive effects due to cable losses etc.
