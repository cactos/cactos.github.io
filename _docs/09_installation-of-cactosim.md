---
title: "Installation of CactoSim"
permalink: /docs/installation-guides/installation-of-cactosim/
---

{% include base_path %}

[Doc9_1]: {{ base_path }}/assets/images/Doc9_1.png "CactoSim Installation"
[Doc9_2]: {{ base_path }}/assets/images/Doc9_2.png "Youtube video"

CactoSim is an Eclipse feature which is integrated with the Palladio and SimuLizar simulation frameworks. During the tool installation all of the core components are fetched automatically from the respective locations.![alt text][Doc9_1]

The installation steps should be performed in this order:

- Download Eclipse Mars Modelling Tools latest [release](http://www.eclipse.org/downloads/packages/eclipse-modeling-tools/neon1). Unpack it in the desired location on the disk and launch.
- Once Eclipse is fully loaded and launched, go to the *Help->Install New Software* menu option. Here the user can install remaining components by the below provided links. Paste the link in the *Work with* field and hit *Enter*. This will resolve all required packages and start the installation wizard.
- Install the Palladio simulation framework by using nightly [update site](http://sdqweb.ipd.kit.edu/eclipse/palladio/nightly)
- Once Eclipse is restarted, in the same way install the SimuLizar add-on also using the [nightly build site](http://sdqweb.ipd.kit.edu/eclipse/simulizar/nightly/)
- Finally, following the same steps, install CactoSim from the [release build site](https://sdqweb.ipd.kit.edu/eclipse/cactos/cactosim/release/2.1/)

- Modify your eclipse.ini by appending the following lines at the very end:

```sh
-Dorg.osgi.service.http.port=9090
-Dfelix.fileinstall.dir=./configuration/eu.cactosfp7.configuration/
-Dfelix.fileinstall.noInitialDelay=true
-Dfelix.fileinstall.poll=1000
```

**Tip:** For configurations on a Mac:
 1. Right click on the eclipse application icon itself, e.g. eclipse.app, 
 2. Select Show package contents, 
 3. Edit Contents>eclipse>eclipse.ini
{: .notice--info}

[![IMAGE ALT TEXT HERE](http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](http://www.youtube.com/watch?v=YOUTUBE_VIDEO_ID_HERE)

![alt text][Doc9_2](https://www.youtube.com/watch?v=Ah6uW1kfjkA)

