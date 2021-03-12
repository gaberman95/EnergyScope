.. _Sets: 

Sets, parameters and variables
==============================

Figure 3 gives a visual representation of the sets with their relative indices used throughout the
paper.
In order to solve a yearly problem over 8760h, we define the sets H_OF_T(t), TD_OF_T(t) and T_H_TD(t) that give respectively, the hour (h), the typical day (td) or both (h,td) based on the period (t). E.g. if January 2 is associated to typical day 1, then H_OF_T(34) = 10,  TD_OF_T(t) = 1 and T_H_TD(34) ={h = 10; td = 1}.
Tables 1 and 2 list and describe the model parameters. Tables 3 and 4 list and describe the independent and dependent variables, respectively.

.. image:: images/Sets.PNG

Figure 3: Visual representation of the sets and indices of the LP framework. Abbreviations: space heating (SH), hot water (HW), temperature (T), mobility (MOB), vehicle-to-grid (V2G), thermal storage (TS).


.. list-table:: Table 1: Time series parameter list with description. Set indices as in Figure 3
   :widths: 25 10 40
   :header-rows: 1

   * - Parameter
     - Units
     - Description
   * - %elec(h,td)
     - [-]
     - Yearly time series (adding up to 1) of electricity end-uses
   * - %sh(h,td)
     - [-]
     - Yearly time series (adding up to 1) of SH end-uses
   * - %pass(h,td)
     - [-]
     - Yearly time series (adding up to 1) of passenger mobility end-uses
   * - %fr(h,td)
     - [-]
     - Yearly time series (adding up to 1) of freight mobility end-uses
   * - cp,t(tech,h,td)
     - [-]
     - Period capacity factor (default 1)



.. list-table:: Table 2: Scenario parameter list with description.
   :widths: 25 15 50
   :header-rows: 1

   * - Parameter
     - Units
     - Description
   * - τ(tech)
     - [-]
     - Investment cost annualization factor
   * - irate
     - [-]
     - Real discount rate
   * - endUsesyear(eui, s)
     - [GWh/y]a
     - Annual end-uses in energy services per sector
   * - endUsesInput(eui)_
     - [GWh/y]a
     - Total annual end-uses in energy services
   * - reshare
     - [-]
     - minimum share [0;1] of primary RE
   * - gwplimit
     - [ktCO2-eq/y]
     - Higher CO2-eq emissions limit
   * - %public,min; %public,max
     - [-] 
     - Lower and upper limit to %Public
   * - %rail,min; %rail,max
     - [-]
     - Lower and upper limit to %Rail
   * - %dhn,min; %dhn,max
     - [-] 
     - Lower and upper limit to %DHN
   * - top(h; td)
     - [h]
     - Time periods duration (default 1h)
   * - fmin; fmax(tech)
     - [GW]ab
     - Min./max. installed size of the technology
   * - fmin,% ; fmax,%(tech)
     - [-]
     - Min./max. relative share of a technology in a layer
   * - avail(res)
     - [GWh/y]
     - Resource yearly total availability
   * - cop(res)
     - [MCHF/GWh] 
     - Specific cost of resources
   * - ηcar,max
     - [-]
     - Maximum number of cars
   * - %Peaksh 
     - [-]
     - Ratio peak/max. space heating demand in typical days
   * - f(res U tech \ sto,l)
     - [GW]c 
     - Input from (< 0) or output to (> 0) layers. f(i; j) = 1
   * - cinv(tech)
     - [MCHF/GW]cb
     - Technology specific investment cost
   * - cmaint(tech)
     - [MCHF/GW/y]cb
     - Technology specific yearly maintenance cost
   * - lifetime(tech)
     - [y]
     - Technology lifetime
   * - gwpconstr(tech)
     - [ktCO2-eq./GW]ab
     - Technology construction specific GHG emissions
   * - gwpop(res)
     - [ktCO2-eq./GWh]
     - Specific GHG emissions of resources
   * - cp(tech)
     - [-]
     - Yearly capacity factor
   * - ηsto,in ; ηsto,out(sto; l)
     - [-]
     - Eficiency [0; 1] of storage input from/output to layer. Set to 0 if storage not related to layer.
   * - %stoloss(sto)
     - [1/h]
     - Losses in storage (self discharge)
   * - tstoin(sto)
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - tstoout(sto)
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - %stoavail(sto)
     - [-]
     - Storage technology availability to charge/discharge
   * - %netloss(eut)
     - [-]
     - Losses coeficient [0; 1] in the networks (grid and DHN)
   * - evBatt,size(v2g)
     - [GWh]
     - Battery size per V2G car technology
   * - cgrid;extra
     - [MCHF]
     - Cost to reinforce the grid due to IRE penetration



* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses
* b[GWh] if tech ϵ STO
* c[Mpkm/h] for passenger, [Mtkm/h] for freight mobility end-uses


.. list-table:: Table 3: Independent variable list with description. All variables are continuous and nonnegative, unless otherwise indicated.
   :widths: 25 15 50
   :header-rows: 1

   * - Variable
     - Units
     - Description
   * - %Public
     - [-]
     - Ratio [0; 1] public mobility over total passenger mobility
   * - %Rail
     - [-]
     - Ratio [0; 1] rail transport over total freight transport
   * - %DHN
     - [-]
     - Ratio [0; 1] centralized over total low-temperature heat
   * - F(tech)
     - [GW]ab
     - Installed capacity with respect to main output
   * - Ft(tech U res,h,td)
     - [GW]ab
     - Operation in each period
   * - Stoin; Stoout(sto,l,h,td)
     - [GW]
     - Input to/output from storage units
   * - PNuc
     - [GW]
     - Constant load of nuclear
   * - %MobPass(TECH OF EUC(MobPass))
     - [-]
     - Constant share of passengers mobility
   * - %HeatDec(TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [-]
     - Constant share of Heat low T decentralised supplied by a technology plus its associated thermal solar and storage
   * - Fsol(TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [GW]
     - Solar thermal installed capacity associated to a decentralised heating technology
   * - Ftsol(TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [GW]
     - Solar thermal operation in each period
     

* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses 
* b[GWh] if tech ϵ STO


.. list-table:: Table 4: Dependent variable list with description. All variables are continuous and non-negative, unless otherwise indicated.
   :widths: 25 15 50
   :header-rows: 1

   * - Variable
     - Units
     - Description
   * - EndUses(l,h,td)
     - [GW]a 
     - End-uses demand. Set to 0 if l ∉ EUT
   * - Ctot
     - [MCHF/y]
     - Total annual cost of the energy system
   * - Cmaint(tech)
     - [MCHF/y]
     - Technology yearly maintenance cost
   * - Cop(res)
     - [MCHF/y]
     - Total cost of resources
   * - GWPtot
     - [ktCO2-eq./y]
     - Total yearly GHG emlissions of the energy system
   * - GWPconstr(tech)
     - [ktCO2-eq.]
     - Technology construction GHG emissions
   * - GWPop(res)
     - [ktCO2-eq./y]
     - Total GHG emissions of resources
   * - Netloss(eut,h,td)
     - [GW]
     - Losses in the networks (grid and DHN)
   * - Stolevel(sto,t)
     - [GWh]
     - Energy stored over the year


* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses

:math: C_{top}