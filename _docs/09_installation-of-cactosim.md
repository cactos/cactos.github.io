---
title: "Installation of CactoSim"
permalink: /docs/installation-guides/installation-of-cactosim/
---

{% include base_path %}

{% include toc %}

## Installation

CactoSim is an Eclipse feature which is integrated with the Palladio and SimuLizar simulation frameworks. During the tool installation all of the core components are fetched automatically from the respective locations.

The installation steps should be performed in this order:

- Download Eclipse Mars R1 Modeling Tools Edition via http://www.eclipse.org/downloads/
- Install MMT QVTo via http://download.eclipse.org/mmt/qvto/updates/releases/3.5.0/
(Note: This step will be removed in the future, but our current build infrastructure necessitates that this is done manually)
- Install CactoSim via one of the update sites: https://sdqweb.ipd.kit.edu/eclipse/cactos/cactosim/nightly/ or https://sdqweb.ipd.kit.edu/eclipse/cactos/cactosim/releases/latest/
- Download https://svn.fzi.de/svn/cactos/code/integration/trunk/eu.cactosfp7.configuration/ and insert into the configuration subfolder of the Eclipse directory.
- Modify your eclipse.ini by appending the following lines at the very end:

```sh
-Dorg.osgi.service.http.port=9090
-Dfelix.fileinstall.dir=./configuration/eu.cactosfp7.configuration/
-Dfelix.fileinstall.noInitialDelay=true
-Dfelix.fileinstall.poll=1000
```
> Note:
> For configurations on a Mac:
> 1. Right click on the eclipse application icon itself, e.g. eclipse.app
> 2. Select Show package contents
> 3. Edit Contents>eclipse>eclipse.ini

Executing test example:

- Configure cactoopt_optimisationalgorithm.cfg in the config folder to your liking, i.e. by setting the algorithm to LinKernighan or Random. This can be done while the platform is running, no need to restart when you change the optimisation settings.
- Boot up Eclipse and import our Y2 demo project: https://svn.fzi.de/svn/cactos/code/sim/trunk/eu.cactosfp7.cactosim.year2demo.bba/
- Run the Eclipse launch configuration for the Y2 Demo: "Year 2 Demonstration.launch".
- Wait for the simulation to finish
- Look at the results in the EDP2 -> Experiments view perspective.


