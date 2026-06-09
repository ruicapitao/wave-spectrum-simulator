# Wave Spectrum Simulator — Agent Guide

## Project structure

- **Single file**: `spectrum-simulator.html` (~3165 lines) — inline HTML, CSS, and JS. No other source files.
- No build tools, no package.json, no bundler, no transpiler.

## Development workflow

- **No build step.** Just edit `spectrum-simulator.html` and open in a browser to test.
- The only dependency is `Plotly.js` loaded via CDN (`https://cdn.plot.ly/plotly-2.35.0.min.js`). Do not add npm or bundler unless explicitly asked.
- No linting, type checking, or formatting tools are configured.

## Architecture

- All state lives in DOM elements (slider values) and a few module-level JS variables (`currentType`, `customSpectrum`, `fftSpectrum`, `lastTimeSeries`, `_commonHs`, `_commonTp`, `_commonGamma`).
- Spectrum computation runs on a fine grid (`N_FINE=4000`), downsampled to `N_PLOT=800` for display.
- The main update loop is `updateAll()` — called by every slider `input` event. It recomputes the spectrum, re-plots with Plotly, and updates the parameter strip.
- `onTypeChange()` switches model groups and carries over common parameters (Hs, Tp, γ) between compatible models.
- Model comparison overlays temporarily swap `spectrumType` to compute each model, then restore the original.

## Key naming conventions

- Slider IDs follow the pattern: `<model-prefix><Param>Slider` (e.g., `hm0Slider`, `gHm0Slider`, `iHsSlider`, `osHm0Slider`, `owHm0Slider`, `tHm0Slider`, `tdDurSlider`).
- Value display elements: `<param>Val` (e.g., `hm0Val`, `gHm0Val`).
- Control group divs: `grp_<type>` (e.g., `grp_jonswap`, `grp_tma`).
- Model type strings: `jonswap`, `pm-generalized`, `pm-ittc`, `ochi-hubble`, `tma`, `custom`.

## Spectrum model functions

| Model | Function | Slider group |
|-------|----------|-------------|
| JONSWAP | `computeJonswap(Hm0, Tp, gamma)` | `grp_jonswap` |
| PM Generalized | `computePMGeneralized(Hm0, Tp)` | `grp_pm-generalized` |
| PM ITTC | `computePM_ITTC(Hs, Tz)` | `grp_pm-ittc` |
| Ochi-Hubble | `computeOchiHubble(hm0S, tpS, lamS, hm0W, tpW, lamW)` | `grp_ochi-hubble` |
| TMA | `computeTMA(Hm0, Tp, gamma, depth)` | `grp_tma` |
| User-selected | (loaded externally, stored in `customSpectrum`) | `grp_custom` |

## Features to be aware of

- **Common parameter carry-over**: `_commonHs`, `_commonTp`, `_commonGamma` track slider values across model switches.
- **Time-domain realization**: `generateTimeSeries()` → `computeTimeSeries()` (random-phase summation, 500 components). Stored in `lastTimeSeries`.
- **FFT from time series**: `computeFFTSpectrum()` (direct DFT, O(N²)). Smoothed via `smoothSpectrum()`. Stored in `fftSpectrum`.
- **Config persistence**: `saveConfig()` / `loadConfig()` use `localStorage` key `"spectrumSimConfig"`.
- **Custom spectrum**: parsed from text input via `parseCustomInput()`, supports `.csv`/`.txt` upload. Agreement analysis (`computeAgreement()`) compares against all 5 models.
- **CSV export**: `downloadCSV()` includes the active spectrum + checked overlay models (interpolated to a common frequency grid).
- **Report**: `generateReport()` builds HTML with input params, spectral moments, engineering commentary, and custom-spectrum agreement table.

## What NOT to do

- Do not add npm dependencies or a build system without being asked.
- Do not add test infrastructure — there are no tests.
- Do not extract CSS or JS into separate files unless explicitly requested.
- Do not change slider ID patterns or model type strings — they are coupled in `onTypeChange()`, `updateAll()`, config save/load, CSV export, and report generation.
