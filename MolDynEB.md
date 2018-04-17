```Matlab
function    MjC_LEPS_MolecDynamics
% Two dimensional version of velocity Verlet algorithm used to compute
% classical molecular dynamics trajectories on a LEPS surface. Surface is
% for exchange reaction: A + BC -> AB + C.
% Vectors are used to compactly store x and y behaviors.

% Define fixed parameters
    m = 1.0;            % mass
    dr = [0.02  0.02];  % differential distance along x and y, as column vector
    t = 0;
    dt = 0.02;
    rmax = 4;
    
% X = linspace(0,2*rmax,50); % for plot of circles marking atoms

% Set surface to 1 for early barrier, 2 for late barrier
    surface = 1; 

% Define initial state of system
        % For a good time try, for surface = 1
        %     r = [3.75 .85 ];
        %     v = [-4.87 -3 ];
    
    r = [3.75 0.85 ];     % initial position
    v = [-4.93 -3];         % initial velocity components
    a = [0 0];          % initial acceleration components
    
    j = 0; % initialize loop counter
    figure(1)
    clf
    
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
%         h = plot( rA,0,'g.',rB,0,'r.',rC,0,'b.','MarkerSize',15);
%        if j == 1;
           h = plot( [ rA rB rC ], 0,'.','MarkerSize',35);
           axis([-rmax rmax -2 2])
           title([' {\color[rgb]{.8 0.1 0.1}atom A,  \color[rgb]{.96 .77 .26}atom B,   \color[rgb]{.23 .52 .77}atom C} '])

           %            size(get(h,'XData'))
%        else
%            set(h,'XData',[ rA; rB; rC ]);
%        end
       
    
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

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

function F = MjC_LEPS_F(r,dr,surface);
s = surface;
%LEPS force computed from LEPS potential
%     Horiz = ( MjC_LEPS([r(1)+dr(1),r(2)]) - MjC_LEPS([r(1)-dr(1),r(2)]) )./(2*dr(1));
%     Vert  = ( MjC_LEPS([r(2)+dr(2),r(1)]) - MjC_LEPS([r(2)-dr(2),r(1)]) )./(2*dr(2));
    Horiz = ( MjC_LEPS([r(1)+dr(1),r(2)],s) - MjC_LEPS([r(1)-dr(1),r(2)],s) )./(2*dr(1));
    Vert  = ( MjC_LEPS([r(2)+dr(2),r(1)],s) - MjC_LEPS([r(2)-dr(2),r(1)],s) )./(2*dr(2));
    F = -[ Horiz Vert ]; % -1*average of L and R = force  
end

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

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

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```
