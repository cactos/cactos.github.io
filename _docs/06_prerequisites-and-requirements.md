---
title: "Prerequisites and Requirements"
permalink: /docs/installation-guides/prerequisites-and-requirements/
---

{% include base_path %}

The installation of CACTOS Toolkit is based on the incentive of the user to use CACTOS. As described in the above section "Typical Usage Scenarios", one can make use only of the [Monitoring](https://cactos.github.io/docs/scenarios/monitoring-only/), the [Datacentre Management](https://cactos.github.io/docs/scenarios/data-centre-management/), the [Simulation](https://cactos.github.io/docs/scenarios/simulation-only/) or install the [full loop](https://cactos.github.io/docs/scenarios/full-loop/). 

The installation of CACTOS was [**Puppet**](https://puppet.com/)-ised, in order to deliver the CACTOS Toolkit as coherent as possible. Hence the only requirement is to install the Puppet client on any virtual machine you choose to place the CACTOS components. There is an [official installation guide](https://docs.puppet.com/puppet/3.8/reference/install_el.html) for Puppet, depending on the operating system. For Ubuntu, i.e. you can just run `sudo apt-get install puppet`.