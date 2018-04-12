{% include mathjax.html %}


# Born-Oppenheimer Approximation Using ($H_2^+$)

The Born-Oppenheimer Approximation states that because the mass of a nucleus is considered significantly larger than 
the mass of an electron, on the time-scale of the motion of an electron, the nucleus can be treated as stationary.
In reality, the nucleus is not stationary, but on the electron time-scale, 
the electron state does not change appreciably with the changing position of the nucleus.

So far in our analyses, we have only considered systems with one or two two particles. In this page, we will finally take into account
a system with three particles. In particular, a dihydrogen cation. 

Like many quantum problems, we have to take into account the Hamiltonian that will be used to describe the overall system: two nuclei
and one electron. By doing this, we can visualize our model in the image below:

![BO](/BO .jpg)

 Here we have two major interactions to consider: the separation between both nuclei and the distance of the elctron from the nuclei.
 
 The Hamiltonian to describe this system can be rewritten as a series of operators that describe the potential energy and kinetic energy 
 of the nuclei and the electron:
 1. The Hamiltonian must describe the translational motion of the electron and nuclei in the system in addition
 to the potential interactions between them
 1. The electronic function parametrically depends on the radius of the nuclei 
 1. Our separation of variables will allow for us to approximate in our calculations 
 
 We carried out this checklist in class by deriving the Hamiltonian, which is illustrated below: 
 
Ĥ =T̂ (nucleus) + T̂(electron) +V̂(nucleus−electron)+V̂(nucleus−nucleus)

$=(\frac{-\hbar^2 }{2M_a}\nabla^2_a + \frac{-\hbar^2 }{2M_b}\nabla^2_b) + \frac{-\hbar^2 }{2M_e}\nabla^2_e + (\frac{-q^2}{4\pi \epsilon_0 r_a} + \frac{-q^2}{4\pi \epsilon_0 r_b})+ \frac{q^2}{4\pi \epsilon_0 R_ab}.$

We can then define our TISE as: $\hat{H}\Psi(r,R)=\xi \Psi(r,R)$ such that: 
<p align="center">$(\hat{T}_{nuclear}+\hat{T}_{electron}+\hat{V}_{nuc-e}+\hat{V}_{nuc-nuc})\Psi(r,R)=\xi \Psi(r,R).$</p>

In order to move forward with our finalized Hamiltonian, we will need to separate according to variables and see if this can be simplied further.
To do this let: $\Psi(r,R)=\psi(r;R)\chi(R),$

This enables us to have our equation in the form:
<p align="center">$\hat{T}_{nuclear}(\psi \chi)+\hat{T}_{electron}(\psi \chi)+\hat{V}_{nuc-e}(\psi \chi)+\hat{V}_{nuc-nuc}(\psi \chi)$</p>   <p align="center">$=\xi \psi \chi.$</p>
                                                
After some simple rearranging, we are left with:
$\hat{T}_{nuclear}(\psi \chi)= (\frac{-\hbar^2 }{2M_a}\nabla^2_a + \frac{-\hbar^2 }{2M_b}\nabla^2_b) (\psi \chi) .$
$= \frac{-\hbar^2 }{2M_a}\nabla^2_a(\psi \chi) + \frac{-\hbar^2 }{2M_b}\nabla^2_b(\psi \chi) .$

At this point, we can utilize the Born-Oppenheimer approximation to aid us in simplifying our Hamiltonian. We have already established
that the proton is significantly larger than the electron, and can be treated as such. The entire system for our dihydrogen cation 
is constantly moving in space, where the single electron moves relative to the center of mass for the system. We can then approximate 
that the rate of change of ψ with respect to Ra is insignificant. 

In doing this, we have: 
$\frac{-\hbar^2 }{2M_b}\nabla^2_a(\psi \chi) = \frac{-\hbar^2 }{2M_b}\psi \frac{\partial^2 \chi}{\partial {R_b}^2}$. 
*(Also for nuclei a)* 

This makes our job a lot easier, and after simple algebraic manipulation, we finally arrive at our Hamiltonian:
<p align="center"> $\hat{T}_{nuclear} \chi + \hat{V}_{nuclear} \chi =\xi \chi$.</p>

Deriving this Hamiltonian, we are left with an equation that describes the dynamics for the two nuclei in our system which is our Schrodinger equation using the Born-Oppenheimer approximation. 
The potential energy operator $\hat{V}_{nuclear}$ is a combination of the nucleus - nucleus repulsion and the electron-nucleus attraction.
This shows that the total potential is based on both the potential energy of the nucleus-nucleus interaction in addition to 
the componenets that go into the energy of the electron. *This includes the KE of the electron as well as the PE interactions 
between the nucleus and electron*

Therefore, the potential energy will have the form seen in the well below:

![bondenergy](/bondenergy.GIF)

For many chemistry majors, this is a familiar image. The large divet is the equilibrium bond radius, which has the lowest energy.
This graph is created by fixing the nuclei at a certain, fixed radius while the electron is placed into the system 
where the lowest energy can then be determined. This is incredible! Because we are now able to observe bonding interactions on a quantum level, molecular dynamics can now be explored using quantum mechanics. This is discussed in the next section.

[Next Section: Potential Energy Surfaces](/PES.md)

[Home](/README.md) 
