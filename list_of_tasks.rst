
List of tasks
==================================

You can chose to work with the pre-filled notebook, or write the code on your own. There are no restrictions.

As a rule of thumb, for testing, make a system that is about at least 5 (not more than 10, speed issues) times the wire length in width and length, and at about a scale-free density :math:`n=N l_w^2 / [L\cdot W]` of more than than 30, but less than a 100. So for a wire of length 10, have a system of size 50x50, with about 50/10*50/10*40 = 1000 wires (scale free density = 40).




First task - Warmup : volatility of the data and finite size problems.
----------

* Create a sample of size 50x50, wire length 10, 1500 wires. Linear resistance 1.59 (silver), radius 0.03, contact resistance 100.
   * Calculate the scale-free density of this system
   * Calculate how many times it exceeds the critical density for percolation (:math:`n=5.63`)
   * Create about the sample again about a 100 times and calculate its resistance every time. Estimate its standard deviation of the resistance.
   * Compare this resistance to the resistance of a sample twice as large, twice as wide, with 4 times as many wires
   * The sizes are in units of microns. How can you use the above result if you want to simulate the resistance of a real sample, which is 2 cm long and .5 mm wide, with the same density (think in terms of resistance of a square) ? Do you think you could simulate the real sample (estimate the number of wires in such a sample, and point out what the problem would be for the computer to perform the simulation).


Second task - Warmup : Detective work #1.
----------

* For the same sample (50,50,10,1500), find out how many contacts each wire has. The t_and_u matrix contains this information (functions). How does this compare to http://iopscience.iop.org/article/10.1088/0957-4484/22/34/345703/pdf equation (21) (:math:`P_{cont}` is calculated before as 0.2027)? Keep in mind that the paper defines :math:`\langle N_{ref} \rangle` as the number of wires inside an area of :math:`S_{ref} = \pi l_w^2`. Hint: The number of wires in the reference area is the true density (not scale-free) of wires (wires per area) times the reference area.
   * From the same paper, take figure 5a). On the x-axis, :math:`D_ol_w^2` means that they have :math:`x\cdot pi` wires in a reference area. Long story short, after a bit of computation, their data point at x=10 corresponds in this case to a network of 250 wires (wire length = 10, size=50x50). Generate the network a 1000 times and calculate the standard deviation of the probability of contact (number of contacts per wire divided by the number of wires in the reference area). Do you trust the error bars on this plot ?
   * Bonus: where do you think the slight deviation between your simulation results and theirs come from?

Third  task - Will be graded : Detective work #2.
----------

An area of investigation is to find an expression of the equivalent resistance :math:`R_{eq}` of this kind of mixed resistor networks i.e conducting wires with an intrinsic resistance and contact resistances. We will investigate the validity of a proposed model published in Physical Review Letters B (a good journal): http://journals.aps.org/prb/pdf/10.1103/PhysRevB.86.134202 . This kind of network, at low densities, has a resistance which behaves like a power-law (percolation theory). However, at very high densities, the percolation theory is not valid anymore (far away from the critical density for percolation), and an alternative, more simple formula should explain the behavior. The claim is the following

.. math::

   \sigma_{low~density} &= (n-n_c)^t & \quad \quad  \text{undisputed result}\\
   \sigma_{high~density} & \sim \frac{1}{bn^{-1}/G_s + n^{-2}/G_c} & \quad \quad \text{their contribution}\\
   \sigma_{combined} &= a\frac{ \left(n-n_c\right)^t }{bn^{t-1}/G_s + \left(n+n_c\right)^{t-2}/G_c} & \quad \quad \text{bringing both in 1 formula}

where :math:`G_s` is the conductivity of the wires (stick) and :math:`G_c` is the conductivity of the conctacts, :math:`n` the scale-free density, :math:`n_c` the critical percolation density (:math:`n_c` =5.63), and :math:`a,b,t` are fitting parameters. Figures 5 and 6 of the paper show a good agreement between the combined formula :math:`\sigma_{combined}` and their simulations.

* Create a sample of size 50x50 :math:`\mu m^2`, wire length 10 :math:`\mu m`, scale free densities ranging from :math:`n \in [30,35,\ldots,100]`. and contact resistance :math:`R_c = 100 [\Omega]`, linear resistance 1.59 :math:`[10^{-2}\cdot \Omega \mu m]` and wire radius 0.03 :math:`[\mu m]` (meaning :math:`R_s = 56.3 [\Omega]`). Calculate for every sample the equivalent resistance :math:`R_{eq} \equiv \frac{1}{\sigma_{eq}}` (only once is enough, no need for statistcs). According to their figures, this represents a high density system. Fit the data with :math:`R_{eq}(a,b,n,R_c=100,R_s=56.3) = \left[\frac{a}{bn^{-1}R_s + n^{-2}Rc}\right]^{-1}` which is the high-density formula of the paper. Retrieve the fit parameters :math:`a_{fit},b_{fit}`. Simulate data again with with :math:`n=50` but now vary the contact resistance :math:`R_c \in 10^{\left[-6,-5,\ldots,5,6\right]}`. **Will be graded:** Plot the ratio of this new data over :math:`R_{eq}(a_{fit},b_{fit},50,R_c,R_s=56.3)` in function of :math:`R_c`. Indicate the value of the parameters :math:`a_{fit},b_{fit}` on the plot.


