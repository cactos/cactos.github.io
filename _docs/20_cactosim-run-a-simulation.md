---
title: "Run a Simulation"
permalink: /docs/tutorials/cactosim-run-a-simulation/
---

{% include base_path %}

[Doc20_1]: {{ base_path }}/assets/images/Doc20_1.png "Load DC"
[Doc20_2]: {{ base_path }}/assets/images/Doc20_2.png "Load DC - Select"
[Doc20_3]: {{ base_path }}/assets/images/Doc20_3.png "Name Project"

Models in the workspace can be simulated using the CactoSim launch configuration. The following shows how to configure and launch a simulation.

From the top Eclipse menu panel __Run->Run Configurations-> (double click) CactoSim__ option needs to be executed creating new simulation run configuration settings.

At first, in the __CACTOS Infrastructure Model__ tab *Figure 1*, the path to the Logical Data centre model is specified. Other required models will be loaded automatically via internal reference links.

![alt text][Doc20_1]
*Figure 1: CACTOS Models location tab*

Next, the __Simulation__ tab (*Figure 2*) allows for the naming of the simulation experiment, the selection of the persistence framework where the simulation results will be stored and the definition of the simulation stopping conditions.   

![alt text][Doc20_2]
*Figure 2: Simulation parameters setup tab*

It is necessary to specify the location where simulation results will be stored. At the __Data Set__ section select the __Browse__ option. If no previous storage was created the list will appear blank. In this case, click __Add__ and select the type of the storage required. The option __In-Memory data source__ will store the results in the volatile memory and after closing Eclipse these results will be lost. However, these results can also be exported to disk for display on visual graphs or outputted comma separated value (CSV) files. 

The __File data source__ can be chosen to save results in the original binary format. If this option is selected the option will be available to select a storage location in the workspace folders or anywhere on the disk. Please refer to *Figure 3* for a visual example.

![alt text][Doc20_3]
*Figure 3: Simulation results storage selection*

Finally, after selecting the storage source, the wizard will return back to the __Simulation__ tab. If all of the parameters were set, then pressing __Apply->Run__ will execute a simulation experiment run.




