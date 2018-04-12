{% include mathjax.html %}

# Harmonic Oscillator Code

Now that we have laid the foundation for what the Selection Rules allow us to observe in quantum states, we can test this newfound knowledge with our simple, PIB code that was written in the early weeks of this course. 

We are already familiar with this segment, as it is just defining our constants found in our Schrodinger Equation, and defining the parameters for our infinite well. 

```Matlab
function PIB( n ) % n is the number of eigenvalues

% Defining Constants
hbar= 1;% hbar 1.05E-34
m=1; % mass in kilograms 9.11E-31
l=1; %5 nm 5E-11
pts=100; % number of discritized points (for second derivative)
w=3; % number of points in barrier
barht=1E6; % bar height on potential matrix in our system
x=linspace(-1,l,pts); % discretized all space, changed from 0 to -1
dx=x(2)-x(1); %dx definition
c=-(hbar.^2)./(2.*m); % constants in kinetic energy; note periods apply to elements only
```

The same may be said with this segment of code, which is just designing our second derivative matrix for KE, with non-zero values along the diagonal.
```Matlab
% Defining second derivative matrix for kinetic energy
% A=-2*eye(pts); % 2 on diagonal
% b=ones(pts-1,1); % vector of 1
% B=diag(b,-1); % 1 below diagnol
% B2=diag(b,1); % 1 above diagnol
% D=A+B+B2; % second derviative
D=(1/((dx)^2)).*(-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1)); % second derivative matrix
```
Here, our KE matrix is left untouched.

```Matlab
% Kinetic energy matrix and constants
T=c.*D; 
```
One critical modification to the PIB code, was to alter Vvec to be equal to the system's potential energy for the HO. Our "spring" potential, or k, is set to 1000 for our model. 
```Matlab
% Defining Potential Energy Matrix
%Vvec=zeros(pts,1); %see notes from 1/23/18 for corresponding image
%Vvec([1:w,(end-(w-1)):end])=barht;
k=1000;
Vvec=0.5*k*x.^2
V=diag(Vvec);
```
The only modification made for this code segment was to change the sc to 75, which allowed greater spacing between our eigenvectors on our figure, making it easier to visualize.
```Matlab
% Defining the Hamiltonian Operator
H=T+V; % Hamiltonian (H) matrix %potential and kinetic energy matrices
[vecs,vals]=eig(H); % finds eigenvectors and eigenvalues (vals is matrix form of eigenvalues)
plot(vals)
[srtvecs,srtvals]=eigsort(vecs,vals); %arranges eigenvalues in ascending order
sc=75; %changed from 100 for better spacing
srtvecs = sc*srtvecs
v=diag(srtvals); % vector of sorted eigenvalues
v(1:5)
figure(2); plot(1:100); % fiddling 
plot(srtvals)
n=ones(pts,1); % column vector of 1s
repvals=n*v';
shiftvecs=srtvecs+repvals; % eigenvectors shifted based on the repvals' matrix
figure(1);plot(x,shiftvecs(:,1:8),x,Vvec); % plot potential well and eigenvectors (1-8)
axis([-inf inf -.25 200]); % custom axes to view eigenvectors
```
This is where the new segment has come into play, and merits discussion. The purpose of this project is to apply our PIB code, into a model that tests the Selection Rules for a Harmonic Oscillator system. We can think of this system as a heteronuclear, diatomic compound, such as H-Cl. If we visualize H-Cl in this light, we can reason that the "heavy" chlorine atom remains relatively stationary, while the hydrogen atom bound to it is moving in an assortment of transitions. In other words, there is a dipole in the direction of chlorine. This manifests mathematically into the formulation: < $$\psi_{i}$$, x, $$\psi_{f}$$ >  = scalar quantity. In other words, this is the vecs vector transpose multiplied by the position operator matrix, times the vecs vector. This provides us the possibility of seeing all the transitions possible for our system. Thus, we plug in the code below using the pcolor command, which allows us to visualize a subset of the total amount of transitions possible. 

To find the probability of a transition from a state $\psi_n$ to $\psi_m$ is given by the transition integral given by

$M_{nm}=\int \psi_n \vec{\mu} \psi_m $.

In order to calculate this, we must change this integral into an inner product. The transition probability is the given by

$M_{nm}=<\psi_n, \vec{\mu} \psi_m >$.

This form is ready for Matlab computation. The code notated below using "M=vecs...." calculated the transition probability.

```Matlab
%Harmonic Oscillator Selection Rules
M=vecs'*diag(x)*vecs %This describes our vecs', reduced mass matrix, and vecs
pcolor(abs(M(1:10, 1:10)).^2) %This sets up our pcolor graph
%colormap gray %If you want graph in grayscale
axis square
end
```
This simple segment of code is what arranged the eigenvalues in ascending order, and was already mentioned previously.
```Matlab
function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```

The resulting figure from this code testing the Selection Rules for a Harmonic Oscillator is:

![HO](/HO.png)

Here we see that the only transition allowed for our HO follows the selection rule of $$DeltaV$$ = +/- 1. This is incredible to calculate,
as we can finally understand what populating MO's means on a quantum scale!

This expounds the concept by applying an oscillating electric field (i.e. light) to a system, and the effect of this oscillating electric field can be visualized by observing how other states then become populated. If the energy of the photon is sufficient enough for the transition to occur, higher energy states can also be populated. 

We can see this same phenomenon in another diagram:

![Transitions](/transitions.gif)

Q: What exactly is this animation showing us, and how does it relate to the one earlier in this section describing the transitions that are permissible?

A: This animation shows the oscillation of our wave function, which we have already defined. The graph on the right displays the amount of contribution from each energy level; for this example there are five. When we start the animation, nearly all of the energy contribution stemmed from the ground state which is highlighted as the orange line. However, as the system continuously gains more energy from the oscillation electric field, more energy levels are then accessible, allowing there to be more contributions from more energy states.

# Final Implications 

This potential well can be applied using the TDSE in a similar way to PIB described in this entire chapter. Both the harmonic oscillator and the Morse Potential can be used to describe the transitions that are allowed in light of an oscilating electric field or without. In the next section is an image of the first 10 energy levels for the HO well. They are evenly spaced and there is more electron density towards the middle of the well than the sides. Accompanied with the image is the complete code with its breakdown.


[Next Section: Exploring the Morse Potential](/MorsePotential.md)

[Previous Section: Quantum Selection Rules](/Selection_Rules.md)

[Home](/README.md)
