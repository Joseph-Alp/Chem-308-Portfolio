function	PosAndMomVarWidth
% Make two 3d plots of psi, one in position space and the
% other in momentum space.

n = 200;
Lx = 10;
x = linspace(-Lx/2,Lx/2,n)';
    dx = abs(x(2)-x(1));
k = ((2*pi)./Lx) .* [-n/2 : 1 : (n/2)-1]';
    dk = abs(k(2)-k(1));

gWidth = [100 10 1];

for kIter = 1:3
for iter = 1:3
    xInit = -Lx/5;
    kInit = -max(k)/5;
    xCenter = [ [xInit:dx:-xInit] [-xInit:-dx:xInit] ];
    kCenter = [0 -kInit kInit];
    animLimit = length(xCenter);

for  j = 1:animLimit
    xvec = exp(-gWidth(iter).*(x-xCenter(j)).^2) .* exp(1i.*kCenter(kIter).*x);
    pvec = fftshift(fft(fftshift(xvec)));
    mx = max(abs(pvec));
    pvec = pvec./mx;

%%% create  3 x n  matrices to define wedges with tips on x axis:
    [Rx,Ix,Rp,Ip,Xx,Yx,Zx,Xp,Yp,Zp] = wedges(xvec,pvec,x,n,k);
 
%%% superimpose mesh and plot3 on shaded plot
	h1 = figure(1);
    subplot(1,2,1)
%         MjC_plot3(Xx,Yx,Zx,x,Rx,Ix,'r','Position Space')
        MjC_plot3(Xx,Yx,Zx,x,Rx,Ix,'r',1)
        title('Position Space')
  %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
    subplot(1,2,2)
%         MjC_plot3(Xp,Yp,Zp,k,Rp,Ip,'b','Momentum Space')
        MjC_plot3(Xp,Yp,Zp,k,Rp,Ip,'b',10)
        title('Momentum Space')
    drawnow
    if j == round(animLimit/4)+1
        pause(2)
    elseif j == round(3*animLimit/4)
        pause(2)
    end
end
end
end
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function  [Rx,Ix,Rp,Ip,Xx,Yx,Zx,Xp,Yp,Zp] = wedges(xvec,pvec,x,n,k);
%%% for 3d graphs create  3 x n  matrices to define wedges
%%% with tips on x axis
      Rx = real(xvec); % pos space
      Ix = imag(xvec); % pos space	
      Rp = real(pvec); % mom space
      Ip = imag(pvec); % mom space

      Xx = [x';x';[x(2:n);x(n)]']; % pos space
      Yx = [zeros(1,n);Rx';[Rx(2:n);0]']; % pos space
      Zx = [zeros(1,n);Ix';[Ix(2:n);0]']; % pos space PosAndMomVarWidth
      Xp = [k';k';[k(2:n);k(n)]']; % mom space
      Yp = [zeros(1,n);Rp';[Rp(2:n);0]']; % mom space
      Zp = [zeros(1,n);Ip';[Ip(2:n);0]']; % mom space
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function   MjC_plot3(Xx,Yx,Zx,x,Rx,Ix,clr,A)
   
        mesh(Xx,Yx,Zx);  % create surface plot
        hold on;
              plot3(x,Rx,Ix,clr); % superimpose red spiral 
              f = fill3([0 0 0 0],[1 -1 -1 1],[1 1 -1 -1],clr);
              alpha(f, 0.05);
              plot3([0 0 ],[-1 1],[0 0],'k') % add axes at origin
              plot3([0 0 ],[0 0],[-1 1],'k') % add axes at origin
        %camproj('perspective')
        hold off
%         title(Title);
    % adjust details of plot
      axis([-inf, inf, -1,1,-1,1])
      xRange = max(x) - min(x);
      daspect([A,1,1]);
      grid on
      colormap([0 0 0]) % use black lines in plot
      view([41,29])
end
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
