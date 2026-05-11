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
## 📚 Background / Theory

Exoplanets are an area of astronomy that have always fascinated me. I have very fond memories from middle school of learning and reading about discovered exoplanets and what it might be like to live on the different cool and unique ones out there. I also remember trying to learn and understand how exoplanets were ever even found and studied - considering how you seeminly can't just point a telescope in a given direction in space to spot them. That childhood love is what inspired me to try delving a little deeper into my fascination and see what exoplanet identification and studying actually look like.

Exoplanets, as noted above, are not able to be easily identified and spotted by simply swiveling a sufficiently high power telescope around. They are far too dim and tiny, especially given their relative nearness to their host stars. Insted, the way exoplanets are typically 'discovered' is by identifying periodic trends in a star's **brightness over time**, also known as a **Light Curve**. A star's light curve is usually obtained by using Photometry to measure the brightness of a star, which is then done multiple times over a given period.   

<img width="686" height="386" alt="image" src="https://github.com/user-attachments/assets/21eaa843-a0cd-4f56-b2d3-7280a3ef70a6" />
(image from AstroPhil on Youtube)

Regular, periodic dips in these light curves can be indicative of an exoplanet, but as with most things in life, it is not quite that simple.


---

## 📊 Method Overview

1. Load TESS light curve data (FITS format)
2. Remove missing values and normalize flux
3. Apply flattening to remove long-term trends
4. Visualize light curve for potential transit events
5. Compute periodogram to search for periodic signals

---

## 🧰 Tools & Libraries

- Python
- lightkurve
- astropy
- numpy
- matplotlib

---

## 📁 Data Source

NASA TESS mission light curve data accessed via the MAST archive.

---

## 🚧 Status

This project is currently in an exploratory stage and is being refined to improve signal detection methods and visualization quality.

---

## 📌 Notes

This project is intended for learning and exploratory data analysis in astronomical time-series datasets, with a focus on exoplanet transit detection techniques.
