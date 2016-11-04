---
title: "Specify and modify a data centre scenario in CactoSim"
permalink: /docs/tutorials/cactosim-specify-and-modify-a-data-centre-scenario/
---

{% include base_path %}

{% include toc %}

[Doc19_1]: {{ base_path }}/assets/images/Doc19_1.png "Load DC"
[Doc19_2]: {{ base_path }}/assets/images/Doc19_2.png "Load DC - Select"
[Doc19_3]: {{ base_path }}/assets/images/Doc19_3.png "Name Project"
[Doc19_4]: {{ base_path }}/assets/images/Doc19_4.png "Credentials"
[Doc19_5]: {{ base_path }}/assets/images/Doc19_5.png "Model Access"

CactoSim provides a wealth of options to modify and adapt physical or logical data centre resources. This section of the user manual explains the individual building blocks used to define and manipulate various simulation scenarios in CactoSim. Users can combine those building blocks to fit the purpose of a specific data centre analysis. 

Each subsection contains detailed step-by-step instructions supported by screenshots of the actual graphical user interface provided by CactoSim. The aim is to cover the functionality of core features of this CactoSim release as well as to introduce the general principle notion of cloud modelling using the provided tree editor interface. This section presents the building blocks in a typical usage order, from importing the models from the Runtime Model Storage to versioning of a model for later analyses.

# Load a Data Centre Model from the Runtime Model Repository
The CACTOS models can be imported (loaded) from the CDO Runtime Model Storage by:

- Clicking in the Eclipse menu __File -> Import__ shown in Figure 1

![alt text][Doc19_1]
*Figure 1: Load a Data Centre Model from the Runtime Model Repository - Import*

- Then expanding the __CactoSim__ folder and selecting the option __Runtime Model Storage to Workspace__ (*Figure 2*). This action will trigger the CactoSim project creation wizard.

![alt text][Doc19_2]
*Figure 2: Load a Data Centre Model from the Runtime Model Repository – Select Wizard*

- Next, provide the name for the project that will be created in the workspace, as shown in *Figure 3*.

![alt text][Doc19_3]
*Figure 3: Load a Data Centre Model from the Runtime Model Repository – Name Project*

- Then enter credentials for accessing the CDO Runtime Model Repository and click “Finish”, shown in *Figure 4*.

![alt text][Doc19_4]
*Figure 4: Load a Data Centre Model from the Runtime Model Repository - Credentials*

- CactoSim will now connect to the server and fetch CACTOS models to the workspace folder. The models can then be viewed and edited in the resource tree viewer, shown in *Figure 5*.
![alt text][Doc19_5]
*Figure 5: Load a Data Centre Model from the Runtime Model Repository – Model Access*

