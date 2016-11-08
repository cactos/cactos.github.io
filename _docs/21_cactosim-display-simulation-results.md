---
title: "Display Simulation Results"
permalink: /docs/tutorials/cactosim-display-simulation-results/
---

{% include base_path %}

{% include toc %}

[Doc21_1]: {{ base_path }}/assets/images/Doc21_1.png "Load DC"
[Doc21_2]: {{ base_path }}/assets/images/Doc21_2.png "Load DC - Select"
[Doc21_3]: {{ base_path }}/assets/images/Doc21_3.png "Name Project"
[Doc21_4]: {{ base_path }}/assets/images/Doc21_4.png "Name Project"
[Doc21_5]: {{ base_path }}/assets/images/Doc21_5.png "Name Project"
[Doc21_6]: {{ base_path }}/assets/images/Doc21_6.png "Name Project"
[Doc21_7]: {{ base_path }}/assets/images/Doc21_7.png "Name Project"
[Doc21_8]: {{ base_path }}/assets/images/Doc21_8.png "Name Project"

Once all of the model components have been created and configured (as shown in __Data Centre Scenario Specification and Modification__), the simulation experiment run has finished (as shown in __Run a Simulation__). This section explains how to access and read the experiment results post completion of a simulation run.

---

# Show resource utilisation for Compute Node

The Simulation results can be accessed, viewed and exported upon completion of a simulation run. From the Eclipse top menu, __Window -> Open Perspective -> Other -> PCM Results__ must be selected. The data store will be represented in the experiments tree view on the left hand side (*Figure 1*) arranged according to the execution time stamp and the name given in the previous step of simulation parameters setup.

![alt text][Doc21_1]
*Figure 1: Show Resource Utilization for Compute Node*

Double-clicking on the resource tuple will bring up the option menu, as shown in Figure 2. Here the visualisation type for displaying simulated results can be selected.

![alt text][Doc21_2]

*Figure 2: Visualisation selection*

Right-clicking will allow the user to access a chart export menu which allows for the moving of results for analysis elsewhere, as shown in *Figure 3*.

![alt text][Doc21_3]

*Figure 3: Chart export menu*

To view CPU utilisation results, select the entry named __State of Active Resource Tuple of CPU [x] on Node x__.

> Note that if the resource tuple has word “EMPTY” in front of it, it means that no data was collected during the simulation.

---

# Show resource utilisation for local storage of Compute Nodes

The procedure for accessing the local Storage simulated utilisation results is the same as one for Processing Unit shown in __Show resource utilization for Compute Node__, only to view HDD utilisation results select entry named __State of Active Resource Tuple of HDD [x] on Node x__. This will display utilization over time results *Figure 1* only for the local disk.

Also another type of resource utilisation representation is available in the form of a frequency histogram, as shown in *Figure 4*.

![alt text][Doc21_4]
*Figure 4: Show resource utilization for local storage of compute nodes*

---

# Show energy consumption for Compute Node

The capabilities of CactoSim to handle energy efficiency analysis are based on the scientific publications  [18][19] that were the foundation for Palladio extension for energy efficiency analyses.

Once the simulation run is finished, the __*.infrastructure__ file that has been created should be opened. This is the model layer where power distribution units are linked to each node.

- Open EDP2 perspective __Experiments__ view, as shown in *Figure 5*.

![alt text][Doc21_5]

*Figure 5: Show energy consumption for compute node - Experiments*

- Select the part of the infrastructure for which you want to perform the analysis, shown in *Figure 6*.

![alt text][Doc21_6]
*Figure 6: Show energy consumption for compute node –Infrastructure model*

- Open the Power Consumption Analysis view, parameterise the analyser, i.e. by setting the sliding window size used to aggregate the CPU utilization. 
- Start the consumption analysis by clicking the respective button. 
- This will open up graphs for the cumulative energy consumption, shown in Figure 7.

![alt text][Doc21_7]
*Figure 7: Show energy consumption for compute node –Energy Consumption*

- As well as the power consumption, shown in *Figure 8*.

![alt text][Doc21_8]
*Figure 8: Show power consumption for compute node*

> Note that Figure 7 and Figure 8 show full screenshots of the Eclipse environment.  The __Power Consumption Analysis__ view can be found under __Window - > Show view -> Power Consumption__.


