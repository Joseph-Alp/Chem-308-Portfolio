The goal of this project was to continue getting comfortable with using vectors and matricies to describe quantum systems. The system
being probed is a PIB. 
The following criteria must be established in order to visualize the eigenvalues for a PIB function:
  1. Define all constants
  2. Discretize all space
  3. Define matrix (V), kinetic energy (T), and their sum (H) as matricies 
  
function PIB( n ) %n is number of eigenvalues
%constants defined
hbar = 1.05E-34/; %hbar in Js
m = 9.11E-31; %mass in kilograms
l = 5E-9; %5 nm
pts = 250; %number of discritized points {for second derivative}
w = 3; %number of points in barrier
barht = 1E6; %bar height on potential matrix. (see 1/23/18 notes for reference)
x = linspace(0,l,pts); % discretized space
c = -(hbar.^2)./(2.*m); %constants in kinetic energy (periods limit operation to elements only)

%Defining Second Derivative Matrix for Kinetic Energy
% A = -2*eye(pts); % 2 on diagonal
% b = ones(pts-1,1); % vector of 1
% B = diag(b,-1); % 1 below diagnol
% B2 = diag(b,1); % 1 above diagnol
% D = A+B+B2; % second derviative
D = -2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1); % second derivative matrix

%Kinetic Energy Matrix 
T = c.*D;

%Defining the Potential Energy Matrix
Vvec=zeros(pts,1);
Vvec([1:w,(end-(w-1)):end])=barht;
V=diag(Vvec);

%Defining Hamiltonian Operator
H = T+V; % determine H by potential and kinetic energy matrices
[vecs,vals]=eig(H); % finding eigenvectors and eigenvalues
vals=diag(vals); % making eigenvalues into vector (same size as x=pts)
figure(1);plot(x,Vvec); % plot of potential energy vs discretized points

end
