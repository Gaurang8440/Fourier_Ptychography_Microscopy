# Theory and Algorithm
- LED array mounted under the sample, a light microscope with a low-NA objective lens, and a monochromatic imaging sensor.
- Successive illumination from multiple angles: relative displacement between spectrum of sample and aperture of objective lens
  <img width="789" height="720" alt="image" src="https://github.com/user-attachments/assets/e4b4a6c3-406a-4b7e-aba5-aeb8795753dd" />
https://biophot.caltech.edu/research/fourier-ptychography
- Low Resolution images from each angle
  
_Note : When the illumination angle is restricted or higher than the angle range of objective, a BF image or a dark eld (DF) scattering image is recorded_

**Optics Theory**

_Assumption: Incident light is an ideal plane wave and sample is relaively thin_

For each $LED_{m,n}$ (row m, column n): illumination wave vector $(k_{x,m,n},k_{y,m,n})$

Transmitted wave field from sample is $O(x,y).e^{(ik_{x,m,n} x,ik_{y,m,n} y)}$

$O(x,y)$ is sample's transmission function

$P(k_x,k_y)$ is Pupil Function (Coordinate transform of pupil function in spatial domain): Acts as a low pass filter

$$\tilde{O}(k_x,k_y) = F \lbrace O(x,y)\rbrace= \iint O(x,y).e^{-i(xk_{x} + yk_{y})} dxdy$$

Image sensor captures an LR intensity image $I_{m,n}$ given by

$$I_{m,n} = | F^{-1} \lbrace F \lbrace O(x,y).e^{(ik_{x,m,n} x,ik_{y,m,n} y)} \rbrace .P(k_x,k_y) \rbrace |^2$$

$$I_{m,n} = | F^{-1} \lbrace \tilde{O}(k_x - k_{x,m,n},k_y - k_{y,m,n}).P(k_x,k_y) \rbrace |^2$$

FPM attempts to eliminate or minimize the variations in amplitude between simulation patterns and captured images iteratively: Non-convex Optimization https://rumn.medium.com/convex-vs-non-convex-functions-why-it-matters-in-optimization-for-machine-learning-39cd9427dfcc

$$\min_{O(k_x,k_y)} \epsilon = \min_{O(k_x,k_y)} \sum_{m,n} \sum_{x,y} |\sqrt{I_{m,n}(x,y)} - | F^{-1} \lbrace \tilde{O}(k_x - k_{x,m,n},k_y - k_{y,m,n}).P(k_x,k_y) \rbrace ||^2$$

[Paper Exchange/Appendix - Ptychography.pdf ](https://github.com/BioPhotonicaLab-IITD/Fourier_ptychography/blob/ab9ef55759e1c3c872dba262cf95e549f1996407/Paper%20Exchange/Appendix%20-%20Ptychography.pdf)

[Paper Exchange/PtychographyTutorial_Revised_SanderKonijnenberg.pdf](https://github.com/BioPhotonicaLab-IITD/Fourier_ptychography/blob/ab9ef55759e1c3c872dba262cf95e549f1996407/Paper%20Exchange/PtychographyTutorial_Revised_SanderKonijnenberg.pdf)

**Algorithm**

1. An initial HR complex amplitude guess of the pupil function and sample spectrum, $P_o(k_x,k_y) and \tilde{O_o}(k_x,k_y)$ respectively. Initial guess of pupil function is a circular shape due to objective design and zero phase (nature of CTf). Up-sampled LR image is taken as first guess for sample spectrum

2. The exit wave at the fourier plane can be estimated by multiplication

$$\phi^e_{m,n}(k_x,k_y) = \tilde{O_o}(k_x -k_{x,m,n},k_y - k_{y,m,n}).P_o(k_x,k_y)$$

  and the simulated LR image on the image plane is inverse Fourier Transform of it: 

$$\phi^e_{m,n}(x,y) = F^{-1}\lbrace \phi^e_{m,n}(k_x,k_y) \rbrace$$

It would have some amplitude and phase information

3. The modulus of the simulated LR image is replaced by the square root of the actual measurement, and the phase remains unchanged.

$$\phi^u_{m,n}(x,y) = \sqrt{I^c_{m,n}(x,y)}\frac{\phi^e_{m,n}(x,y)}{|\phi^e_{m,n}(x,y)|}$$

4.The modified LR image is then used to update the corresponding spectrum region of sample estimate in the Fourier domain.

$$\tilde{O}(k_x,k_y) = F \lbrace \phi^u_{m,n}(x,y) \rbrace.P(k_x,k_y) + \phi^e_{m,n}(k_x,k_y)[1-P(k_x,k_y)]$$

Single iteration is completed when all the captured images are used to update corresponding parts of the sample spectrum in Fourier domain. $i$ iterations are reapeated until the solution converges in the limits of an error metric defined by

$$\epsilon_i = \frac {\sum_{x,y,m,n}(\sqrt{I^c_{m,n}(x,y)}-|\phi^e_{m,n}(x,y)|)^2}{\sum_{x,y,m,n}I^c_{m,n}(x,y)}$$
