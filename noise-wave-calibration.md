Noise-wave calibration
======================
_The code and methods for doing noise-wave calibration_

Last updated: 2026-06-09

## Noise wave calibration

* **Observed:** 2026-06-09  (by Jordan Norris)
* **Reporter:** Rashi Srivastava
* **Receiver config:** RHINO receiver chain with switched calibration states.
* **Other config notes:** Uses laboratory VNA measurements from the `rhino-sparams` repository.

We currently use the noise-wave calibration method of **Kirkham et al.** to estimate the receiver noise contribution before recovering the antenna temperature.

The observing sequence is usually based on repeated switching between the antenna and calibration states. A typical cycle is:

1. `antenna/source`
2. `noise_diode`
3. `heated_load`
4. `load`

Additional diagnostic source states such as `open`, `short`, `long_open`, `long_short`, and `test_src` are included periodically. These states provide different reflection coefficients and are used to constrain or validate the noise-wave solution.

The current calibration uses laboratory VNA measurements to fix the reflection parameters for each source state and the receiver input. These S-parameter measurements are stored in the `rhino-sparams` repository and interpolated onto the SDR frequency grid before solving the calibration equations.

The extracted quantities are:

* `T_unc`: uncorrelated receiver noise term.
* `T_cos`: correlated cosine noise-wave term.
* `T_sin`: correlated sine noise-wave term.
* `T_NS`: effective noise-source temperature.

The fit is performed independently for each frequency channel. 

The main diagnostics are the recovered noise-wave spectra and calibration residuals for each state. Large residuals or sharp frequency structure in the recovered parameters usually indicate issues that need further checking, such as residual RFI, S11 interpolation problems, temperature mismatch, or poorly conditioned calibration states.

<img width="1289" height="590" alt="image" src="https://github.com/user-attachments/assets/0f54ac6e-c39e-443b-9eed-b72e03e4e66e" />

The figure above shows the recovered noise-wave parameters across the analysis band. The recovered T_NS is around 1000--1400 K and decreases slowly with frequency. The other terms, T_unc, T_cos, and T_sin, show smoother receiver-noise structure, but there is a clear sharp feature around 70.8 MHz. This feature is treated as a diagnostic warning and is checked against the residuals, RFI masks, S11 interpolation, and conditioning of the fit.

<img width="1289" height="490" alt="image" src="https://github.com/user-attachments/assets/794743c4-f736-41d9-897d-b2e47fb25b7b" />

The residual plot shows the difference between the model-predicted and measured calibrator temperatures for each fitted calibration state. Ideally, these residuals should be close to zero and should not show strong state-dependent spectral structure. In this run, most states remain within tens of kelvin, but open has noticeably larger scatter than the other states. A common feature is also visible around 70.8 MHz, matching the feature seen in the recovered noise-wave parameters.

<img width="1308" height="811" alt="image" src="https://github.com/user-attachments/assets/b7b2bb68-9169-42c5-bc00-5306fa1edf13" />

The test-source state is used as a held-out validation check. The top panel shows the mean calibrated test-source temperature across 75 blocks. It is recovered close to 298--300 K across most of the band. The bottom panel shows the per-block residuals relative to the mean test-source spectrum. These residuals are mostly centred around zero, with scatter at the tens-of-kelvin level and a visible narrow feature around 70.8 MHz.

The current diagnostics show that the calibration broadly recovers the expected source temperatures, but the feature around 70.8 MHz and the larger scatter in the open residuals require further investigation before using the full band for antenna-temperature recovery.
