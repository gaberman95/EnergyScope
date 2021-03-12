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
   * - %\ :sub:`elec`\ (h,td)
     - [-]
     - Yearly time series (adding up to 1) of electricity end-uses
   * - %\ :sub:`sh`\ (h,td)
     - [-]
     - Yearly time series (adding up to 1) of SH end-uses
   * - %\ :sub:`pass`\ (h,td)
     - [-]
     - Yearly time series (adding up to 1) of passenger mobility end-uses
   * - %\ :sub:`fr`\ (h,td)
     - [-]
     - Yearly time series (adding up to 1) of freight mobility end-uses
   * - c\ :sub:`p,t`\ (tech,h,td)
     - [-]
     - Period capacity factor (default 1)



.. list-table:: Table 2: Scenario parameter list with description.
   :widths: 25 18 50
   :header-rows: 1

   * - Parameter
     - Units
     - Description
   * - τ(tech)
     - [-]
     - Investment cost annualization factor
   * - i\ :sub:`rate`\ 
     - [-]
     - Real discount rate
   * - endUses\ :sub:`year`\ (eui, s)
     - [GWh/y]\ :sup:`a`\ 
     - Annual end-uses in energy services per sector
   * - endUsesInput(eui)_
     - [GWh/y]\ :sup:`a`\ 
     - Total annual end-uses in energy services
   * - re\ :sub:`share`\ 
     - [-]
     - minimum share [0;1] of primary RE
   * - gwp\ :sub:`limit`\ 
     - [ktCO\ :sub:`2-eq`\ /y]
     - Higher CO\ :sub:`2-eq`\  emissions limit
   * - %\ :sub:`public,min`\ ; %\ :sub:`public,max`\ 
     - [-] 
     - Lower and upper limit to %\ :sub:`Public`\  
   * - %\ :sub:`rail,min`\ ; %\ :sub:`rail,max`\ 
     - [-]
     - Lower and upper limit to %\ :sub:`Rail`\ 
   * - %\ :sub:`dhn,min`\ ; %\ :sub:`dhn,max`\ 
     - [-] 
     - Lower and upper limit to %\ :sub:`DHN`\ 
   * - t\ :sub:`op`\ (h; td)
     - [h]
     - Time periods duration (default 1h)
   * - f\ :sub:`min`\ ; f\ :sub:`max`\ (tech)
     - [GW]\ :sup:`ab`\ 
     - Min./max. installed size of the technology
   * - f\ :sub:`min,%`\  ; f\ :sub:`max,%`\ (tech)
     - [-]
     - Min./max. relative share of a technology in a layer
   * - avail(res)
     - [GWh/y]
     - Resource yearly total availability
   * - c\ :sub:`op`\ (res)
     - [MCHF/GWh] 
     - Specific cost of resources
   * - η\ :sub:`car,max`\ 
     - [-]
     - Maximum number of cars
   * - %\ :sub:`Peaksh`\  
     - [-]
     - Ratio peak/max. space heating demand in typical days
   * - f(res U tech \ sto,l)
     - [GW]\ :sup:`c`\ 
     - Input from (< 0) or output to (> 0) layers. *f(i; j) = 1* if *j* is main output layer for technology/resource *i*
   * - c\ :sub:`inv`\ (tech)
     - [MCHF/GW]\ :sup:`cb`\ 
     - Technology specific investment cost
   * - c\ :sub:`maint`\ (tech)
     - [MCHF/GW/y]\ :sup:`cb`\ 
     - Technology specific yearly maintenance cost
   * - lifetime(tech)
     - [y]
     - Technology lifetime
   * - gwp\ :sub:`constr`\ (tech)
     - [ktCO\ :sub:`2-eq`\ ./GW]\ :sup:`ab`\ 
     - Technology construction specific GHG emissions
   * - gwp\ :sub:`op`\ (res)
     - [ktCO\ :sub:`2-eq`\ ./GWh]
     - Specific GHG emissions of resources
   * - c\ :sub:`p`\ (tech)
     - [-]
     - Yearly capacity factor
   * - η\ :sub:`sto,in`\ ; η\ :sub:`sto,out`\ (sto; l)
     - [-]
     - Eficiency [0; 1] of storage input from/output to layer. Set to 0 if storage not related to layer.
   * - %\ :sub:`sto,loss`\ (sto)
     - [1/h]
     - Losses in storage (self discharge)
   * - t\ :sub:`sto,in`\ (sto)
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - t\ :sub:`sto,out`\ `\ (sto)
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - %\ :sub:`sto,avail`\ (sto)
     - [-]
     - Storage technology availability to charge/discharge
   * - %\ :sub:`net,loss`\ (eut)
     - [-]
     - Losses coeficient [0; 1] in the networks (grid and DHN)
   * - ev\ :sub:`Batt,size`\ (v2g)
     - [GWh]
     - Battery size per V2G car technology
   * - c\ :sub:`grid,extra`\ 
     - [MCHF]
     - Cost to reinforce the grid due to IRE penetration



* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses
* b[GWh] if *tech* ϵ STO
* c[Mpkm/h] for passenger, [Mtkm/h] for freight mobility end-uses


.. list-table:: Table 3: Independent variable list with description. All variables are continuous and nonnegative, unless otherwise indicated.
   :widths: 25 18 50
   :header-rows: 1

   * - Variable
     - Units
     - Description
   * - %\ :sub:`Public`\ 
     - [-]
     - Ratio [0; 1] public mobility over total passenger mobility
   * - %\ :sub:`Rail`\ 
     - [-]
     - Ratio [0; 1] rail transport over total freight transport
   * - %\ :sub:`DHN`\ 
     - [-]
     - Ratio [0; 1] centralized over total low-temperature heat
   * - F(tech)
     - [GW]\ :sup:`ab`\ 
     - Installed capacity with respect to main output
   * - F\ :sub:`t`\ (tech U res,h,td)
     - [GW]\ :sup:`ab`\ 
     - Operation in each period
   * - Sto\ :sub:`in`\ ; Sto\ :sub:`out`\ (sto,l,h,td)
     - [GW]
     - Input to/output from storage units
   * - P\ :sub:`Nuc`\ 
     - [GW]
     - Constant load of nuclear
   * - %\ :sub:`MobPass`\ (TECH OF EUC(MobPass))
     - [-]
     - Constant share of passengers mobility
   * - %\ :sub:`HeatDec`\ HeatDec(TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [-]
     - Constant share of Heat low T decentralised supplied by a technology plus its associated thermal solar and storage
   * - F\ :sub:`sol`\ (TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [GW]
     - Solar thermal installed capacity associated to a decentralised heating technology
   * - F\ :sub:`tsol`\ (TECH OF EUT((HeatLowTDEC) \ {DecSolar})
     - [GW]
     - Solar thermal operation in each period
     

* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses 
* b[GWh] if *tech* ϵ STO


.. list-table:: Table 4: Dependent variable list with description. All variables are continuous and non-negative, unless otherwise indicated.
   :widths: 25 18 50
   :header-rows: 1

   * - Variable
     - Units
     - Description
   * - EndUses(l,h,td)
     - [GW]\ :sup:`a`\  
     - End-uses demand. Set to 0 if l ∉ EUT
   * - C\ :sub:`tot`\ 
     - [MCHF/y]
     - Total annual cost of the energy system
   * - C\ :sub:`inv`\ 
     - [MCHF]
     - Technology total investment cost
   * - C\ :sub:`maint`\ (tech)
     - [MCHF/y]
     - Technology yearly maintenance cost
   * - C\ :sub:`op`\ (res)
     - [MCHF/y]
     - Total cost of resources
   * - GWP\ :sub:`tot`\ 
     - [ktCO\ :sub:`2-eq`\ ./y]
     - Total yearly GHG emlissions of the energy system
   * - GWP\ :sub:`constr`\ (tech)
     - [ktCO\ :sub:`2-eq`\ .]
     - Technology construction GHG emissions
   * - GWP\ :sub:`op`\ (res)
     - [ktCO\ :sub:`2-eq`\ ./y]
     - Total GHG emissions of resources
   * - Net\ :sub:`loss`\ (eut,h,td)
     - [GW]
     - Losses in the networks (grid and DHN)
   * - Sto\ :sub:`level`\ (sto,t)
     - [GWh]
     - Energy stored over the year


* a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses

