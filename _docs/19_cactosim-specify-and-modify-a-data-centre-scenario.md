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
[Doc19_6]: {{ base_path }}/assets/images/Doc19_6.png "Model Access"
[Doc19_7]: {{ base_path }}/assets/images/Doc19_7.png "Model Access"
[Doc19_8]: {{ base_path }}/assets/images/Doc19_8.png "Model Access"
[Doc19_9]: {{ base_path }}/assets/images/Doc19_9.png "Model Access"
[Doc19_10]: {{ base_path }}/assets/images/Doc19_10.png "Model Access"
[Doc19_11]: {{ base_path }}/assets/images/Doc19_11.png "Model Access"
[Doc19_12]: {{ base_path }}/assets/images/Doc19_12.png "Model Access"
[Doc19_13]: {{ base_path }}/assets/images/Doc19_13.png "Model Access"
[Doc19_14]: {{ base_path }}/assets/images/Doc19_14.png "Model Access"
[Doc19_15]: {{ base_path }}/assets/images/Doc19_15.png "Model Access"
[Doc19_16]: {{ base_path }}/assets/images/Doc19_16.png "Model Access"
[Doc19_17]: {{ base_path }}/assets/images/Doc19_17.png "Model Access"
[Doc19_18]: {{ base_path }}/assets/images/Doc19_18.png "Model Access"
[Doc19_19]: {{ base_path }}/assets/images/Doc19_19.png "Model Access"
[Doc19_20]: {{ base_path }}/assets/images/Doc19_20.png "Model Access"
[Doc19_21]: {{ base_path }}/assets/images/Doc19_21.png "Model Access"
[Doc19_22]: {{ base_path }}/assets/images/Doc19_22.png "Model Access"

CactoSim provides a wealth of options to modify and adapt physical or logical data centre resources. This section of the user manual explains the individual building blocks used to define and manipulate various simulation scenarios in CactoSim. Users can combine those building blocks to fit the purpose of a specific data centre analysis. 

Each subsection contains detailed step-by-step instructions supported by screenshots of the actual graphical user interface provided by CactoSim. The aim is to cover the functionality of core features of this CactoSim release as well as to introduce the general principle notion of cloud modelling using the provided tree editor interface. This section presents the building blocks in a typical usage order, from importing the models from the Runtime Model Storage to versioning of a model for later analyses.

---
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

---
# Load a scenario specification from the prediction model storage

Once the models have been stored in the prediction model storage (see “Store a scenario specification in the prediction model storage”) they can be loaded and explored by standard versioning tools procedures. 

Right-click the models folder under the Model Repository view and selecting the __Checkout__ option, see *Figure 6*.

![alt text][Doc19_6]
*Figure 6: Load a Scenario Specification from the Prediction Model Storage - Checkout

Create a local project folder where the models will be placed by giving it a name, see *Figure 7*.

![alt text][Doc19_7]
*Figure 7: Load a Scenario Specification from the Prediction Model Storage – Create Project

- Once the models are checked-out they will appear in the model explorer window which is by default located on the left hand side, see *Figure 8*.

![alt text][Doc19_8]
*Figure 8: Load a Scenario Specification from the Prediction Model Storage – Model Explorer

---
# Creation of Virtual Machines

The creation of VMs is required for scenarios with additional VMs deployed in the data centre. Those VMs can be based on existing VMs in the Infrastructure models or completely customized to fit the behaviour of VMs for any given scenario. 

In order to create a Virtual Machine model element, it firstly has to have a valid __VM Image__ entity to be linked with. Once the models are retrieved using instructions from “*Load a Data Centre Model from the Runtime Model Repository*”: 

- Double click the logical data centre model file in the workspace to open it. Next right-click the top __Logical DC Model__ element and from the menu select __New Child -> VM Image__, as shown in *Figure 9*.

![alt text][Doc19_9]
*Figure 9: Creating of VM - VM Image Instance

- Define properties of a newly created __VM Image__ entity under the __Properties__ view, as shown in *Figure 10*.

![alt text][Doc19_10]
*Figure 10: Creating of VM –VM Image Properties

- Next right click on the __Hypervisor__ entity and select __New Child -> Virtual Machine__ menu, shown in Figure 11.

![alt text][Doc19_11]
*Figure 11: Creating of VM –New Instance

- Further following the same principle right click on the created __Virtual Machine__ instance and create __VM Image Instance__, __Virtual Memory__, __Virtual Processing Unit__ and application model. A sample configuration is shown in Figure 12.

![alt text][Doc19_12]
*Figure 12: Creating of VM - Configuration

---
#Creation of Compute Nodes

Adaptation scenarios can require the adding of new compute nodes to the simulated data centre. Compute nodes belong to racks, which are contained in the physical data centre model. In order to create compute node elements, the following steps need to be performed:

- Right-click on the __Rack__ element which should contain the new node, select __New Child -> Compute Node__, as shown in *Figure 13*.

![alt text][Doc19_13]
*Figure 13: Creation of Compute Nodes – New Entity

- In the newly created __Compute Node__ entity properties fill in the required attributes. Right click on the newly created node and create as a child __Processing Unit Specification__, __Storage Specification__ and __Memory Specification__. Example configuration options are shown in *Figure 14.

![alt text][Doc19_14]
*Figure 14: Creation of Compute Nodes – Configuration Properties

---
#Assignment of VMs to Compute Nodes and Moving of VMs

In order to assign a VM to a compute node it needs to be linked to a hypervisor that is running on that node. Note that each physical node can only have one hypervisor. You may want to re-use an existing hypervisor and move a VM there by Cut-and-Paste or via Drag-and-Drop. In the section “Creation of Compute Nodes” it was shown how to create a new “Compute Node” entity. In this section we will create a “Hypervisor” and move a VM to it. To begin:

![alt text][Doc19_15]
*

![alt text][Doc19_16]
*

![alt text][Doc19_17]
*

![alt text][Doc19_18]
*

![alt text][Doc19_19]
*

![alt text][Doc19_20]
*

![alt text][Doc19_21]
*

![alt text][Doc19_22]

