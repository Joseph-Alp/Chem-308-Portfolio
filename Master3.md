# The Particle In The Box

The Particle in a Box (PIB) describes some particle of mass, m that is confined between two walls at x = 0 and x = L: 
the potential energy is zero inside the box but rises abruptly to infinity at the "walls" or boundaries. This ensures that the 
observed particle *must* exist somewhere within the set boundaries.
This model is an idealization of the potential energy of a gas-phase molecule that is free to move in a one-dimensional container.
*We see this model probed and explored from week 1 - week 4 of the MatLab chapters.

For our purposes, we focused a single particle in a one dimentional box of width a= 1 nm. We then set the potential energy inside the box to 0. At the boundary for our box, we set the potential energy to a value larger than the particle’s total energy. The potential energy is  also given by a matrix in the position basis. Using what we know about our linear algebraic assumptions, the potential matrix contains the values of the potential energy for reach position (x) along its diagonal. We are this able to set the number of position points by discretizing our space. After determining these variables, we then construct the kinetic energy matrix, which takes the form of the wave function's second derivative (found through both the right and left hand derivatives). After perfomring these calculations in MatLab, we are able to solve the TISE to yield the energy eigenvectors of the first five states:

![eigenvectors](/eigenvalues.png)
