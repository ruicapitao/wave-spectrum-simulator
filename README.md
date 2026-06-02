# Wave Spectrum Simulation and Analysis

Interactive web-based wave spectrum simulator for offshore engineering and structural load analysis. Explore how spectral shape changes with sea state parameters across multiple empirical wave spectrum models.

**[Launch the simulator →](spectrum-simulator.html)**

## Features

- **5 spectrum models**: JONSWAP, PM Generalized, PM ITTC, Ochi-Hubble (bimodal), TMA (shallow water), plus **User-selected spectrum** (load your own f, S(f) pairs)
- **Interactive sliders** for wave height, peak/zero-crossing period, peakedness γ, and water depth — all update in real time with bidirectional numeric inputs; common parameters (Hs, Tp, γ) carry over when switching models
- **User-selected spectrum**: a dropdown model option — load your own S(f) data via text input (f, S pairs), file upload (.csv/.txt) via styled button, or example button; includes **agreement analysis** (Pearson r, RMSE, KS statistic vs all 5 models) and overlay comparison (pink trace) when data is loaded
- **Multiple spectrum overlay**: check any combination of models (distinct colors/dashes) for side-by-side comparison; User-selected overlay appears when data is available
- **RAO / Response module**: define a Response Amplitude Operator (single-DOF oscillator or custom pairs) to compute the response spectrum S_R(f) = S(f)·|H(f)|² as pink dashed overlay
- **Time-domain realization**: generate wave elevation time series via random-phase summation (up to 3600 s), with configurable time step (0.01–1.0 s), CSV download with descriptive filename, and FFT spectrum overlay; status bar shows model config, points, timestep, and duration
- **FFT spectrum from time series**: compute one-sided power spectrum via direct DFT with configurable moving-average smoothing (1–21 bins), overlaid on the main spectrum plot
- **Wave power display**: deep-water energy flux P (kW/m) computed from ρg∫S(f)·c_g(f) df
- **Breaking limit warnings**: visual alerts for Hs/d > 0.5 (TMA) and steepness Hs/Lp > 0.1
- **Engineering report** with spectral moments, derived parameters, model-specific commentary, RAO response table, and custom-spectrum agreement ranking — exportable to clipboard or HTML
- **Save/load configuration** via localStorage (all slider values, model type, time-domain state)
- **CSV export** of current spectrum data, all visible overlay models, and FFT-derived spectrum in one file, with descriptive filenames (e.g. `jonswap_γ3.3_Hs2.5_Tp10.0_spectrum.csv`)
- **Download plots as PNG** with context-aware filenames
- **Touch-friendly** slider thumbs on mobile

## Supported Spectra

| Model | Parameters | Description |
|-------|-----------|-------------|
| **JONSWAP** | Hₛ, Tₚ, γ (1–10) | Deep-water developing sea; γ controls peak enhancement |
| **PM Generalized** | Hₛ, Tₚ | Two-parameter Pierson–Moskowitz (γ=1) |
| **PM ITTC** | Hₛ, T_z | ITTC formulation using zero-crossing period |
| **Ochi-Hubble** | Hₛ, Tₚ, γ (swell + sea) | Bimodal; combined swell and wind-sea components |
| **TMA** | Hₛ, Tₚ, γ, depth | Shallow-water JONSWAP with dispersion-relation depth factor |
| **User-selected spectrum** | f, S(f) pairs | Custom spectrum loaded from text pairs, file upload, or example |

## Usage

Open `spectrum-simulator.html` in any modern browser. No build step or server required. All computation runs client-side in JavaScript.

The default view opens with JONSWAP (γ=3.3). Select a different model from the **Spectrum Model** dropdown to switch parameter sets — common parameters (Hs, Tp, γ) are preserved across compatible models.

### Interpreting the plots

- **Main spectrum plot**: Spectral density S(f) vs frequency. The peak is marked with a star. Filled area shows total energy. Additional overlays appear for Ochi-Hubble (swell/sea components), TMA (deep-water equivalent), RAO response, checked comparison models, and FFT-derived spectrum.
- **Params strip**: Real-time computed parameters — fp, peak S, ε, Te, Hs check, Tz, wave power. A second strip appears for FFT-derived parameters when enabled.
- **Generate Report**: Produces a structured document with input parameters, spectral moments, RAO response, and custom-spectrum agreement ranking.

## Dependencies

- [Plotly.js](https://plotly.com/javascript/) (loaded via CDN) — all chart rendering
- No other libraries or build tools required

## License

MIT — see [LICENSE](LICENSE).
