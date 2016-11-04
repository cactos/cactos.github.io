---
title: "Prerequisites and Requirements"
permalink: /docs/installation-guides/prerequisites-and-requirements/
---

{% include base_path %}

The installation of CACTOS Toolkit is based on the incentive of the user to use CACTOS. As described in the above section "Typical Usage Scenarios", one can make use only of the [Monitoring](https://cactos.github.io/docs/scenarios/monitoring-only/), the [Datacentre Management](https://cactos.github.io/docs/scenarios/data-centre-management/), the [Simulation](https://cactos.github.io/docs/scenarios/simulation-only/) or install the [full loop](https://cactos.github.io/docs/scenarios/full-loop/). 

# Install Puppet

The installation of CACTOS was [**Puppet**](https://puppet.com/)-ised, in order to deliver the CACTOS Toolkit as coherent as possible. Hence the only requirement is to install the Puppet client on any virtual machine you choose to place the CACTOS components. 
All the components of CACTOS were described as Puppet modules.
There is an [official installation guide](https://docs.puppet.com/puppet/3.8/reference/install_el.html) for Puppet, depending on the operating system. For Ubuntu 14.04, i.e. you can just run:

```bash
wget https://apt.puppetlabs.com/puppetlabs-release-pc1-trusty.deb
sudo dpkg -i puppetlabs-release-pc1-trusty.deb
sudo apt-get update
sudo apt-get install puppet
sudo apt-get install puppet-agent # to get the last version 4.8.0
```

Test the installed version with `puppet --version`. If it returns 4.8.0, you are good to go. In any other case, try to get the 4.8.0 version from Puppet guides.


## A generic CACTOS Puppet module installation

Every CACTOS module has some dependencies to other technologies. The description lies in the `metadata.json` file in every module.
For example:

```json
{
  "name": "cactos-cactos_monitoring_gui",
  "version": "0.1.0",
  "author": "cactos",
  "summary": null,
  "license": "Apache-2.0",
  "source": "",
  "project_page": null,
  "issues_url": null,
  "dependencies": [
    {"name":"puppetlabs-stdlib","version_requirement":">= 1.0.0"},
    {"name":"stankevich-python","version_requirement":">= 1.17.0"},
	{"name":"puppet-archive","version_requirement":">= 1.1.2"}
  ],
  "data_provider": null
}
```

In the dependencies are the `puppetlabs-stdlib`, `stankevich-python`, `puppet-archive`. Install each one of them as `sudo puppet module install <dependency_name>`.

After installing the dependencies, a folder structure is created under the folder `/etc/puppetlabs/code/environments/production/` and all the modules are installed under the folder path `/modules`.
Also the CACTOS modules, ***must be placed under the modules folder***.

After configuration run:

```bash 
puppet apply site.pp
```

# Install more required packages

* Install git package

```bash
sudo apt-get install git
```