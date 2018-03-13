# Harmonic Oscillator Code

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

% Defining second derivative matrix for kinetic energy
% A=-2*eye(pts); % 2 on diagonal
% b=ones(pts-1,1); % vector of 1
% B=diag(b,-1); % 1 below diagnol
% B2=diag(b,1); % 1 above diagnol
% D=A+B+B2; % second derviative
D=(1/((dx)^2)).*(-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1)); % second derivative matrix


% Kinetic energy matrix and constants
T=c.*D; %See 1/25 notebook for notation details for reference 

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

%Harmonic Oscillator Selection Rules
M=vecs'*diag(x)*vecs %This describes our vecs', reduced mass matrix, and vecs
pcolor(abs(M(1:10, 1:10)).^2) %This sets up our pcolor graph
%colormap gray %If you want graph in grayscale
axis square
end

function [ srtvecs,srtvals ] = eigsort( vecs,vals )
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end
```
