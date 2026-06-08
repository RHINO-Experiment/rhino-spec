RFI flagging
============

Last updated: 2026-06-08

MomentRFI state-wise cleaning of calibration waterfalls
------------------------------------------------------
 * **Observed:** Spring 2026
 * **Reporter:** Rashi Srivastava
 * **Receiver config:** RHINO calibration observations with switched calibration states.
 * **Other config notes:** Cleaning applied state-by-state after removing switch-settling spectra.

MomentRFI is used to identify and remove time-frequency RFI contamination from the RHINO calibration waterfalls before solving for the receiver noise-wave parameters. The waterfall is first split by switch state, so that states such as `load`, `noise_diode`, `heated_load`, `open`, `short`, `long_open`, and `long_short` are cleaned independently.

This is necessary because each calibration state has a different absolute power level and spectral shape. Cleaning the full waterfall at once can confuse real state-dependent calibration structure with RFI-like deviations.

The current implementation applies a multi-pass smooth-surface fit to each state waterfall. Pixels that deviate significantly from the fitted smooth surface are flagged using iterative sigma clipping. The final mask also allows promotion of bad frequency channels and bad time rows if a large enough fraction of that channel or row is contaminated.

Typical settings used in the current run are:

 * Three MomentRFI passes.
 * Polynomial degrees 5 and 7.
 * Sigma thresholds of 3.5--4.0.
 * Channel promotion threshold: 12%.
 * Row promotion threshold: 35%.
 * Additional row/channel sigma threshold: 5.
 * Binary final masks.
 * Optional row/channel-only mode for conservative flagging.

The main outputs saved from this step are:

 * `waterfall_clean`: cleaned full waterfall.
 * `cleaned_by_state`: cleaned waterfall for each switch state.
 * `mask_by_state`: final binary mask for each state.
 * `pixel_mask_by_state`: pixel-level MomentRFI mask.
 * `fitted_surface_by_state`: smooth fitted surface used for outlier detection.
 * `bad_channels_by_state`: promoted bad frequency channels.
 * `bad_rows_by_state`: promoted bad time rows.

This step is mainly diagnostic and preventative. Residual RFI can bias the later noise-wave calibration, especially the recovered `T_NS`, `T_unc`, `T_cos`, and `T_sin` terms. It can also introduce artificial spectral structure that looks calibration-related but is actually contamination.

<img width="2210" height="911" alt="image" src="https://github.com/user-attachments/assets/3b12c394-16f5-42c0-88a4-c388bb6865b4" />

In this plot, the initial pixel mask flags only 0.20% of pixels, but the final mask flags 6.43% after row/channel promotion. This indicates that the dominant contamination is not just isolated pixels, but structured features such as persistent frequency-channel artefacts and a few bad time rows.

<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/b6b0e4cc-a3f8-4bb9-85ee-983bfecbcddb" />
<img width="1189" height="390" alt="image" src="https://github.com/user-attachments/assets/f656f677-cec6-404e-aab7-1fd1c2bc43d1" />

The channel-score plot shows several very strong narrow-band outliers, especially near the 68--72 MHz region. These are treated as persistent channel artefacts and promoted to full-channel flags. The row-score plot shows a strong time-localised feature around row index ~70--80, which is promoted to a bad time row in the final mask.

The cleaning parameters are currently tuned empirically for the RHINO calibration waterfalls. They should be rechecked for each observing run, especially the row/channel promotion thresholds, since over-aggressive flagging could remove valid calibration structure.
