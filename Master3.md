# The Particle In The Box

The Particle in a Box (PIB) describes some particle of mass, m that is confined between two walls at x = 0 and x = L: 
the potential energy is zero inside the box but rises abruptly to infinity at the "walls" or boundaries. This ensures that the 
observed particle *must* exist somewhere within the set boundaries.
This model is an idealization of the potential energy of a gas-phase molecule that is free to move in a one-dimensional container.
*We see this model probed and explored from Week 1 - Week 4 of the MatLab chapters.

For our purposes, we focused a single particle in a one dimentional box of width a= 1 nm. We then set the potential energy inside the box to 0. At the boundary for our box, we set the potential energy to a value larger than the particle’s total energy. The potential energy is  also given by a matrix in the position basis. Using what we know about our linear algebraic assumptions, the potential matrix contains the values of the potential energy for reach position (x) along its diagonal. We are this able to set the number of position points by discretizing our space. After determining these variables, we then construct the kinetic energy matrix, which takes the form of the wave function's second derivative (found through both the right and left hand derivatives). After perfomring these calculations in MatLab, we are able to solve the TISE to yield the energy eigenvectors of the first five states:

![eigenvectors](/eigenvalues.png)

The code used to generate this image can be found in the Week 1 - Week 4 MatLab codes and are explained in depth. However, a quick glimpse
of the coude can be found here.

```Matlab
% First need to define constants
  hbar=1;
  m=1; % mass of electron
  l=1; % length of box 
  pts=250; % number of discretized points
  w=3; % number of points within infinite wall
  x=linspace(0,l,pts); % discretized space
  dx=x(2)-x(1);
  barht=1E6; %bar height on potential matrix
  c=-(hbar.^2)/(2.*m); % constant in kinetic energy operator
% Next can use kinetic and potential matrices already defined
  H=T+V
% Next determine eigenvectors and eigenvalues
  [vecs,vals]=eig(H); 
% Separate states by eigenvalues
  sc=-100 % scalar factor
  vecs=sc*vecs
  repvals=(ones(pts,1))*vals';
  shiftvecs=srtvecs+repvals;
% Finally plot eigenvectors for different states
  figure(1);plot(x,shiftvecs(:,1:n),x,Vvec);
  axis([-inf inf -.5 300]); % adjusts axes to be able to see eigenvectors
  ```
  
Using this code, we have a program which discritizes space and combines the PE and KE into a PIB hamiltonian matrix. These two matricies are combined suh that: One is a matrix composed of the sorted eigenvectors, the other has eigenvalues of the total energy matrix with diagonal elements of another matrix, vals. Once the eigenvalues and eigenvectors of the Hamiltonian matrix were found, these eigenvalues and eigenvectors were sorted so that they will be plotted in terms of increasing energy. As we increase in our energy, we see the formation of more nodes. The figure above contains an *n* number of eigenvectors for the 1-D PIB.

[Previous Section: Observable Operator Properties](/Master2.md)

[Home](/README.md) 
