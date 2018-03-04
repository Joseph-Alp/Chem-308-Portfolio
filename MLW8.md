{% include mathjax.html %}

So far throughout this course, the TDSE has been observed in terms of the differential as described in the [Master](/Master.md).  Now,
we are interested in the differences with respect to the position and time components of the wave function used in the TDSE. In order to
do this, the steps to re-write the TDSE in light of this new inquiry are described as follows:

# The TDSE Difference Equation 

We already know the TDSE to be: \begin{equation}\label{differential} \hat{H}\psi_{(x,t)}=i\hbar\frac{\partial\psi_{(x,t)}}{\partial t} \end{equation}.

- This form of the TDSE includes the partial derivative $$\frac{\partial\psi_{(x,t)}}{\partial t}$$. 
Here, the partial derivative describes the small changes in $$\psi_{(x,t)}$$ with respect to $$t$$. This partial derivative
can be further altered by swapping the change in wave function with a delta as seen: 
\begin{equation}\label{delta2} \hat{H}\psi_{(x,t)}=i\hbar\frac{\Delta\psi_{(x,t)}}{\Delta t} \end{equation}

- The equation in the form does not completely get us to where we want, as there now exists a ratio of the wave function over the change in time.
This can be remedied by taking it a step further:

Rewriting $$\Delta\psi_{(x,t)}$$ as the difference between two states yields: 
\begin{equation}\label{delta3} \Delta\psi_{(x,t)}=\psi_{(x,t+\Delta t)}-\psi_{(x,t)} \end{equation}

However, we want to be able to graph the wave function at a certain time! Leaving our wave function in this format is clunky, and 
can be further simplified by solving for $$\psi_{(x,t+\Delta t)}$$ in the above equation (3). This will provide us the ability to graph 
the wave function after the delta time change. 

- By substituting $$\Delta\psi_{(x,t)}$$ with (2), we see that:
\begin{equation}\label{delta4} \hat{H}\psi_{(x,t)}=i\hbar\frac{\psi_{(x,t+\Delta t)}-\psi_{(x,t)}}{\Delta t} \end{equation}

This form of the wave function we want for the TDSE. Using simple algebraic manipulation and factoring out our constants,
we can isolate the wave function with the delta t to yield: 

\begin{equation}\label{delta7} \psi_{(x,t+\Delta t)}=(\frac{\Delta t}{i\hbar}\hat{H}+1)\psi_{(x,t)} \end{equation}

It was a point of initial contention if $$\psi_{(x,t)}$$ could have been factored out of the overall equation. After realizing that 
this is no different than saying the Hamiltonian operator is the sum of the kinetic and potential energy operators, we were able to 
continue with the factoring with ease. As we are not pulling out anything being acted upon by a different Hamiltonian, we are in good shape. 
This is no different than pulling out a scalar. 

This our new, rewritten wave function that is equal to the operator that is used to operate on the original wave function. If 
we want to delve into the minutiae of how this new wave function would look like in MatLab, we can do this simply by studying our equation:

We already know that the operator is the sum of two matrices: 
* The constants & the Hamiltonian operator
* The scalar of one with values along the diagonal 

Using this, we can neatly plot wave functions after defining our change in time and use 
the output of the operation input for the next. 



