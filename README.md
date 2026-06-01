# Empirical Spectrum Simulator

Interactive web-based wave spectrum simulator for offshore engineering and structural load analysis. Explore how spectral shape changes with sea state parameters across multiple empirical wave spectrum models.

**[Launch the simulator →](jonswap-spectrum-simulator.html)**

## Features

- **7 spectrum models**: JONSWAP, PM Generalized, PM ITTC, Ochi-Hubble (bimodal), TMA (shallow water), White Noise, Regular Wave
- **Interactive sliders** for wave height, peak/zero-crossing period, peakedness γ, and water depth — all update in real time
- **Sensitivity analysis** with 3 live parameter sweeps per model showing how peak spectral density responds
- **Engineering report** with spectral moments, derived parameters, and physics-based interpretation for structural loads
- **Comparison overlays**: Ochi-Hubble shows individual swell/wind-sea components; TMA shows deep-water equivalent
- **Reference γ ticks** at 1 (PM), 3.3 (JONSWAP), 7, and 10 for the JONSWAP peakedness slider

## Supported Spectra

| Model | Parameters | Description |
|-------|-----------|-------------|
| **JONSWAP** | Hₛ, Tₚ, γ (1–10) | Deep-water developing sea; γ controls peak enhancement |
| **PM Generalized** | Hₛ, Tₚ | Two-parameter Pierson–Moskowitz (γ=1) |
| **PM ITTC** | Hₛ, T_z | ITTC formulation using zero-crossing period |
| **Ochi-Hubble** | Hₛ, Tₚ, γ (swell + sea) | Bimodal; combined swell and wind-sea components |
| **TMA** | Hₛ, Tₚ, γ, depth | Shallow-water JONSWAP with dispersion-relation depth factor |
| **White Noise** | Hₛ | Flat constant spectral density |
| **Regular Wave** | H, T | Monochromatic narrow Gaussian spike |

## Usage

Open `jonswap-spectrum-simulator.html` in any modern browser. No build step or server required. All computation runs client-side in JavaScript.

The default view opens with JONSWAP (γ=3.3). Select a different model from the **Spectrum Model** dropdown to switch parameter sets.

### Interpreting the plots

- **Main spectrum plot**: Spectral density S(f) vs frequency. The peak is marked with a star. Filled area shows total energy.
- **Sensitivity panels** (below): Each sweeps one parameter across its range and plots the resulting peak spectral density. Use these to assess which parameter most strongly affects structural response.
- **Generate Engineering Report**: Produces a structured document with input parameters, spectral moments, and model-specific engineering commentary.

## Dependencies

- [Plotly.js](https://plotly.com/javascript/) (loaded via CDN) — all chart rendering
- No other libraries or build tools required

## License

MIT — see [LICENSE](LICENSE).
