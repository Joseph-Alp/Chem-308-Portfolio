{% include mathjax.html %}

# Potential Energy Surfaces 

Because we are now able to observe bonding interactions on a quantum level, molecular dynamics can now be explored using quantum mechanics. We are now able to close out our semester long course by incorporating all we have learned into exploring molecular dynamics for a given particle(s) using the chemical equation: $$A + BC \rightarrow AB + C$$

Simulations based on quantum molecular dynamics make it possible to view experimental activity as it happens. We have seen the short comings of Classical Physics when trying to describe quantum mechanics throughout this course. To recap: Quantum molecular dynamics is  different from classical molecular dynamics, which is primarily concerned with the classical motion of atoms interacting with a given potential. We are interested in the subatomic activities occuring with a compound, where Newtn's Classical Laws do not fully explain what we are witnessing. Therefore, we can design a Matlab program that allows us to observe these subatomic interactions by observing the energy barriers a particle must overcome in order for $$A + BC \rightarrow AB + C$$ to take place. This reaction was studied using three different surfaces that represent different conditions; the first being an early barrier.


# Early Energy Barrier

![early barrier image](/EarlyBarrier.png)

(*Source: MjC*)

An early barrier models the exothermic reaction taking place where the energy of the reactants are higher than the products. Despite being exothermic by its own nature, the reaction is not guarateed to happen. This is because a certain amount of energy is needed to get over the *"saddle point."* In this case, the saddle point is shifted to the right, as seen in the left graph. The right graph shows how the "slices" of the surface are the same as the potential well of binding for the products.


# Late Energy Barrier 

![late barrier image](/LateBarrier.png)
(*Source: MjC*)

This graph displays an endothermic reaction, as noted by the energy of the reactants being lower than the energy of the products.  The reaction will only occur if enough kinetic energy is applied to the system to get it over the "saddle point." On the left, we see that the saddle point is shifted to the left. The right graph shows a "slice" of the surface to show the potential energy well of the products.


# Lennard-Jones Potential

The third type of graph centers around the Lennard-Jones Potential, which describes the potential energy of interaction between two non-bonding atoms or molecules based on their distance of separation. The Lennard-Jones potential equation accounts for the difference between attractive forces (such as dipole-dipole, dipole-induced dipole, and London interactions) and repulsive forces. The potential can be expressed in the follow equation: *$V_{LJ} = 4 \epsilon ((\frac {\sigma}{r})^{12}-(\frac {\sigma}{r})^6)$,*

In this equation, $\epsilon$ notates well depth, $\sigma$ represents the distance at which the intermolecular potential between the two particles is zero; $r$ is the distance between particles (measured from the center of one particle to the center of the other particle). 

This well represents the reaction of non-reactive species (i.e. noble gases). As the variable in the equation state, the potential takes into account the attractive and repulsive forces of the particles which can be seen at the very end of this section.

# Tinkering With Early Surface Barrier

The first instance of an early surface barrier explored centered around the exothermic reaction not occuring. 

![ESGIF](/EBNoRxn.gif)

We witness the AB molecule *almost* separating where the reaction loiters around the saddle point. The top left animation at the saddle point has atoms A and C appearing to vibrate with atom C at the same frequency, indicating that a possible reaction may happen). However, it does not; there is not enough energy to get over the saddle point. 

The second instance of an early surface barrier explored has the exothermic reaction taking place.

![complete](/EBRxnOccurs.gif)

We know this reaction actually takes place by the AB molecule separating entirely. Additionally, the BC molecule is generated with A no longer bound to the reactant. We see the reaction has enough energy to overcome the saddle point, where the total energy of the BC molecule is lower than the starting material of AB.


# Tinkering With Late Surface Barrier

Just as we saw with the first case of the early surface barrier, the reaction does not take place as there is not enough energy to overcome the saddle point. 

![image](/LBNoRxn.gif)

However, if we were to increase the energy such that it overcome the saddle point, then the reaction would take place.

# Lennard-Jones Potential Barrier

As we would expect, the overall reaction does not occur with the Lennard-Jones potential. This well represents the reaction of non-reactive species (i.e. noble gases), that otherwise would *not* be reactive. As a result, no amount of PE can overcome the unfavorable reaction conditions; cauting there to be no reaction.

![LJagain](/LJPot.gif)


# Working With The Molecular Dynamics Code

The code(s) for working with the early, late, and LJ potentials are all provided on the home page; several important features should be kept in mind:
* The early barrier examples were generated by modifying the initial velocities of AB and BC
* The later barrier examples were generated by decreasing the initial velocities
* Tinkering with the initial positions will also make for good exploratory fun to see if the saddle point can be overcome

*(All animations taken from code generated by Professor Matt Cote)*




