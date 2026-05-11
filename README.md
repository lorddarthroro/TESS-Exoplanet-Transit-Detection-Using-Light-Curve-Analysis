# 🪐 TESS Exoplanet Transit Detection

This project explores time-series photometric data from the NASA Transiting Exoplanet Survey Satellite (TESS) mission to identify potential exoplanet transit signals using signal processing techniques.

The workflow focuses on analyzing stellar light curves to detect periodic dips in brightness that may indicate the presence of orbiting exoplanets.

---

## 🔬 Objective

To build a simple end-to-end pipeline for:
- Loading TESS light curve data
- Preprocessing and cleaning flux measurements
- Detecting transit-like dips in stellar brightness
- Analyzing periodicity using frequency-domain methods

---

## 🧰 Tools & Libraries

- Python
- lightkurve
- astropy
- numpy
- matplotlib

---

## 📊 Method Overview

1. Load TESS light curve data (FITS format)
2. Remove missing values and normalize flux
3. Apply flattening to remove long-term trends
4. Visualize light curve for potential transit events
5. Compute periodogram to search for periodic signals

---

## 📁 Data Source

NASA TESS mission light curve data accessed via the MAST archive.

---

## 🚧 Status

This project is currently in an exploratory stage and is being refined to improve signal detection methods and visualization quality.

---

## 📌 Notes

This project is intended for learning and exploratory data analysis in astronomical time-series datasets, with a focus on exoplanet transit detection techniques.
