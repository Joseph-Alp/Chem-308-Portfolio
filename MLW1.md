{% include mathjax.html %} 


[Home](/README.md)


Kinetic Energy within a PIB

This brief code details the parameters for kinetic energy within a PIB system. Here, we have defined our function as dependent on three variables which constitute a series of vectors. We have specified our inputs: where n is the size of our matrix and dx is the change in our x variables.

Additionally, we define both sides of our matrix as right and left. 
```Matlab
function [R,L,D] = kinetic(n,dx) % n = the size of matrix; dx = the change in x

% M = -eye(n);
% a = ones(n-1,1);
% R = M + diag(a,-1);
R = (1/dx)*(-eye(n) + diag(ones(n-1,1),-1)); % the right derivative matrix

``` 
The second half of this code wraps up the left derivative matrix, and prepared to take its second derivative for the right and left side
in order to calculate the total kinetic energy for the PIB.

```Matlab
% N = eye(n);
% b = -1*ones(n-1,1);
% L = N + diag(b,1);
L = (1/dx)*(eye(n) + diag(-1*ones(n-1,1),1)); % the left derivative matrix

% Da = R*L; %first entry -1
% Db = L*R; % last entry -1
% D = (Da + Db)/2;

D = (R*L + L*R)/2; % second derivative

end function 
```
