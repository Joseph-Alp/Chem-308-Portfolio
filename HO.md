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
Likewise, the same can be said for this code segment, as it was previously discussed in depth. The only modification made for this project was changing the sc to 75, which allowed greater spacing between our eigenvectors on our figure, making it easier to visualize. 
```Matlab
% Kinetic energy matrix and constants
T=c.*D; 

% Defining Potential Energy Matrix
%Vvec=zeros(pts,1); %see notes from 1/23/18 for corresponding image
%Vvec([1:w,(end-(w-1)):end])=barht;
k=1000;
Vvec=0.5*k*x.^2
V=diag(Vvec);

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
This is where the new segment has come into play, and merits discussion. The purpose of this project is to apply our PIB code, into a model that tests the Selection Rules for a Harmonic Oscillator system. We can think of this system as a heteronuclear, diatomic compound, such as H-Cl. If we visualize H-Cl in this light, we can reason that the "heavy" chlorine atom remains relatively stationary, while the hydrogen atom bound to it is moving in an assortment of transitions. In other words, there is a dipole in the direction of chlorine. This manifests mathematically into the formulation: <$\Psi_{i}, x, $\Psi_{f}> $ = scalar quantity. In other words, this is the vecs vector transpose multiplied by the position operator matrix, times the vecs vector. This provides us the possibility of seeing all the transitions possible for our system. Thus, we plug in the code below using the pcolor command, which allows us to visualize a subset of the total amount of transitions possible. 
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

It turns out that the only transition allowed for our HO follows the selection rule of /DeltaV = +/- 1. 
