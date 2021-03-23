.. _Swiss:

Swiss energy system data
========================

This appendix reports the input data for the application of the LP modeling framework to the case study of Switzerland in the years 2035 and 2011, the latter used for model verification. The resources and technologies in Figure 6 of the paper are characterized in terms of energy and mass balances, cost (operating and investment), and environmental impact (global warming potential (GWP)).
For GHG emissions, LCA data are taken from the Ecoinvent database v3.2 [11] using the "allocation at the point of substitution" method. GWP is assessed with the "GWP100a - IPCC2013" indicator. For technologies, the GWP impact accounts for the technology construction; for resources, it accounts for extraction, transportation and combustion.
For the cost, the reported data are the nominal values for Switzerland in the year 2035. All costs are expressed in *real*  Swiss Francs for the year 2015 (\ :sub:`2015`\ ). All cost data used in the model originally expressed in other currencies or referring to another year are converted to CHF\ :sub:`2015`\  to offer a coherent comparison. The method used for the conversion is illustrated by Eq. 43.

.. math::
	c_{inv}\left [ CHF_{2015} \right ]=c_{inv}\left [ C_{y} \right ]\cdot \frac{USD_{y}}{C_{y}} \cdot \frac{CEPCI_{2015}\left [ USD_{2015} \right ]}{CEPCI_{y}\left [ USD_{y} \right ]}\cdot \frac{CHF_{2015}}{USD_{2015}}  (43)

.. list-table:: Table 5: CEPCI values [12]
   :widths: 25 25
   :header-rows: 1

   * - Year
     - CEPCI
   * - 1982 
     - 285.8
   * - 1990 
     - 357.6
   * - 1991
     - 362.3
   * - 1992
     - 367.0
   * - 1993
     - 371.7
   * - 1994
     - 376.4
   * - 1995
     - 381.1
   * - 1996
     - 381.7
   * - 1997
     - 386.5
   * - 1998
     - 389.5
   * - 1999
     - 390.6
   * - 2000
     - 394.1
   * - 2001
     - 394.3
   * - 2002
     - 395.6
   * - 2003
     - 402.0
   * - 2004
     - 444.2
   * - 2005
     - 468.2
   * - 2006
     - 499.6
   * - 2007
     - 525.4
   * - 2008
     - 575.4
   * - 2009
     - 521.9
   * - 2010
     - 550.8
   * - 2011
     - 585.7
   * - 2012
     - 584.6
   * - 2013
     - 567.3
   * - 2014
     - 576.1
   * - 2015
     - 556.3


Where C and *y* are the currency and the year in which the original cost data are expressed, respectively, is the symbol of American Dollars and the Chemical Engineering's Plant Cost Index (CEPCI) [12] is an index taking into account the evolution of the equipment cost (values reported in Table 5). As an example, if the cost data are originally in EUR\ :sub:`2010`\ , they are first converted to USD\ :sub:`2010`\ , then brought to USD\ :sub:`2015`\  taking into account the evolution of the equipment cost (by using the CEPCI), and finally converted to CHF\ :sub:`2015`\ . The intermediate conversion to USD is motivated by the fact that the CEPCI is expressed in *nominal* USD. ALthough this conversion method is originally defined for technology-related costs, in this thesis as a simplification it used also for the cost of resources.

Energy demand
-------------

The EUD for heating, electricity and mobility in 2035 is calculated from the data in [13] for the"Politisches Massnahmenpaket" ("PMF", Political Measures of the Federal Council) scenario in the year 2035.

Heating
^^^^^^^
The EUD for SH in households is calculated as the product of the number of inhabitants in Switzerland, the per capita living space and the annual specific heating requirement (Table 6). The EUD for HW in households is the only heating requirement which is not calculated based on the "PMF" scenario. It is calculated assuming a *per capita* daily HW consumption of 50L/day/inhabitant and a temperature increase of 40 °C [14].


.. list-table:: Table 6: Data for the calculation of the end use energy demand in the households sector.
   :widths: 45 30
   :header-rows: 1

   * - 
     - "PMF" scenario in 2035 [13]
   * - Population [10\ :sup:`6`\  people]
     - 8.89
   * - Living space [m\ :sup:`2`\ /person]
     - 67
   * - Specific heating requirement [kWh/m\ :sup:`2`\ /y]
     - 49.5
   * - HW consumption [L/day/person]
     - 50 [14]
   * - Temperature increase for HW production [°C]
     - 40



Table 7 reports input data and calculated values for the heating EUD in the different sectors. The calculation of the end-use heating demand in the industry and services sectors starts from the FEC data by type of heat usage, available in Table 9-18 and Table 9-23 in [13]. The FEC values reported in [13] are the sum of the fuel consumption in boilers, the electricity consumption for direct electric heating and for HPs, and the ambient heat used by the latter. The EUD for heating in the industry and service sectors accounts for the heat supplied by the HPs (equal to the sum of the ambient heat and their electricity consumption), the heat produced by direct electric heating systems (equal to their electricity consumption) and the heat supplied by boilers (which is estimated assuming a 90% efficiency).
For both sectors, first the FEC is shared among the different technologies, then it is proportionally divided among space heating, hot water and process heating. The ambient heat consumption is obtained from tables 9-21 and 9-27 in [13]. The electricity consumed by the heat pumps using the reported ambient heat is calculated using a coefficient of performance (COP) of 3.7. The COP is based on the ambient heat and electricity consumption of the heat pumps in the household sector in 2035 (table 9-7 and 9-10 in [13]). The electricity consumption for direct electric heating is computed as the sum of the electricity consumption for space heating, hot water and process heating (Tables 9-19 and 9-24 in [13]) minus the calculated electricity consumption of the heat pumps. The use of direct electric heating systems is divided between space heating, hot water and process heating proportionally to the FEC of each end-use type. It is assumed that heat pumps are not used for the high temperature EUD in the industry sector. Thus, the use of heat pumps is shared between space heating and hot water.
In the model, there is a repartition between low temperature and high temperature heating EUD. The first one includes EUD for space heating and hot water. The second one is the EUD for process heating. The services sector has only low temperature heating EUD, while the industry sector has both.

Process heating and HW demand are considered constant over the year, whereas SH demand is shared over the year according to %\ :sub:`heating`\ , which is illustrated in Figure 8 (based on the data presented in Appendix D of [15]). Another illustration is Table 8 that summarises these data by aggregating the monthly heat demands.

table7
imagen

.. list-table:: Table 8: Aggregated monthly distribution factors for SH demand (%heating) and varying electricity demand (%elec).
   :widths: 7 7 7 7 7 7 7 7 7 7 7 7 7  
   :header-rows: 2

   * - Yearly
     - share
     - (adding
     - up
     - to
     - 1)
     - of
     - space
     - heating
     - and
     - electricity
     - [-]
     -
   * -
     - Jan.
     - Feb.
     - Mar.
     - Apr.
     - May
     - Jun.
     - Jul.
     - Aug.
     - Sep.
     - Oct.
     - Nov.
     - Dec.
   * - %\ :sub:`heating`\ 
     - 0.179
     - 0.168
     - 0.138
     - 0.064
     - 0.036
     - 0.010
     - 0.007
     - 0.010
     - 0.029
     - 0.078
     - 0.111
     - 0.170
   * - %\ :sub:`elec`\ 
     - 0.091
     - 0.081
     - 0.089
     - 0.079
     - 0.081
     - 0.079
     - 0.078
     - 0.080
     - 0.082
     - 0.084
     - 0.086
     - 0.089
    