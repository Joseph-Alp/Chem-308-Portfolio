{% include mathjax.html %}

# Observable Operators 

Observables take real values only. Therefore we must require that the operators that represent observables have only real eigenvalues, due to the fact that we want to identify the eigenvalues with the possible results of measurements. This can only be guaranteed if we only use Hermitean operators to represent observables. A Hermitian operator has real eigenvalues, and eigenvectors which form an orthonormalizable basis. This guarantees that predicted measurement results will be real values. Furthermore, wave functions expressed as a vector can be broken down into a linear combination of the basis vectors covering all space. As a result, we must adhere to the main principles of Hermetian operators:
1. Hermitean operators have real eigenvalues
1. The eigenfunctions of a Hermitean operator that belong to different eigenvalues are orthogonal
1. If a Hermitean operator is acting on a vector space V, there exists an orthogonal basis
of V made of eigenvectors


# Observable States Of Particle

The operator used for a PIB system determines the physical state of the particle. For instance, operating with the kinetic energy 
operator will generate information of the particle's KE at different states of energy. Furthermore, the average kinertic energy could be 
calculated by finding the expectation value, or simply the average, based on the possible states the particle may exist. 

# Changing Basis Sets 

Knowing how to convert a vector to a different basis has many practical applications throughout this course.
Changing Bases

A basis of a vector space V is a set of vectors in V that is linearly independent and spans V. Furthermore, an ordered basis is a list, rather than a set, meaning that the order of the vectors in an ordered basis matters. However, there is often another coordinate system that simplifies the problem. This is particularly noted when solvind TDSE's for non-stationary quantum states.

We have already established that vectors can notated by different bases such as kinetic energy, position, and momentum. For example, if a wave function $$\psi(x)$$ is operated on by a Hamiltonian, $$\hat{H}$$, in the position basis- we know that this is its natural basis. How is this the case? We know this because $$\psi(x)$$ is written in terms of a position basis, as is hamiltonian. In order to be operated on, both must be in the same bases; this ensures us that the eigenvalue output using a Hamiltonian operator in any basis will always be the same. However, we know that energy is simply a scalar. This is useful to bear in mind, as we are then able to change between bases by multiplying the eigenvector matrix or its inverse to convert them between position and energy. To do this, we can use the eigenvectors and to go from the position basis to the energy basis you use the inverse of the eigenvectors using the following MatLab code that is found throughout all of our problems that require this conversion:

$$[vecs]\psi_E=\psi_x$$

$$\psi_E = [vecs]^{-1} \psi_x$$

Keeping this relation in mind, we are freed to explore TDSE problems as a vector or matrix's basis is no longer a limiting factor. In partocular, non-stationary quantum states can be further explored. We can simply express the wave function in an energy basis and then convert it back to the position basis after the needed operation is performed.

[Next Section: The Particle In a Box Paradigm (PIB)](/Master3.md)

[Previous Section: Vectors & Quantum State Descriptors](/Master1.md)

[Home](/README.md)
