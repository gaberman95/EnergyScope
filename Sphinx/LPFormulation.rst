.. _LPFormulation:

Linear Programming model formulation
====================================

The energy system is formulated as a linear programming (LP) problem. It optimises the design by computing the installed capacity of each technology, as well as the operation in each period, to meet the energy demand and minimize the total annual cost of the system. In the following, we present the complete formulation of the model. It accounts for sets, parameters, variables, constraints and the objective function. The model formulation is expressed by the equations in Figure 4 and Eqs. (1)-(42).

End-use demand
--------------

We use the end-use demand (EUD) instead of the final energy consumption (FEC) to characterise the demand. According to the definition of the European commission, FEC is defined as *"the energy which reaches the final consumer's door"* [3]_. In other words, the FEC is the amount of input fuel needed to satisfy the EUD in energy services. As an example, in the case of decentralized heat production with a gas boiler, the FEC is the amount of NG consumed by the boiler; the EUD is the amount of heat produced by the boiler, i.e. the heating service needed by the final user. This modelling choice has two advantages. First, it introduces a clear distinction between demand and supply. On the one hand, the demand concerns the definition of the end-uses, i.e. the requirements in energy services (e.g. the mobility needs). On the other hand, the supply concerns the choice of the energy conversion technologies to supply these services (e.g. the types of vehicles used to satisfy the mobility needs). Based on the technology choice, the same EUD can be satisfied with different FEC, depending on the efficiency of the chosen energy conversion technology. Second, it facilitates the inclusion in the model of electric technologies for heating and transportation.
The hourly end-use demand (**EndUses**) is computed based on the yearly end-use demand (*endUsesInput*), distributed according to a normalised time series.

.. image:: images/EndUseDemand.PNG

Figure 4: **EndUses** calculation starting from yearly demand model inputs (endUsesInput). Adapted from [6]_. Abbreviations: space heating (sh), district heating network (DHN), hot water (HW), passenger (pass) and freight (fr).

Figure 4 graphically presents the constraints associated to the hourly end use demand (**EndUses**), e.g. the public mobility demand at time t is equal to the hourly passenger mobility demand times the public mobility share (**%Public**).
Electricity end-uses result from the sum of the electricity-only demand, assumed constant throughout the year, and the variable demand of electricity, distributed across the periods according to %*elec*. Low-temperature heat demand results from the sum of the yearly demand for hot water (HW), evenly shared across the year, and space heating (SH), distributed across the periods according to %*sh* .
The percentage repartition between centralized (DHN) and decentralized heat demand is defined by the variable **%DHN**. High temperature process heat and mobility demand are evenly distributed across the periods. Passenger mobility demand is expressed in passenger-kilometers (pkms), freight transportation demand is in ton-kilometers (tkms). The variables **%Public** and **%Rail** define the penetration of public transportation in passenger mobility and of train in freight, respectively.


Cost, emissions and objective function
--------------------------------------

The objective Eq. (1) is the minimisation of the total annual cost of the energy system (**Ctot**), defined as the sum of the annualized investment cost of technologies (τ **Cinv**), the operating and maintenance cost of technologies (**Cmaint**) and the operating cost of the resources (**Cop**). The total investment cost (Cinv) of each technology results from the multiplication of its specific investment cost (*cinv*) and its installed size (F), the latter defined with respect to the main end-uses output type Eq. (3). Cinv is annualised with the factor τ , calculated based on the interest rate (*irate*) and the technology lifetime (*lifetime*) Eq. (2). The total operation and maintenance cost is calculated in the same way Eq. (4). The total cost of the resources is calculated as the sum of the end-use over different periods multiplied by the period duration (*top*) and the specific cost of the resource (*cop*) Eq. (5). Note that, in Eq. (5), summing over the typical days using the set T_H_TD is equivalent to summing over the 8760h of the year.


.. math::
	10_{6}		(1)
