.. _workflow:

Getting Started
===============

The code, its documentation and the case study are gathered on a GitHub repository1. In the index and the README.md file is summarise how to launch the energy model in four steps. Here below, we propose an extensive explanation including how to compute the typical days and manage data. The data are managed through excel files which are related ones to each others. The models are coded in AMPL, using the solver CPLEX. However, the energy model proposed can be run using the open-source GLPK and the GLPSOL solver.


Files structure and download
----------------------------

EnergyScope Typical Days (EnergyScope TD) is structured as shown in Figure 13. A main folder contains three sub-folders, first one is dedicated to data management. Second, for the files related to typical days selection (STEP 1). Third and last branch regroups the files related to the energy model (STEP 2). Table 38 describes each files.
By ensuring that the download files respect the structure, the links between files should be respected and User could use the quick start procedure to launch the code.

Table 35: Yearly shares of decentralized low temperature heat & CHP technologies for the Swiss energy system in 2011.



	================= =======================
	**Technologies**	**Share heat[%]**	
	================= =======================
	HP		6.0%
	Thermal HP	0.0%
	CHP NG		0.5%
	CHP Oil		0.1%
	FC NG		0.0%
	FC H2		0.0%
	Boiler NG	25.7%
	Boiler Wood		8.2%
	Boiler Oil	49.8%
	Solar Th.	0.5%
	Direct Elec.	9.2%
	================= =======================

Table 36: Yearly shares of DHN low temperature heat & CHP technologies for the Swiss energy system in 2011.


	================= =======================
	**Technologies**	**Share heat[%]**	
	================= =======================
	HP		4.8%
	CHP NG		1.2%
	CHP Wood		6.6%
	CHP Waste	72.5%
	Boiler NG	13.8%
	Boiler Wood		0.0%
	Boiler Oil	0.6%
	Deep Geothermal	0.4%
	================= =======================
.. _README.md: