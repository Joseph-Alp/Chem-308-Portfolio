# Fourier Transformation

A Fourier series represents any periodic function as a sum of sine and cosine functions with appropriate coefficients. 
Since the sinusoids each have a representative frequency a periodic function in time can be analyzed in terms of its frequency. 
We have already discussed changing basis sets in previous sections; however, we have not yet discussed how to transform between position and 
momentum. This is possible through what is commonly referred to as the *Fourier transformation*.

We can represent a state with either \bgroup\color{black}$\psi(x)$\egroup or with \bgroup\color{black}$\phi(p)$\egroup where 
Φ = momentum-space wavefunction, and Ψ = position-space wavefunction. 
With these variables, we are able to Fourier transform from one to the other using the following symmetric Fourier transform:

![Fourier](/fourier.png) 

Note that this is only in 1-dimension. 

Q: What can we expect to see when performing the Fourier transform between position and momentum?
A: We can observe the following graph generated in MatLab using this code.

![Four1](/four2.gif) 
![Four2](/four3.gif)

In each of the graphs represented, we have the position and momentum basis. The plane in the middle is at zero position (x = 0), and
zero momentum (k = 0). We are able to observe that at a higher momemntum, there is a shortening in the wavelength, 
an increase in steepness, and an increase in energy. As time progresses, we see the evolution of both basis sets.



