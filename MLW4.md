
# Updated, Finalized Format For PIB 

In order to have normalized data for our PIB, we set our constants equal to 1. We set the number of discretized spaces to 100 across all groups to ensure uniformity. Other than this brief modifications, the constant values are the same as in [week 2](/MLW2.md). 

```Matlab
function PIB( n ) % n is the number of eigenvalues

% Defining Constants
hbar= 1;% hbar 1.05E-34
m=1; % mass in kilograms 9.11E-31
l=1; %5 nm 5E-11
pts=100; % number of discritized points (for second derivative)
w=3; % number of points in barrier
barht=1E6; % bar height on potential matrix in our system
x=linspace(0,l,pts); % discretized all space
dx=x(2)-x(1); %dx definition
c=-(hbar.^2)./(2.*m); % constants in kinetic energy; note periods apply to elements only
```
Here, the second derivative matrix, defined as D, is organized. This complies all of the constants defined above into a formula capable of providing us with a wave function for our particle further down the line.

```Matlab
% Defining second derivative matrix for kinetic energy
% A=-2*eye(pts); % 2 on diagonal
% b=ones(pts-1,1); % vector of 1
% B=diag(b,-1); % 1 below diagnol
% B2=diag(b,1); % 1 above diagnol
% D=A+B+B2; % second derviative
D=(1/((dx)^2)).*(-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1)); % second derivative matrix
```

Here, we have set up our the kinetic energy matrix, and will be modifying this section further. In short, the KE matrix is equal to the speed of light multiplied by the complex congugate of our second derivative matrix.

```Matlab
% Kinetic energy matrix and constants
T=c.*D; %See 1/25 notebook for notation details for reference 
```

The potential energy for our system is given by a matrix in the position basis. The matrix has the values of the potential energy for reach position (x) along its diagonal. The number of position points is discrete and can easily be varied in our Matlab code pending our needs, which we determined back in our constants section. To create the potential energy matrix, we need to create a square matrix of some desired size. The matrix originally has zeros in all its entries, then we add the potential energy values on its diagonal using the following code:

```Matlab
% Defining Potential Energy Matrix
Vvec=zeros(pts,1); %see notes from 1/23/18 for corresponding image
Vvec([1:w,(end-(w-1)):end])=barht;
V=diag(Vvec);
```

The next paramount feature of this code is to define our Hamiltonian operator, which we have determined to be equal to thesum of the KE matrix and potential energy.
```Matlab
% Defining the Hamiltonian Operator
H=T+V; % Hamiltonian (H) matrix %potential and kinetic energy matrices
```
This last major chunk of code is were most of the calculations take place. As we have already defined our KE and PE matricies, as well as our Hamiltonian, we can insert our vecs and vals to solve for our eigenvectors and eigenvalues for the PIB, respectively. These details are also noted in the comments for the code mentioned below:

```Matlab
[vecs,vals]=eig(H); % finds eigenvectors and eigenvalues (vals is matrix form of eigenvalues)
plot(vals)
[srtvecs,srtvals]=eigsort(vecs,vals); %arranges eigenvalues in ascending order
sc=100;
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

end
```

This is the code previously mentioned that arranged the eigenvalues in ascending order for ease of interpretation in the final figure. 
```Matlab 
function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```
[Home page](/README.md))
