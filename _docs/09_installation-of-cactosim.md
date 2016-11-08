---
title: "Installation of CactoSim"
permalink: /docs/installation-guides/installation-of-cactosim/
---

{% include base_path %}

[Doc9_1]: {{ base_path }}/assets/images/Doc9_1.png "CactoSim Installation"

CactoSim is an Eclipse feature which is integrated with the Palladio and SimuLizar simulation frameworks. During the tool installation all of the core components are fetched automatically from the respective locations.![alt text][Doc9_1]

The installation steps should be performed in this order:

- Use the Eclipse Modeling Tools [Neon](http://www.eclipse.org/downloads/)
- Install QVTo SDK 3.6 [Update Site](http://download.eclipse.org/mmt/qvto/updates/releases/3.6.0/)
- Install CactoSim from release [update site](https://sdqweb.ipd.kit.edu/eclipse/cactos/cactosim/releases/latest/)

**Note:**
Do not restart Eclipse after 3). Instead, close it, conduct step 4)-6), and then start it again)
{: .notice--info}

- Download [this](https://svn.fzi.de/svn/cactos/code/integration/trunk/eu.cactosfp7.configuration/) and insert into the configuration subfolder of the Eclipse directory
- Modify your eclipse.ini by appending the following lines at the very end:

```sh
-Dorg.osgi.service.http.port=9090
-Dfelix.fileinstall.dir=./configuration/eu.cactosfp7.configuration/
-Dfelix.fileinstall.noInitialDelay=true
-Dfelix.fileinstall.poll=1000
```

- Due to interferences of CDO UI Plugins the OSGi start levels of certain plugins have to be changed. Unfortunately, this has to be done by hand and cannot be automated. The appropriate configuration file bundles.info lies within the folder (eclipse-folder)/configuration/org.eclipse.equinox.simpleconfigurator. The file is comma-separated, the first column specifies plugin-name, the column before the last specifies start level, and the last one specifies the auto start setting.
- The following bundles have to be adjusted from start level 4 to 7

```
- org.eclipse.emf.cdo.ui 
- org.eclipse.emf.cdo.ui.admin
- org.eclipse.emf.cdo.ui.compare
- org.eclipse.emf.cdo.ui.shared
- org.eclipse.emf.cdo.ui.team
```

- The following bundles have to get auto start set from false to true:

```
- org.eclipse.equinox.cm
- org.apache.felix.fileinstall
- eu.cactosfp7.cactoopt.optimisationservice.* (for all optimisation algorithms which should be available)
- eu.cactosfp7.cactoopt.placementservice.* (for all placement algorithms which should be available)
```

**Tip:** For configurations on a Mac:
 1. Right click on the eclipse application icon itself, e.g. eclipse.app, 
 2. Select Show package contents, 
 3. Edit Contents>eclipse>eclipse.ini
{: .notice--info}

# Tutorial Links

Please see the following tutorial links for how to use CactoSim:

- [How to specify and modify a data centre scenario in CactoSim](https://cactos.github.io/docs/tutorials/cactosim-specify-and-modify-a-data-centre-scenario/)

- [How to run a simulation](https://cactos.github.io/docs/tutorials/cactosim-run-a-simulation/)

- [How to display simulation results](https://cactos.github.io/docs/tutorials/cactosim-display-simulation-results/)

# Meet CactoSim Video
[![youtube video](https://cactos.github.io/assets/images/Doc9_2.PNG)](https://www.youtube.com/watch?v=Ah6uW1kfjkA)



