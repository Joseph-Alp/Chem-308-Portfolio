


The goal of this project was to continue getting comfortable with using vectors and matricies to describe quantum systems. The system
being probed is a PIB. We are going a sept further from the Week 1 code by actually defining our PIB, and then calculating the KE.

The following criteria must be established in order to visualize the eigenvalues for a PIB function:
  1. Define all constants
  2. Discretize all space
  3. Define matrix (V), kinetic energy (T), and their sum (H) as matricies 
  
Here, our function for our PIB is defined by an arbitrary number of eigenvalues. 
  
```Matlab 
function PIB( n ) %n is number of eigenvalues
``` 
It is important to define all of our constants within our system in order to understand our resulting wave functions.
As a result, we have defined our mathematical constants such as hbar, mass (m), lenth of our box (l), the height of our barrier (w), and the amount of discretized points which is important for taking the second derivative of our schrodinger equation. 
```Matlab
%constants defined
hbar = 1.05E-34/; %hbar in Js
m = 9.11E-31; %mass in kilograms
l = 5E-9; %5 nm
pts = 250; %number of discritized points {for second derivative}
w = 3; %number of points in barrier
barht = 1E6; %bar height on potential matrix. (see 1/23/18 notes for reference)
x = linspace(0,l,pts); % discretized space
c = -(hbar.^2)./(2.*m); %constants in kinetic energy (periods limit operation to elements only)
``` 

Here, the secondderivative matrix, defined as D, is organized. This complies all of the constants defined above into a formula capable of providing us with a wave function for our particle further down the line. 
```Matlab
%Defining Second Derivative Matrix for Kinetic Energy
% A = -2*eye(pts); % 2 on diagonal
% b = ones(pts-1,1); % vector of 1
% B = diag(b,-1); % 1 below diagnol
% B2 = diag(b,1); % 1 above diagnol
% D = A+B+B2; % second derviative
D = -2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1); % second derivative matrix
``` 
Here, we have set up our the kinetic energy matrix, and will be modifying this section further. In short, the KE matrix is equal to the speed of light multiplied by the complex congugate of our second derivative matrix. 
```Matlab
%Kinetic Energy Matrix 
T = c.*D;
```
The potential energy for our system is given by a matrix in the position basis. The matrix has the values of the potential energy for reach position (x) along its diagonal. The number of position points is discrete and can easily be varied in our Matlab code pending our needs.
To create the potential energy matrix in Matlab, we first need to create a square matrix of the desired size. The matrix originally has zeros in all its entries, then we add the potential energy values on its diagonal using the following code:

```MatLab
%Defining the Potential Energy Matrix
Vvec=zeros(pts,1);
Vvec([1:w,(end-(w-1)):end])=barht;
V=diag(Vvec);
```

%Defining Hamiltonian Operator
H = T+V; % determine H by potential and kinetic energy matrices
[vecs,vals]=eig(H); % finding eigenvectors and eigenvalues
vals=diag(vals); % making eigenvalues into vector (same size as x=pts)
figure(1);plot(x,Vvec); % plot of potential energy vs discretized points

end
```

[Home](/README.md)
