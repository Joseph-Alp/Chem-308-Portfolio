{% include mathjax.html %}

# Morse Potential

From Quantum, we understand the Harmonic Oscillator to be an approximation from classical physics. This is due in partially to the fact that an arbitrary potential curve  V(x)  can usually be approximated as a harmonic potential. Furthermore, it is one of the few quantum-mechanical systems for which an exact, analytical solution exists.  

In the previous section, we saw how to solve for the HO, PIB in accordance to our selection [rules](/HO.md) in MatLab. However, this also results in a lot of anharmonicity for our model as we are largely approximating. A much more effective method of approximation for the vibrational structure of the molecule than the harmonic oscillator is to incorporate the Morse Potential. This is because it explicitly includes the effects of bond breaking and accounts for the anharmonicity of real bonds with non-zero transition probability for overtone and combination bands.

The Morse Potential is a good approximation to $$/V(x)$$, and using the same code as the previous section, we can incorporate this into our HO model. 


```Matlab
function MorsePotential(n)

hbar=1; %hbar in Js
m=1; % mass of electron
l=1; % 5nm 
pts=250; % number of discretized points
w=3; % number of points in barrier
x=linspace(-1,l,pts); % discretized space
dx=x(2)-x(1);
barht=1E6; %bar height on potential matrix
c=-(hbar.^2)/(2.*m); % constant in kinetic energy operator
k=1e3; % spring constant for potential energy operator
q=-1; %charge of electron 
De=1e3;
a=1;

% Defining Kinetic Energy Operator (Matrix) (T)
% A=-2*eye(pts); % 2 on diagonal
% b=ones(pts-1,1); % vector of 1
% B=diag(b,-1); % 1 below diagnol
% B2=diag(b,1); % 1 above diagnol
% D=A+B+B2; % second derviative
D=(1/((dx)^2)).*(-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1)); %Second derivative matrix
T=c.*D;
```
This is the only section modified to include the Morse Potential, where Vvec is redefined to include the Morse Potential.
```Matlab
%Define PE Operator (matrix), (V) w/h Morse Potential
Vvec=De*(1-exp(-a*x)).^2;
V=diag(Vvec);
```
```Matlab
H=T+V; % Hamilotian Operator Matrix (H)

[vecs,vals]=eig(H); % determining eigen vectors and eigenvalues
[vecs,vals]=eigsort(vecs,vals); % sorting eigenvalues in ascending order
sc=100;
vecs=sc*vecs;
v=diag(vals); % vector of sorted eigenvalues
% % figure(5)
% % plot(v(1:100))
% %r=ones(pts,1); % column vector of 1's
repvals=(ones(pts,1))*v';
% % repvals(1:6,1:6)
shiftvecs=vecs+repvals; % eigenvectors shifted based on repvals matrix

%figure(1);plot(x,Vvec);
%figure(1);plot(x,vecs(:,1:n));
figure(1);plot(x,shiftvecs(:,1:n),x,Vvec); % plot potential well and eigenvectors (1-5)
axis([-inf inf 0 450]); % adjusts axes to be able to see eigenvectors
end

function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```

We are then able to visualize the first ten energy levels, where we can see the wave function behavior. Where the wave function meets the well boundaries is where we can visualize tunnelling take place. It is also at these points where we see KE = 0, and PE = max. The concave curvature of the wave function at each energy level creates nodes. The area under these curves express the probability density of locating our particle, which can be expressed by the expectation value for position. 

![MP](/MP.png)

Unlike the energy levels of the harmonic oscillator potential, which are evenly spaced by ħω, the Morse potential level spacing decreases as the energy approaches the dissociation energy. 

[Home](/README.md)

