# 🪐 TESS Exoplanet Transit Detection

This project explores time-series photometric data from the NASA Transiting Exoplanet Survey Satellite (TESS) mission to identify potential exoplanet transit signals using signal processing techniques.

The workflow focuses on analyzing stellar light curves to detect periodic dips in brightness that may indicate the presence of orbiting exoplanets.

This project is based on the NASA HEASARC tutorial [“How to Find an Exoplanet with TESS Data”](https://heasarc.gsfc.nasa.gov/docs/tess/HowToFindAnExoplanet-UserVersion.html) and uses Lightkurve to reproduce and extend the analysis of Pi Mensae c (Huang et al. 2018). Additional interpretation and signal-processing discussion were added independently.

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
Image source: [AstroPhil](https://www.youtube.com/@AstroPhil2000) on Youtube
<br><br>

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
2. Remove missing values and normalize flux (flux is the amount of light received per unit area per unit time from the star, essentially a measure for brightness)
3. Apply flattening to remove long-term trends
4. Visualize light curve for potential transit events
5. Compute periodogram to search for periodic signals
---
## 🪐🔭 Findings

### TIC 261136679
Note: this exploration in partiular closely follows https://heasarc.gsfc.nasa.gov/docs/tess/HowToFindAnExoplanet-UserVersion.html with a few alterations  
I analyzed TESS light curve data for TIC 261136679, which corresponds to star Pi Mensae (also known as HD 39091), known to host 3 exoplanets (Pi Mensae b, Pi Mensae c, and Pi Mensae d). This can provide an effective baseline as I know what to expect from this data, making the effective goal of this analysis specifically to see if we can find evidence of the existence of an exoplanet given what we already know. 

Loading the data in using the lightkurve library, we can 'flatten' the data to remove slow, smooth variations that are likely caused by factors such as instrumental drift, long-term stelllar variability, etc. Flattening removes long-term trends while preserving short-duration features like transits. Graphing after this flattening results in the following graph. 

<img width="777" height="376" alt="image" src="https://github.com/user-attachments/assets/9ca50c97-4beb-4961-a5cf-5ff5f2a6b46d" />

We can see from this graph that there is a period of time with considerable noise between ~1346 and ~1351. Thus, before further analysis, I filtered the data to remove observations in that time frame for cleaner processing.

<img width="781" height="394" alt="image" src="https://github.com/user-attachments/assets/8b5914f1-f1c8-4d76-b7cb-c7351bd5f887" />

After this, I applied from filtering to remove outliars, although the results output (below) didn't seem to alter the graph drastically if at all. This may be because the PDCSAP_FLUX data used is already processed to some degree, but it was worth keeping to be thorough. 

<img width="781" height="394" alt="image" src="https://github.com/user-attachments/assets/51bbbd13-7922-41bb-9c3f-3f27985e232e" />

Finally, I applied a fold, which is a way of 'rearranging time' so that a repeating signal lines up with itself. Instead of plotting flux versus absolute time, we plot it versus phase, where time is taken modulo a chosen period. This effectively “wraps” the light curve every X days so that all transits occurring at the same point in their orbit stack on top of each other.

This can be hard to understand, but astropy has a really helpful visualization (below). In the left image, the data is shown before folding. In the right, it is folded on a period of 2 days, so each point represents where it sits within that repeating cycle. The x-axis is now a phase-like scale from 0 to 2 days, meaning that events like transits line up at the same position in each cycle.

<p float="left">
  <img src="https://github.com/user-attachments/assets/fd056be2-389d-4bab-86e9-e1588e97a8e1" width="48%" />
  <img src="https://github.com/user-attachments/assets/99f6b55b-758c-4b08-bb9a-238ed634e201" width="48%" />
</p>

Once folded on the time interval of 6.27 days (the known orbital period of Pi Mensae c) , this is our new data graph:

<img width="781" height="394" alt="image" src="https://github.com/user-attachments/assets/52446f4b-de17-4de3-a564-d0ef7490b9b7" />

Here, we can see a pretty clear 'dip' in the normalized flux around the 0 phase. This indicates that transit events align consistently when folded at this period, supporting the presence of a periodic signal consistent with a planetary orbit. 

Taking this a step further, we can generate a periodogram to see if we can identify a high-peak around the expected time period (6.27 days). It is worth noting, "power" in this case is not a measure of brightness, but rather measures how strongly the light curve becomes periodic when folded at each trial period; higher values indicate a better repeating match.

<img width="751" height="379" alt="image" src="https://github.com/user-attachments/assets/fcaf1cbd-30ee-486e-a034-9d064bb009d0" />


As we can see, there is a clear peak at around the expected orbital period. However, there are several smaller spikes earlier that could be the result of some noise, or perhaps an artifact of how periodograms are generated. This is a worthy subject of further investigation. A cursory investigation and search shows this could be the result of harmonics. In this context, the periodic signals correspond to the fundamental orbital period of the system (6.27 days). This corresponds to a fundamental frequency of _f_ = 1/_P_, where _P_=6.27 days. Harmonics are integer multiples of this frequency (2_f_, 3_f_, etc), and can appear as additional spikes in a periodogram due to non-sinusoidal signal structure. Since the periodogram is in period space, these would show in fractional periods, like _P_/2 and _P_/3 (6.27/2 ≈ 3.14 and 6.27/3 ≈ 2.09) (https://en.wikipedia.org/wiki/Fourier_series).

This would be fun to revisit and understand better in the future, but for now I will leave it at that. 

### TIC 261136679
Next, I tried using a TIC corresponding with WASP-18, a star with a known 'hot jupiter'. I challenged myself to try to find the oribital period from the data instead of looking it up ahead of time, that way I could validate my results and process. Below are my results, slightly more succinct then the previous section as I've already detailed the general steps above.

After cleaning and normalizing:

<img width="756" height="376" alt="image" src="https://github.com/user-attachments/assets/b75e83ba-7a51-4122-8fde-ba5c57734645" />

Interestingly, the dipping flux pattern here seems pretty clear and frequent! I wonder if this has to do with the size of the planet. After I tried an initial fold with a period of 6.27 (the period in the previous example), I was able to identify several dips, leading me to beleive that the period was likely shorter.

<img width="756" height="376" alt="image" src="https://github.com/user-attachments/assets/b74f4dbf-3aad-4582-8452-0e0b0a02d9b0" />


Checking the max power from the periodogram generated, I got a value of ~ 1.882. However, it still showed two dips

<img width="764" height="376" alt="image" src="https://github.com/user-attachments/assets/f11526dd-b772-4a28-a740-b76c1feff7d3" />

Finally, after adjusting the period to be half of the 1.88 (perhaps a harmonic?), I arrived at a period of ~ 0.94, and once I adjusted the epoch time to fit it best, I was greeted with the following result

<img width="756" height="376" alt="image" src="https://github.com/user-attachments/assets/9b16ca59-940b-438a-87eb-dd48b1cd112b" />

Here, the fold seems to suggest that the period of the planet is around 0.94. And indeed, Wasp-18b has the (in my opinion, suprisingly) low orbital period of 0.941452379 days (https://en.wikipedia.org/wiki/WASP-18b). Success!


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

https://heasarc.gsfc.nasa.gov/docs/tess/HowToFindAnExoplanet-UserVersion.html

https://www.hughosborn.co.uk/2021/01/04/so-you-think-youve-found-an-exoplanet/

https://docs.astropy.org/en/stable/timeseries/index.html

https://en.wikipedia.org/wiki/Fourier_series
