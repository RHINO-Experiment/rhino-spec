# System noise properties
_Estimates of the system temperature and observing time required for signal detection_

Last updated: 2026-06-21

## System temperature

TODO: Basic system temperature model, including LST-dependent sky contribution.

## Target sensitivity

We will assume the basic radiometer equation, $\sigma_T = T_{\rm sys} / \sqrt{\delta \nu\, t_{\rm obs}}$. 
If we assume 500 kHz channels and an average of 6 hours of observing per night, we 
can work out how long it would take to reach the 50 mK noise sensitivity level per 
channel, which should be sufficient for a reasonably significant detection of 
typical ~100 mK physical absorption features, and a strong detection/rejection of 
the ~500 mK EDGES feature. This ignores systematic and calibration effects, and so 
is highly idealised, but it should give us ballpark figures for how to observe.

The total observing time must be further moderated by efficiency factors, such as 
the fraction of time spend observing through the antenna vs other sources.

For any reasonable system temperature of order a few thousand Kelvin, only one night 
of observing is needed to reach this level, assuming an efficiency factor of unity. 
For more reasonable efficiency factors, this is still only a few nights.
