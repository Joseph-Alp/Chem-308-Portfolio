```Matlab
function    MolecDynamics_LJ
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Two dimensional version of velocity Verlet algorithm.
% Vectors are used to compactly store x and y behaviors.
% Define fixed parameters
    m = 1.0;   % mass
    dr = [0.02  0.02];% % differential distance along x and y, as column vector
    t = 0;
    dt = 0.02;
    rmax = 4;
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Define initial state of system
    r = [3.9  1.1];   % initial position
    v = [-1.5 -0];    % initial velocity components
    a = [0 0];    % initial acceleration components
    F = [0 0];
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Lennard-Jones parameters
    epsilonAB=1;
    epsilonBC=1;
    epsilonAC=1;
    sigmaAB=1;
    sigmaBC=1;
    sigmaAC=1;
    params = [epsilonAB,epsilonBC,epsilonAC,sigmaAB,sigmaBC,sigmaAC];
    
    j = 0; % initialize loop counter
    figure(1)
    clf
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% Apply velocity Verlet integration, build up vectors for plotting
% for j = 1:1000
while max(r) < rmax
    j = j + 1;
    r(j+1,:) = r(j,:) + v(j,:).*dt + 0.5*a(j,:).*dt.^2;
    F(j+1,:) = LJ_F( r(j+1,:),dr,params );
    a(j+1,:) = F(j+1,:)./m ; % Lennard-Jones force
    v(j+1,:) = v(j,:) + 0.5*(a(j+1,:) + a(j,:)).*dt;
    Vtraj(j+1,:) = LJ_Vr( r(j+1,:),params ); % potential energy at each point in trajectory
    T(j+1) = 0.5*m*( v(j+1,1).^2 ) + 0.5*m*( v(j+1,2).^2 ); % kinetic energy
    t(j+1) = t(j) + dt;

    
    com = (r(j+1,1)+r(j+1,2) + r(j+1,1)+r(j+1,2))./3; % center of mass
    rA = r(j+1,1) - com;
    rB = r(j+1,2) - com;
    rC = r(j+1,1)+r(j+1,2) - com;
    subplot(3,2,1)
%         h = plot( rA,0,'g.',rB,0,'r.',rC,0,'b.','MarkerSize',15);
%        if j == 1;
       h = plot( [ rA rB rC ], 0,'.','MarkerSize',35);
       axis([-rmax rmax -2 2])
       title([' {\color[rgb]{.8 0.1 0.1}atom A,  \color[rgb]{.96 .77 .26}atom B,   \color[rgb]{.23 .52 .77}atom C} '])
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Plot vectors after loop has completed

    subplot(3,2,[ 3 5])
        % [V,r1,r2] = LEPS;
       if j == 1
           [V,r1,r2] = LJ_Plot(params);
            contour3(r1,r2,V,25)
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
%         view(98,78);
        view(0,90);
        xlabel('A - BC separation');
        ylabel('AB - C separation')
        axis square
        drawnow
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% 
subplot(3,2,2)
        % plot position
        plot(t,r)
        title('Position Components')
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
        
% optional quiver plot of force vectors
%         [V,r1,r2] = LJ_Plot(params) ;
% %         [F] = LJ_F([r1 r2],dr,params);
% %         F = LJ_F( r(2:end,:),dr,params);
% %         size(r)
% %         size(F)
%         quiver( r( 2:end , 1), r( 2:end , 2), F( 2:end , 1) , F( 2:end , 2)  )
%         hold on
%         contour3(r1,r2,V,25)
%         hold off
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%
function [F] = LJ_F(r,dr,params);
%Lennard-Jones force computed from LJ potential
    Horiz = ( LJ_Vr([r(1)+dr(1),r(2)],params) - LJ_Vr([r(1)-dr(1),r(2)],params) )./(2*dr(1));
    Vert = ( LJ_Vr([r(2)+dr(2),r(1)],params) - LJ_Vr([r(2)-dr(2),r(1)],params) )./(2*dr(2));
    F = - [ Horiz Vert ]; % -1*average of L and R = force   
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%
function   V = LJ_Vr(r,params)
% Lennnard-Jones potential at point r = [rAB rBC]
% Lennard-Jones parameters
    epsilonAB = params(1);
    epsilonBC = params(2);
    epsilonAC = params(3);
    sigmaAB = params(4);
    sigmaBC = params(5);
    sigmaAC = params(6);

% extract components of r from input    
    rAB = r(1);
    rBC = r(2);

    V = 4*epsilonAB*((sigmaAB./rAB).^12-(sigmaAB./rAB).^6)...
        +4*epsilonBC*((sigmaBC./rBC).^12-(sigmaBC./rBC).^6)...
        +4*epsilonAC*((sigmaAC./(rAB+rBC)).^12-(sigmaAC./(rAB+rBC)).^6);
end 
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%
function   [V,r1,r2] = LJ_Plot(params)
    epsilonAB = params(1);
    epsilonBC = params(2);
    epsilonAC = params(3);
    sigmaAB = params(4);
    sigmaBC = params(5);
    sigmaAC = params(6);
    
    rAB=[1:0.02:4];
    rBC=[1:0.02:4];
    [rAB,rBC]=meshgrid(rAB,rBC);
    
    r1 = rAB;
    r2 = rBC;

    V = 4*epsilonAB*((sigmaAB./rAB).^12-(sigmaAB./rAB).^6)...
        +4*epsilonBC*((sigmaBC./rBC).^12-(sigmaBC./rBC).^6)...
        +4*epsilonAC*((sigmaAC./(rAB+rBC)).^12-(sigmaAC./(rAB+rBC)).^6);
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```
