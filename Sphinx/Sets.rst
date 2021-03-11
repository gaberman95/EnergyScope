.. _Sets: 

Sets, parameters and variables
==============================

Figure 3 gives a visual representation of the sets with their relative indices used throughout the
paper.
In order to solve a yearly problem over 8760h, we define the sets H_OF_T(t), TD_OF_T(t) and T_H_TD(t) that give respectively, the hour (h), the typical day (td) or both (h,td) based on the period (t). E.g. if January 2 is associated to typical day 1, then H_OF_T(34) = 10, TD_OF_T(t) = 1 and T_H_TD(34) ={h = 10; td = 1}.
Tables 1 and 2 list and describe the model parameters. Tables 3 and 4 list and describe the independent and dependent variables, respectively.

.. image:: images/Sets.PNG

Figure 3: Visual representation of the sets and indices of the LP framework. Abbreviations: space heating (SH), hot water (HW), temperature (T), mobility (MOB), vehicle-to-grid (V2G), thermal storage (TS).


.. list-table:: Table 1: Time series parameter list with description. Set indices as in Figure 3
   :widths: 25 10 50
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


.. list-table:: Table 2: Scenario parameter list with description. Set indices as in Figure 3
   :widths: 25 10 50
   :header-rows: 1

   * - Parameter
   	 - Units
   	 - Description
   * - _τ(tech)_
     - [-]
     - Investment cost annualization factor
   * - _irate_
     - [-]
     - Real discount rate
   * - _endUsesyear(eui, s)_
     - [GWh/y]a
     - Annual end-uses in energy services per sector
   * - _endUsesInput(eui)_
     - [GWh/y]a
     - Total annual end-uses in energy services
   * - _reshare_
     - [-]
     - minimum share [0;1] of primary RE
   * - _gwplimit_
     - [ktCO2-eq/y]
     - Higher CO2-eq emissions limit
   * - _%public,min; %public,max_
     - [-] 
     - Lower and upper limit to %Public
   * - _%rail,min; %rail,max_
     - [-]
     - Lower and upper limit to %Rail
   * - _%dhn,min; %dhn,max_
     - [-] 
     - Lower and upper limit to %DHN
   * - _top(h; td)_
     - [h]
     - Time periods duration (default 1h)
   * - _fmin; fmax(tech)_
     - [GW]ab
     - Min./max. installed size of the technology
   * - _fmin,% ; fmax,%(tech)_
     - [-]
     - Min./max. relative share of a technology in a layer
   * - _avail(res)_
     - [GWh/y]
     - Resource yearly total availability
   * - _cop(res)_
     - [MCHF/GWh] 
     - Specific cost of resources
   * - _ηcar,max_
     - [-]
     - Maximum number of cars
   * - _%Peaksh_ 
     - [-]
     - Ratio peak/max. space heating demand in typical days
   * - _f(res U tech \ sto,l)_
     - [GW]c 
     - Input from (< 0) or output to (> 0) layers. f(i; j) = 1
   * - _cinv(tech)_
     - [MCHF/GW]cb
     - Technology specific investment cost
   * - _cmaint(tech)_
     - [MCHF/GW/y]cb
     - Technology specific yearly maintenance cost
   * - _lifetime(tech)_
     - [y]
     - Technology lifetime
   * - _gwpconstr(tech)_
     - [ktCO2-eq./GW]ab
     - Technology construction specific GHG emissions
   * - _gwpop(res)_
     - [ktCO2-eq./GWh]
     - Specific GHG emissions of resources
   * - _cp(tech)_
     - [-]
     - Yearly capacity factor
   * - _ηsto,in ; ηsto,out(sto; l)_
     - [-]
     - Eficiency [0; 1] of storage input from/output to layer. Set to 0 if storage not related to layer.
   * - _%stoloss(sto)_
     - [1/h]
     - Losses in storage (self discharge)
   * - _tstoin(sto)_
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - _tstoout(sto)_
     - [-]
     - Time to charge storage (Energy to power ratio)
   * - _%stoavail(sto)_
     - [-]
     - Storage technology availability to charge/discharge
   * - _%netloss(eut)_
     - [-]
     - Losses coeficient [0; 1] in the networks (grid and DHN)
   * - _evBatt,size(v2g)_
     - [GWh]
     - Battery size per V2G car technology
   * - _cgrid;extra_
     - [MCHF]
     - Cost to reinforce the grid due to IRE penetration
     

a[Mpkm] (millions of passenger-km) for passenger, [Mtkm] (millions of ton-km) for freight mobility end-uses
b[GWh] if tech 2 STO
c[Mpkm/h] for passenger, [Mtkm/h] for freight mobility end-uses