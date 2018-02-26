{% include mathjax.html %} 


# Viewing Quantum Functions Through Linear Algebra

A large portion of this course uses vectors to describe the quantum states that exist within a system. 

In quantum chemistry, it was established that a wavefunction is a complete discription of a particle's properties. This may include, but
is not limited to, the momentum, position, and kinetic energy of a particle within a system. Another vital component discussed was the 
operator, which describes the observable property of a particle (i.e. momentum, position, angular momemtun, spin, etc.). For every 
observable exists an operator which extracts the needed information from the particle's wavefunction. 

These principles can be applied to the Schrodinger equation: Hψ(x)=Eψ(x) where the possible measurement results in a set of eigenvalues.
There, the HH is the Hamiltonian operator.
For every eigenvalue obtained, there must also exist a definitively defined state. 

The equation that describes quantum mechanics of particles in well defined energy states can be determined by the time independent 
Schrödinger Equation, Ψ(x)Ψ(x).

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
 

# Observable Operators 

Observables take real values only. Therefore we must require that the operators that represent observables have only real eigenvalues, due to the fact that we want to identify the eigenvalues with the possible results of measurements. This can only be guaranteed if we only use Hermitean operators to represent observables. A Hermitian operator has real eigenvalues, and eigenvectors which form an orthonormalizable basis. This is guarantees that predicted measurement results will be real values. As a result, we must adhere to the main principles of Hermetian operators:
1. Hermitean operators have real eigenvalues
1. The eigenfunctions of a Hermitean operator that belong to different eigenvalues are orthogonal
1. If a Hermitean operator is acting on a vector space V, there exists an orthogonal basis
of V made of eigenvectors

# The Particle In The Box

The Particle in a Box (PIB) describes some particle of mass, m that is confined between two walls at x = 0 and x = L: 
the potential energy is zero inside the box but rises abruptly to infinity at the "walls" or boundaries. This ensures that the 
observed particle *must* exist somewhere within the set boundaries.
This model is an idealization of the potential energy of a gas-phase molecule that is free to move in a one-dimensional container.
*We see this model probed and explored from week 1 - week 4 of the MatLab chapters.

For our purposes, we focused a single particle in a one dimentional box of width a= 1 nm. We then set the potential energy inside the box to 0. At the boundary for our box, we set the potential energy to a value larger than the particle’s total energy. The potential energy is  also given by a matrix in the position basis. Using what we know about our linear algebraic assumptions, the potential matrix contains the values of the potential energy for reach position (x) along its diagonal. We are this able to set the number of position points by discretizing our space. After determining these variables, we then construct the kinetic energy matrix, which takes the form of the wave function's second derivative (found through both the right and left hand derivatives). After perfomring these calculations in MatLab, we are able to solve the TDSE to yield the energy eigenvectors:


![https://github.com/Joseph-Alp/Chem-308-Portfolio/blob/master/eigenvalues.png]


# Observable States Of Particle

The operator used for a PIB system determines the physical state of the particle. For instance, operating with the kinetic energy 
operator will generate information of the particle's KE at different states of energy. Furthermore, the average kinertic energy could be 
calculated by finding the expectation value, or simply the average, based on the possible states the particle may exist. 
