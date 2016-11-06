---
title: "Installation of CactoOpt and Integration Tools"
permalink: /docs/installation-guides/installation-of-cactoopt-and-integration-tools/
---

{% include base_path %}

{% include toc %}

The installation of CactoOpt and the Integration tools, requires the [Installation of CactoScale](https://cactos.github.io/docs/installation-guides/installation-of-cactoscale/).
Additionally the following components should be installed:

* Cloudiator
* OS-Proxy
* Runtime Optimisation
* Runtime Controller
* Runtime GUI

<figure>
  <img src="{{ base_path }}/assets/images/Cactos_Setup.png" alt="CACTOS Toolkit Components">
</figure>

Below, the configuration of the required Puppet modules is described.

**ProTip:** Make sure you have Puppet 4.8.0 installed properly.
{: .notice--info}

# Cloudiator

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-cloudiator.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```ruby
class { 'cactos_cloudiator':
 mysql_col_name => '' 
 mysql_col_pw   => '',	
 mysql_root_pw  => '', 
 col_secret     => '',
 col_prefix     => ''
}
```

# OS-Proxy

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-os-proxy.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```ruby
class { 'cactos_os_proxy':}
```

# Runtime Optimisation

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-runtime-optimisation.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```ruby
class { 'cactos_runtime_optimisation':}
```

**4.** The rest of the configuration should be handled manually.

# Runtime Controller

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-runtime-controller.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```ruby
class { 'cactos_runtime_controller':}
```

# Runtime GUI

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-runtime-gui.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```ruby
class { 'cactos_runtime_gui':
 runtimeController  => '' # The IP of the Runtime Controller VM
 runtimeManagement  => '', # The IP of the Runtime Optimisation VM
 monitoringService  => '', # The IP of the Monitoring Cluster Gateway 
 colosseumServer    => '', # The IP of the Colosseum VM
 monitoringServer   => ''
}
```

Congratulations! You have installed CactoOpt and the integration tools. Now you can manage your datacentre efficiently and make it power performant.

