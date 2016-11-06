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
sudo -i
wget https://apt.puppetlabs.com/puppetlabs-release-pc1-trusty.deb
sudo dpkg -i puppetlabs-release-pc1-trusty.deb
sudo apt-get update
sudo apt-get install puppet
sudo apt-get install puppet-agent # to get the last version 4.8.0
```

Test the installed version with `puppet --version`. If it returns 4.8.0, you are good to go. In any other case, try to get the 4.8.0 version from Puppet guides.


## Install more required packages

* Install git package

```bash
sudo apt-get install git
```

# A generic CACTOS Puppet module installation

Every CACTOS module has some dependencies to other technologies. An easy way to install them is to use a package manager lik `librarian-puppet`.

**1.** Make sure you have installed `Puppet` and run `gem install librarian-puppet`

**2.** Navigate to the folder `/etc/puppetlabs/code/environments/production/` and run `librarian-puppet init`. A file with the name `Puppetfile` will be created.

**3.** Modify the `Puppetfile` and add the git repository of the CACTOS tool you want to install. The file after modification should look like this:

```ruby
#!/usr/bin/env ruby
#^syntax detection

forge "https://forgeapi.puppetlabs.com"

# use dependencies defined in metadata.json
# metadata

# use dependencies defined in Modulefile
# modulefile

# A module from the Puppet Forge
# mod 'puppetlabs-stdlib'

# A module from git
# mod 'puppetlabs-ntp',
#   :git => 'git://github.com/puppetlabs/puppetlabs-ntp.git'

# A module from a git branch/tag
 mod 'puppetlabs-<class_name_of_module_in_init.pp>',
   :git => '<git_repo_https>'
#   :ref => '1.4.x'

# A module from Github pre-packaged tarball
# mod 'puppetlabs-apache', '0.6.0', :github_tarball => 'puppetlabs/puppetlabs-apache'
```

All the modules are installed under the folder path `/modules`.

**4.** Create a file with the name `site.pp`, with the configuration defined for each tool in the installation guides and save the file.

**5.** Finally run:

```bash 
puppet apply site.pp
```

**Attention!** A minimum requirement for installing CACTOS with Puppet, is to have the Puppet v4.8.0 on an Ubuntu 14.04.
{: .notice--danger}
