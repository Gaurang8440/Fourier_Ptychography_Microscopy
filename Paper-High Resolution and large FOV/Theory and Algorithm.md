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

