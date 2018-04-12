```Matlab
function    LEPS_MolecDynamics
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%% Two dimensional version of velocity Verlet algorithm used to compute
%  classical molecular dynamics trajectories on a LEPS surface. Surface is
%  for exchange reaction: A + BC -> AB + C.
%  Vectors are used to compactly store x and y behaviors.
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%% Define Fixed Parameters
    m = 1.0;            % mass
    dr = [0.02  0.02];  % differential distance along x and y, as column vector
    t = 0;
    dt = 0.02;
    rmax = 4;   
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%% Surface Choice: change these to observe chemical reactivity
      surface = 1; % early barrier surface
    % surface = 2; % late barrier surface
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%% Other Parameters: change these to determine chemical reactivity
    r = [3.99 0.85];     % initial position
    v = [-6.2 -3];       % velocity of the reactants
    a = [0 0];           % initial acceleration components
            % Define initial state of system
            % For a good time try, for surface = 1
            % r = [3.75 .85 ];
            % v = [-4.87 -3 ];
    j = 0; % initialize loop counter
    figure(1)
    clf
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%% Loop for Graphing
while max(r) < rmax 
    j = j + 1;
    t(j+1) = t(j) + dt;
  % compute next step along trajectory
    r(j+1,:) = r(j,:) + v(j,:).*dt + 0.5*a(j,:).*dt.^2;
    F(j+1,:) = MjC_LEPS_F( r(j+1,:),dr,surface ); % LEPS force
    a(j+1,:) = F(j+1,:)./m ; 
    v(j+1,:) = v(j,:) + 0.5*(a(j+1,:) + a(j,:)).*dt;
  % store potential and kinetic energies for plotting
    Vtraj(j+1,:) = MjC_LEPS( r(j+1,:),surface ); % potential energy at each point in trajectory
    T(j+1) = 0.5*m*( v(j+1,1).^2 ) + 0.5*m*( v(j+1,2).^2 ); % kinetic energy
    
    com = (r(j+1,1)+r(j+1,2) + r(j+1,1)+r(j+1,2))./3; % center of mass
    rA = r(j+1,1) - com;
    rB = r(j+1,2) - com;
    rC = r(j+1,1)+r(j+1,2) - com;
% Plot vectors after loop has completed

    subplot(3,2,1)
        h = plot( rA,0,'g.',rB,0,'r.',rC,0,'b.','MarkerSize',15);
       if j == 1;
           h = plot( [ rA rB rC ], 0,'.','MarkerSize',35);
           axis([-rmax rmax -2 2])
           title([' {\color[rgb]{.8 0.1 0.1}atom A,  \color[rgb]{.96 .77 .26}atom B,   \color[rgb]{.23 .52 .77}atom C} '])
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%   
    subplot(3,2,[3 5])
        if j == 1;
            % plot LEPS surface first iteration of loop only
            [V,r1,r2] = rMjC_LEPS_Surface(rmax,surface);
            contour3(r1,r2,V,35)
            hold on
            g = surf(r1,r2,V);
            shading interp
            alpha(0.3)
            AxisLims = axis;
            hold on
        end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%  
        plot3( r( 2:end , 1),r( 2:end , 2),Vtraj(2:end),'r.',...
            r( 2:end , 1),r( 2:end , 2),Vtraj(2:end),'b' )
        axis(AxisLims);
        view(0,90);
        xlabel('A - BC separation');
        ylabel('AB - C separation')
        title('A + BC \rightarrow AB + C')
        axis square
        drawnow
        rotate3d on
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
    subplot(3,2,2)
        plot(t,r)
        title('Position Components')
        legend('AB sep.','BC sep.')
    subplot(3,2,4)
        % plot velocity components
        plot(t,v)
        title('Velocity components')
    subplot(3,2,6)
        % plot energies
        plot(t,T)
        hold on
        plot(t,Vtraj)
        plot(t,T' + Vtraj)
        hold off
        title('Energy')
        legend('kinetic E','potential E','total E')

end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
function F = MjC_LEPS_F(r,dr,surface);
s = surface;
%LEPS force computed from LEPS potential
%     Horiz = ( MjC_LEPS([r(1)+dr(1),r(2)]) - MjC_LEPS([r(1)-dr(1),r(2)]) )./(2*dr(1));
%     Vert  = ( MjC_LEPS([r(2)+dr(2),r(1)]) - MjC_LEPS([r(2)-dr(2),r(1)]) )./(2*dr(2));
    Horiz = ( MjC_LEPS([r(1)+dr(1),r(2)],s) - MjC_LEPS([r(1)-dr(1),r(2)],s) )./(2*dr(1));
    Vert  = ( MjC_LEPS([r(2)+dr(2),r(1)],s) - MjC_LEPS([r(2)-dr(2),r(1)],s) )./(2*dr(2));
    F = -[ Horiz Vert ]; % -1*average of L and R = force  
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
function  [V,r1,r2] = rMjC_LEPS_Surface(rmax,surface);
n = 50;
r = linspace(0.4,rmax,n)';
[r1, r2] = meshgrid(r,r);

for j = 1:n
for k = 1:n
   V(j,k) = MjC_LEPS([r1(j,k) r2(j,k)],surface); 
end
end

end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
function  [V,r1,r2] = MjC_LEPS_Surface(rmax,surface);
    n = 50;
    r = linspace(0.4,rmax,n)';
    [r1, r2] = meshgrid(r,r);

    for j = 1:n
    for k = 1:n
       V(j,k) = MjC_LEPS([r1(j,k) r2(j,k)],surface); 
    end
end
            figure
            contour3(r1,r2,V,35)
            hold on
            g = surf(r1,r2,V);
            shading interp
            alpha(0.3)
            if surface == 1
                title('Early Barrier')
            else
                title('Late Barrier')
            end
            
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
function V = MjC_LEPS(R,surface)
% Input R should have [r1 r2]. r3 will be calculated from them.

 if nargin == 0
    r1 = 2.5; % AB
    r2 = 0.75; % BC
    r3 = r1 + r2; % AC
    R = [r1 r2 r3];
end
    r1 = R(1); % AB
    r2 = R(2); % BC
    r3 = r1 + r2; % AC
    R = [r1 r2 r3];

% Which surface should be used? 1 for early barrier, 2 for late barrier
    % surface = 1; 
        if surface == 1
        % Surface I; early barrier
            a = 0.05;
            b = 0.30;
            c = 0.05;
        else    
        % Surface II; late barrier
            a = 0.30;
            b = 0.05;
            c = 0.05;
        end

% Bond dissociation energies: AB, BC, AC (kcal/mol)
    D1 = 109.435;
    D2 = 109.435;
    D3 = 79.435;
    D = [D1 D2 D3];

% Morse constant for exp decay; same for AB, BC, AC (1/angstroms)
    beta = 1.942; 
    
% Equilibrium bond lengths; same for AB, BC, AC (angstroms)    
    re = 0.742; 
    
% Compute {Q1, Q2, Q3, J1, J2, J3} from r1, r2, and r3
for j = 1:3
    r = R(j); % select AB, BC, or AC distance
    Q(j) = D(j)/4*(3*exp(-2*beta*(r-re))-2*exp(-beta*(r-re))); % Coulomb
    J(j) = D(j)/4*(exp(-2*beta*(r-re))-6*exp(-beta*(r-re))); % Exchange
end

% Create LEPS surface from coulomb and exchange terms
    V = Q(1)/(1+a) + Q(2)/(1+b) + Q(3)/(1+c)...
        -sqrt( (J(1)/(1+a))^2 + (J(2)/(1+b))^2 + (J(3)/(1+c))^2 -...
        (J(1)*J(2))/((1+a)*(1+b)) - (J(2)*J(3))/((1+b)*(1+c))...
        - (J(1)*J(3))/((1+a)*(1+c)) );   
end
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% 
```
