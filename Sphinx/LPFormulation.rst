.. _LPFormulation:

Model formulation
=================

The energy system is formulated as a linear programming (LP) problem. It optimises the design by computing the installed capacity of each technology, as well as the operation in each period, to meet the energy demand and minimize the total annual cost of the system. In the following, we present the complete formulation of the model. It accounts for sets, parameters, variables, constraints and the objective function. The model formulation is expressed by the equations in Figure 4 and Eqs. (1)-(42).

End-use demand
^^^^^^^^^^^^^^

We use the end-use demand (EUD) instead of the final energy consumption (FEC) to characterise the demand. According to the definition of the European commission, FEC is defined as *"the energy which reaches the final consumer's door"* [3]_. In other words, the FEC is the amount of input fuel needed to satisfy the EUD in energy services. As an example, in the case of decentralized heat production with a gas boiler, the FEC is the amount of NG consumed by the boiler; the EUD is the amount of heat produced by the boiler, i.e. the heating service needed by the final user. This modelling choice has two advantages. First, it introduces a clear distinction between demand and supply. On the one hand, the demand concerns the definition of the end-uses, i.e. the requirements in energy services (e.g. the mobility needs). On the other hand, the supply concerns the choice of the energy conversion technologies to supply these services (e.g. the types of vehicles used to satisfy the mobility needs). Based on the technology choice, the same EUD can be satisfied with different FEC, depending on the efficiency of the chosen energy conversion technology. Second, it facilitates the inclusion in the model of electric technologies for heating and transportation.
The hourly end-use demand (**EndUses**) is computed based on the yearly end-use demand (*endUsesInput*), distributed according to a normalised time series.

.. image:: images/EndUseDemand.PNG

Figure 4: **EndUses** calculation starting from yearly demand model inputs (*endUsesInput*). Adapted from [6]_. Abbreviations: space heating (sh), district heating network (DHN), hot water (HW), passenger (pass) and freight (fr).

Figure 4 graphically presents the constraints associated to the hourly end use demand (**EndUses**), e.g. the public mobility demand at time t is equal to the hourly passenger mobility demand times the public mobility share (**%\ :sub:`Public`\ **).
Electricity end-uses result from the sum of the electricity-only demand, assumed constant throughout the year, and the variable demand of electricity, distributed across the periods according to ** %\ :sub:`elec.`\ **. Low-temperature heat demand results from the sum of the yearly demand for hot water (HW), evenly shared across the year, and space heating (SH), distributed across the periods according to **%\ :sub:`sh`\ **.
The percentage repartition between centralized (DHN) and decentralized heat demand is defined by the variable **%\ :sub:`DHN`\ **. High temperature process heat and mobility demand are evenly distributed across the periods. Passenger mobility demand is expressed in passenger-kilometers (pkms), freight transportation demand is in ton-kilometers (tkms). The variables **%\ :sub:`Public`\ ** and **%\ :sub:`Rail`\ ** define the penetration of public transportation in passenger mobility and of train in freight, respectively.


Cost, emissions and objective function
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The objective Eq. (1) is the minimisation of the total annual cost of the energy system (**C\ :sub:`tot`\ **), defined as the sum of the annualized investment cost of technologies (τ**C\ :sub:`inv`\ **), the operating and maintenance cost of technologies (**C\ :sub:`maint`\ **) and the operating cost of the resources (**C\ :sub:`op`\ **). The total investment cost (**C\ :sub:`inv`\ ** ) of each technology results from the multiplication of its specific investment cost (** c\ :sub:`inv`\ **) and its installed size (**F**), the latter defined with respect to the main end-uses output type Eq. (3). ** C\ :sub:`inv`\  **is annualised with the factor τ , calculated based on the interest rate (**i\ :sub:`rate`\ **) and the technology lifetime (*lifetime*) Eq. (2). The total operation and maintenance cost is calculated in the same way Eq. (4). The total cost of the resources is calculated as the sum of the end-use over different periods multiplied by the period duration (**t\ :sub:`op`\ **) and the specific cost of the resource (**c\ :sub:`op`\ **) Eq. (5). Note that, in Eq. (5), summing over the typical days using the set T_H_TD is equivalent to summing over the 8760h of the year.


.. math::
	min  \mathbf{C_{tot}} = \sum_{j\in TECH}^{} (\tau (j)\mathbf{C_{inv}}(j) + \mathbf{C_{maint}}(j)) + \sum_{i \in RES}^{} \mathbf{C_{op}}(i)	(1)

.. math::
	s.t \; \; \;\tau (j) = \frac{i_{rate}*(i_{rate}+1)^{lifetime(j))}}{(i_{rate}+1)^{lifetime(j)-1)}}\; \; \; \forall j \in TECH	(2)

.. math::
	\mathbf{C_{inv}}(j) = c_{inv}(j)*\mathbf{F}(j)\; \; \; \forall j \in TECH (3)

.. math::
	\mathbf{C_{maint}}(j) = c_{maint}(j)*\mathbf{F}(j)\; \; \; \forall j \in TECH (4)

.. math::
	\mathbf{C_{op}}(i)=\sum_{t\in T\mid \left \{h,td  \right \}\in  THTD(t)}^{} c_{op}(i)*\mathbf{F_{t}}(i,h,td)t_{op}(h,td)\; \; \; \forall i \in RES (5)


The global annual greenhouse gas (GHG) emissions are calculated using a life cycle assessment (LCA) approach, i.e. taking into account emissions of technologies and resources \from cradle to grave". For climate change, the natural choice as indicator is the global warming potential (**GWP**), expressed in ktCO2-eq./year. In Eq. (6), the total yearly emissions of the system (GWPtot) are defined as the sum of the emissions related to the construction and end-of-life of the energy conversion technologies (**GWPconstr**), allocated to one year based on the technology lifetime (*lifetime*), and the emissions related to resources (**GWPop**). Similarly to the costs, the total emissions related to the construction of technologies are the product of the specific emissions (*gwpconstr*) and the installed size (**F**), Eq. (7). The total emissions of resources are the emissions associated to fuels (from cradle to combustion) and imports of electricity (*gwpop*) multiplied by the period duration (*top*) (Eq 8).

.. math::
	\mathbf{GWP_{tot}}= \sum_{j\in TECH}^{}\frac{\mathbf{GWP_{constr}}(j)} {lifetime(j))} +\sum_{i\in RES}^{} \mathbf{GWP_{op}}(i) (6)

.. math::
	\mathbf{GWP_{constr}}(j)=gwp_{constr}(j)\mathbf{F}(j)\; \; \; \forall j\in TECH (7)

.. math::
	\mathbf{GWP_{op}}(i)=\sum_{t\in \mid T\left \{ h,td \right \}\in THTD(t))}^{} gwp_{op}(i)\mathbf{F_{t}}(i,h,td)t_{op}(h,td)\; \; \; \forall i\in RES (8)

System design and operation
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The installed capacity of technologies (**F**) is constrained between upper and lower bounds (*fmax* and *fmin*), Eq. (9). This formulation allows accounting for old technologies still existing in the target year (lower bound), but also for the maximum deployment potential of a technology. As an example, for hydroelectric power plants, *fmin* represents the existing installed capacity (which will still be available in the future), while *fmax* represents the maximum potential.

.. math::
	f_{min}(j)\leq \mathbf{F}(j)\leq f_{max}(j)\; \; \; \forall j\in TECH (9)


The operation of resources and technologies in each period is determined by the decision variable **Ft**. The capacity factor of technologies is conceptually divided into two components: a capacity factor for each period (*cp,t*) depending on resource availability (e.g. renewables) and a yearly capacity factor (*cp*) accounting for technology downtime and maintenance. For a given technology, the definition of only one of these two is needed, the other one being fixed to the default value of 1. Eqs. (10) and (11) link the installed size of a technology to its actual use in each period (Ft) via the two capacity factors. The total use of resources is limited by the yearly availability (*avail*), Eq. (12).

.. math::
	\mathbf{F_{t}}(j,h,td)\leq \mathbf{F}(j)c_{p,t}(j,h,td)\; \; \; \forall j\in TECH, \forall h\in H,\forall td\in TD (10)

.. math:: 
	\sum_{t\in T\mid \left \{h,td  \right \}\in  THTD(t)}^{}\mathbf{F_{t}}(j,h,td)t_{op}(h,td)\leq \mathbf{F}(j)c_{p}(j)\sum_{t\in T\mid \left \{h,td  \right \}\in  THTD(t)}^{}t_{op}(h,td)\; \; \; \forall j\in TECH (11)

.. math::
	\sum_{t\in T\mid \left \{h,td  \right \}\in  THTD(t)}^{}\mathbf{F_{t}}(i,h,td)t_{op}(h,td)\leq avail(i) \; \; \; \forall i\in RES (12)

The matrix *f* defines for all technologies and resources outputs to (positive) and inputs (negative) layers. Eq. (13) expresses the balance for each layer: all outputs from resources and technologies (including storage) are used to satisfy the EUD or as inputs to other resources and technologies.	

.. math::
	\sum_{i\in RES \cup TECH\setminus STO}^{}f(i,l)\mathbf{F_{t}}(i,h,td) +\sum_{j\in STO}^{} (\mathbf{STO_{out}}(j,l,h,td)-\mathbf{STO_{in}}(j,l,h,td))-\mathbf{EndUses}(l,h,td)=0\; \; \; \forall l\in L,\forall h\in H,\forall td\in TD (13)

Storage
^^^^^^^

The storage level (**Stolevel**) at a time step (*t*) is equal to the storage level at *t*-1 (accounting for the losses in *t*-1), plus the inputs to the storage, minus the output from the storage (accounting for input/output efficiencies (14) ). The storage systems which can only be used for short-term (daily) applications are included in the STO DAILY set. For these units, Eq. (15) imposes that the storage level be the same at the end of each typical day. Adding this constraint drastically reduces the computational time. For the other storage technologies, which can also be used for seasonal storage, the capacity is bounded by Eq (16). For these units, the storage behaviour is thus optimized over 8760h, as explained in the methodology Section of the paper.

.. math::
	\mathbf{Sto_{level}}(j,t)= \mathbf{Sto_{level}}(j,t-1)\cdot (1-%_{sto_{loss}}(j))+ t_{op}(h,td)\cdot (\sum_{l\in L\mid \eta _{sto,in(j,l)> 0)}}^{}\mathbf{Sto_{in}}(j,l,h,td)\eta _{sto,in}(j,l)-\sum_{l\in L\mid \eta _{sto,out(j,l)> 0)}}^{}\mathbf{Sto_{out}}(j,l,h,td)\eta _{sto,out}(j,l))\; \; \; \forall j\in STO, \forall t\in T\mid \left \{ h,td \right \}\in THTD(t) (14)

.. math::
	\mathbf{Sto_{level}}(j,t)=\mathbf{F_{t}}(j,h,td)\; \; \; \forall j\in STO DAILY, \forall t\in T\mid \left \{ h,td \right \}\in THTD(t) (15)

.. math::
	\mathbf{Sto_{level}}(j,t)=\mathbf{F}(j)\; \; \; \forall j\in STO \setminus STO DAILY, \forall t\in T (16)

Eqs. (17)-(18) force the power input and output to zero if the layer is incompatible. As an example, a PHS will only be linked to the electricity layer (input/output efficiencies > 0). All other efficiencies will be equal to 0, to impede that the PHS exchanges with incompatible layers (e.g. mobility, heat, etc). Eq. (19) limits the power input/output of a storage technology based on its installed capacity (**F**) and three specific characteristics. First, storage availability (*%stoavail*) is defined as the ratio between the available storage capacity and the total installed capacity (default value is 1). This parameter is required to realistically represent V2G, for which we assume that only a fraction of the fleet can charge/discharge at the same time. Second and third, the charging/discharging time (*tstoin , tstoout* ), which are the time to complete a full charge/discharge from empty/full storage5. As an example, a daily thermal storage can be fully discharged in minimum 4 hours (*tstoout* = 4[h]), and fully charged in maximum 4 hours (*tstoin* = 4[h]).

.. math::
	\mathbf{Sto_{in}}(j,l,h,td)\cdot (\left \lceil \eta _{sto,in}(j,l) \right \rceil -1)=0\; \; \; \forall j\in STO,\forall l\in L,\forall h\in H, \forall td\in TD (17)

.. math::
	\mathbf{Sto_{out}}(j,l,h,td)\cdot (\left \lceil \eta _{sto,out}(j,l) \right \rceil -1)=0\; \; \; \forall j\in STO,\forall l\in L,\forall h\in H, \forall td\in TD (18)

.. math::
	(\mathbf{Sto_{in}}(j,l,h,td)t_{sto_{in}}(j)-\mathbf{Sto_{out}}(j,l,h,td)t_{sto_{out}}(j))\leq \mathbf{F}(j)%_{sto_{avail}}(j)\; \; \; \forall j\in STO,\forall l\in L,\forall h\in H, \forall td\in TD (19)

