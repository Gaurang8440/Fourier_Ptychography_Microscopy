# High-resolution and large field-of-view Fourier ptychographic microscopy and its applications in biomedicine
 **An Pan, Chao Zuo and Baoli Yao**

- High Resolution
- Wide FOV
- Quantitative Phase Recovery

**Problems**   

- Phase Loss
- Aberration induced Artifacts
- Narrow depth of field
- Trade off: Resolution and FOV

_FPM is an optimization problem
Euler's formula: Connection with structured illumination Microscopy_

**Limitations**

1. Objective lens acts as a _low pass filter_ with cut-off frequency determined by Numerical Aperture (NA); NA=n*sin(theta); acts as a resolution limit
2. [https://doi.org/10.1364/OE.23.003472](url)
3. A better resolution (larger NA) implies a smaller FOV and a shorter DOF that makes aberration correction harder.
4. Resolvable pixels, Space-Bandwidth Product (SBP)
5. Scanning FOV with a high NA objective may lead to scanning, refocusing and stitching artifacts.
6. Biological cells have poor absorption and contrast under conventional microscopes is low.
7. Spatial structures - uneven distribution of refractive index - phase information: camera sensors record intensity and information gets lost. Requires labeling with fluorochromes which in itself has limitations: long preparation time, phototoxicity, photobleaching, etc.
8. Zernike Phase Contrast Microscopy: Non linear relationship with its phase<img width="1100" height="577" alt="Image" src="https://github.com/user-attachments/assets/f03266b0-4475-41a5-a3b7-5285b00dd19a" /> [https://microbenotes.com/phase-contrast-microscopy/](url)


Coherent Diffraction Imaging: lens less imaging system (noise sensitive) ---> **Ptychography**: acquires multiple diffraction patterns through the scan of a localized illumination. Redundant information in the overlap regions of the illuminated spots is exploited for phase retrieval.

<img width="1815" height="770" alt="Image" src="https://github.com/user-attachments/assets/24bbc66c-4fb2-4def-9d11-128661c4302b" /> [https://www.physics.ucla.edu/research/imaging/research_CDI.html](url)

### Fourier ptychographic microscopy (FPM)

- The insight of FPM is that the objective can only collect light at certain angles, termed NA, however, parts of the scattering light can also be collected due to light matter interaction (Rayleigh or Mie scattering considering the feature size of sample).
-  Instead of conventionally starting with HR and stitching together for a larger FOV, FPM uses low NA objective to take advantage of its innate large FOV and stitches together low resolution (LR) images in Fourier space to recover HR.
- There is no need for mechanical scanning and successive refocusing
