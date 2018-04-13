# PIB Using TISE

Below is a continuation of the work from Week 2, involving the PIB system. Only continuing to tweak the code and variables. As no new fundamental information is covered in this section, please read the code comments notated by "%" for any details. 

```Matlab
function PIB( n ) % n is the number of eigenvalues

% Defining Constants
hbar=1.05E-34;% hbar
m=9.11E-31; % mass in kilograms
l=5E-11; %5 nm
pts=300; % number of discritized points (for second derivative)
w=3; % number of points in barrier
barht=1E6; % bar height on potential matrix in our system
x=linspace(0,l,pts); % discretized all space
c=-(hbar.^2)./(2.*m); % constants in kinetic energy; note periods apply to elements only

% Defining second derivative matrix for kinetic energy
% A=-2*eye(pts); % 2 on diagonal
% b=ones(pts-1,1); % vector of 1
% B=diag(b,-1); % 1 below diagnol
% B2=diag(b,1); % 1 above diagnol
% D=A+B+B2; % second derviative
D=-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1); % second derivative matrix
```
This segment of code was introduced in order to set the constraints for the KE matrix. We also defined the PE matrix as well as the Hamiltonian operator which incorporates the KE and PE matricies.
```Matlab
% Kinetic energy matrix and constants
T=c.*D; %See 1/25 notebook for notation details for reference 

% Defining Potential Energy Matrix
Vvec=zeros(pts,1); %see notes from 1/23/18 for corresponding image
Vvec([1:w,(end-(w-1)):end])=barht;
V=diag(Vvec);

% Defining the Hamiltonian Operator
H=T+V; % Hamiltonian (H) matrix %potential and kinetic energy matrices
[vecs,vals]=eig(H); % finds eigenvectors and eigenvalues (vals is matrix form of eigenvalues)
[srtvecs,srtvals]=eigsort(vecs,vals); %arranges eigenvalues in ascending order
v=diag(srtvals); % vector of sorted eigenvalues
k=[1:1:pts]; % row vector of evenly spaced numbers with number of pts defined
n=ones(pts,1); % column vector of 1s
repvals=0.25*n*k;
shiftvecs=srtvecs+repvals; % eigenvectors shifted based on the repval matrix
figure(1);plot(x,shiftvecs(:,1:8),x,Vvec); % plot potential well and eigenvectors (1-8)
axis([-inf inf -.25 2.5]); % custom axes to view eigenvectors

end

% Ascending Code From Week 3, Part 2
function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```
[Next Section: Finalized TISE, PIB Code](/MLW4.md) 

[Previous Section: Code For Defining The KE Matrix For PIB](/MLW2.md) 

[Home](/README.md)
