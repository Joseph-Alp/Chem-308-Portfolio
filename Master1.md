{% include mathjax.html %} 


# Viewing Quantum Functions Through Linear Algebra

A large portion of this course uses vectors to describe the quantum states that exist within a system. 
In order to do continue with discussions about the TISE and TDSE, a background refresher in complex numbers may be necessary,
which can be found [here](/Complex_Numbers.md).

In quantum chemistry, it was established that a wavefunction is a complete discription of a particle's properties. This may include, but
is not limited to, the momentum, position, and kinetic energy of a particle within a system. Another vital component discussed was the 
operator, which describes the observable property of a particle (i.e. momentum, position, angular momemtun, spin, etc.). For every 
observable exists an operator which extracts the needed information from the particle's wavefunction. 

These principles can be applied to the Schrodinger equation: Hψ(x)=Eψ(x) where the possible measurement results in a set of eigenvalues.
There, the HH is the Hamiltonian operator.
For every eigenvalue obtained, there must also exist a definitively defined state. 

The equation that describes quantum mechanics of particles in well defined energy states can be determined by the time independent 
Schrödinger Equation, Ψ(x)Ψ(x). Four our purposes, this will consist primarily of function. When using functions to represent the wave function, the Hamiltonian can be expressed as: $$\hat{H} = -\frac{\hbar^2}{2m}\frac{\partial^2}{\partial x^2} + V(x)$$. Here, $$m$$ is the mass of the particle and $$V(x)$$ is the potential energy operator. Furthermore, the stationary state energies are equal to $$\psi_n=\sqrt{\frac{2}{l}}sin(\frac{n\pi x}{l})$$ where $$n$$ is the stationary state and $$l$$ is the length of the box for our model.

This concept is the foundation for all of our MatLab codes centering around the TISE from Week 1 - Week 4, and is commented in detail.


The time dependent Schrödinger describes all physically realizable states, 
and is defined by the equation: \begin{equation}\label{tdse} \mathcal{H}\Psi(x,t) = E\Psi(x,t) \end{equation} 
where $$\mathcal{H}$$ is the Hamiltonian operator formed 
by the sum of the potential and kinetic energy operators, and $$\Psi(x,t)$$ is a time- and space-dependent wavefunction.

In viewing this, we can understand quantum states and being made up of other, possible states. As a result, we can utilize MatLab
to show that the states of a quantum system can be representedvia vectors in a complex vector space whch was first demonstrated 
during [Week 1](/MLW1.md) of this course. This concept was taken a step further by looking at [three dimentional space](/MLW4.md) (x,y,z) as a basis set for vectors in a PIB.

Thus, several assumptions must be made inorder to interchange bases when taking the inner product:
* Wave functions and other quantum states can be represented as vectors in complex  space
* Quantum superpositions can be described as vector sums of their constituent states
* Measurements are associated with their linear operators (observables) on the space of quantum states
* We normalize our wave functions in order to ensure a 100% possibility of determining the properties of our particle 
