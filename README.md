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

### ✨ Defining Light Curve

Exoplanets, as noted above, are not able to be easily identified and spotted by simply swiveling a sufficiently high power telescope around. They are far too dim and tiny, especially given their relative nearness to their host stars. Instead, the way exoplanets are typically 'discovered' is by identifying periodic trends in a star's **brightness over time**, also known as a **Light Curve**. A star's light curve is usually obtained by using Photometry to measure the brightness of a star, which is then done multiple times over a given period.   

<img width="686" height="386" alt="image" src="https://github.com/user-attachments/assets/21eaa843-a0cd-4f56-b2d3-7280a3ef70a6" />
(image source: [AstroPhil](https://www.youtube.com/@AstroPhil2000) on Youtube)

Regular, periodic dips in these light curves can be indicative of an exoplanet. This method of identifying exoplanets is known as **The Transit Method**.

<img width="672" height="332" alt="image" src="https://github.com/user-attachments/assets/6bc524d9-bea8-4956-b138-a7f56819fff4" />

Image source: [The Zooniversers Blog](https://blog.zooniverse.org/2015/07/08/introducing-the-planet-hunters-educators-guide/)

When a planet transits in front of it's host star (relative to Earth), a tiny percentage of the light from that star is blocked, which appears as a dip on the light curve. This event is called a **transit**. As one can imagine given the size difference between stars and planets, these differences in brightness are relatively small, but not imperceivable. A graph that shows several of these dips in regular intervals is what we would be looking to find.

<img width="576" height="432" alt="image" src="https://github.com/user-attachments/assets/0fdf8711-67f8-480b-a1d9-b6f94159cfba" />

Image source: https://avanderburg.github.io/tutorial/tutorial2.html

---

### 📈 Signal Processing

**Signal processing** broadly describes analyzing, modifying, and synthesizing signal data (such as sound, images, seismic signals, etc). Extracting meaningful data from TESS (NASA's Transiting Exoplanet Survey Satellite) in fundamentally a signal processing problem. Light curves are combinations of astrophysical signals along with various sources of noise that can originate from instrument issues, observation conditions, etc. This noise can make light curve data messy and hard to analyze, and thus cleaning raw photometric data is an important step in making otherwise faint periodic signals easier to detect.

The workflow includes:

**Preprocessing**: Removing missing values and normalizing flux measurements to establish a consistent baseline across observations.
**Detrending**: Applying a flattening function to remove long-term variability and instrumental drift.
**Filtering**: Reducing short-term noise and outliers that may interfere with signal detection.
**Feature detection**: Searching for potential transit-like dips in brightness and analyzing periodic structure using periodograms.

A **periodogram** is a tool that finds periodic patterns in data, and is especially used for time-series data. Our periodogram will plot period (in days) versus power (signal strength). What we would expect to see, ideally, in the case of an exoplanet being present is a strong isolated peak somewhere in the graph. 

<img width="330" height="204" alt="image" src="https://github.com/user-attachments/assets/69c5fbbd-de33-455c-82e7-7bfd3f16d62d" />

Image source: https://coolwiki.ipac.caltech.edu/index.php/What_is_a_periodogram%3F

---

## 📊 Method Overview

1. Load TESS light curve data (FITS format)
2. Remove missing values and normalize flux
3. Apply flattening to remove long-term trends
4. Visualize light curve for potential transit events
5. Compute periodogram to search for periodic signals
---
## 🪐🔭 Findings
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
---

## Works Cited
https://imagine.gsfc.nasa.gov/science/toolbox/timing1.html
https://medium.com/@msilvertant/hunting-exoplanets-using-the-transit-method-918e764e5576
https://www.youtube.com/watch?v=hEr1dp3wC20
https://coolwiki.ipac.caltech.edu/index.php/What_is_a_periodogram%3F
https://www.mathworks.com/discovery/digital-signal-processing.html?utm_source=chatgpt.com
