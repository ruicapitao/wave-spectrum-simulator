# Wave Spectrum Simulator

Interactive web-based wave spectrum simulator for offshore engineering and structural load analysis. Explore how spectral shape changes with sea state parameters across multiple empirical wave spectrum models.

**[Launch the simulator →](spectrum-simulator.html)**

## Features

- **7 spectrum models**: JONSWAP, PM Generalized, PM ITTC, Ochi-Hubble (bimodal), TMA (shallow water), White Noise, Regular Wave
- **Interactive sliders** for wave height, peak/zero-crossing period, peakedness γ, and water depth — all update in real time with bidirectional numeric inputs
- **Custom spectrum input**: load your own S(f) data via text input, file upload (.csv/.txt), or example button — overlays red dashed line on all plots
- **Agreement analysis**: real-time Pearson r, RMSE, and KS statistics vs custom spectrum; full 7-model ranking table in report
- **Multiple spectrum overlay**: check any combination of the 7 models (distinct colors/dashes) for side-by-side comparison
- **RAO / Response module**: define a Response Amplitude Operator (single-DOF oscillator or custom pairs) to compute the response spectrum S_R(f) = S(f)·|H(f)|² as pink dashed overlay
- **Time-domain realization**: generate wave elevation time series via random-phase summation (up to 3600 s), with CSV upload, download, and FFT spectrum overlay
- **FFT spectrum from time series**: compute one-sided power spectrum via direct DFT with configurable moving-average smoothing (1–21 bins), overlaid on the main spectrum plot
- **Sensitivity analysis** with 3 live parameter sweeps per model showing how peak spectral density responds
- **Wave power display**: deep-water energy flux P (kW/m) computed from ρg∫S(f)·c_g(f) df
- **Breaking limit warnings**: visual alerts for Hs/d > 0.5 (TMA) and steepness Hs/Lp > 0.1
- **Engineering report** with spectral moments, derived parameters, model-specific commentary, RAO response table, and custom-spectrum agreement ranking — exportable to clipboard or HTML
- **Save/load configuration** via localStorage (all slider values, model type, time-domain state)
- **CSV export** of current spectrum data and time-series data
- **Touch-friendly** slider thumbs on mobile

## Supported Spectra

| Model | Parameters | Description |
|-------|-----------|-------------|
| **JONSWAP** | Hₛ, Tₚ, γ (1–10) | Deep-water developing sea; γ controls peak enhancement |
| **PM Generalized** | Hₛ, Tₚ | Two-parameter Pierson–Moskowitz (γ=1) |
| **PM ITTC** | Hₛ, T_z | ITTC formulation using zero-crossing period |
| **Ochi-Hubble** | Hₛ, Tₚ, γ (swell + sea) | Bimodal; combined swell and wind-sea components |
| **TMA** | Hₛ, Tₚ, γ, depth | Shallow-water JONSWAP with dispersion-relation depth factor |
| **White Noise** | Hₛ, f_min, f_max | Flat constant spectral density over a frequency band |
| **Regular Wave** | H, T | Monochromatic narrow Gaussian spike |

## Usage

Open `spectrum-simulator.html` in any modern browser. No build step or server required. All computation runs client-side in JavaScript.

The default view opens with JONSWAP (γ=3.3). Select a different model from the **Spectrum Model** dropdown to switch parameter sets.

### Interpreting the plots

- **Main spectrum plot**: Spectral density S(f) vs frequency. The peak is marked with a star. Filled area shows total energy. Additional overlays appear for Ochi-Hubble (swell/sea components), TMA (deep-water equivalent), custom spectrum, RAO response, comparison models, and FFT-derived spectrum.
- **Sensitivity panels** (below): Each sweeps one parameter across its range and plots the resulting peak spectral density. A red dotted line marks the current slider value.
- **Params strip**: Real-time computed parameters — fp, peak S, ε, Te, Hs check, Tz, wave power. A second strip appears for FFT-derived parameters when enabled.
- **Generate Engineering Report**: Produces a structured document with input parameters, spectral moments, RAO response, and custom-spectrum agreement ranking.

## Dependencies

- [Plotly.js](https://plotly.com/javascript/) (loaded via CDN) — all chart rendering
- No other libraries or build tools required

## License

MIT — see [LICENSE](LICENSE).
