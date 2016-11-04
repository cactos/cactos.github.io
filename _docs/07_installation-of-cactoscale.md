---
title: "Installation of CactoScale"
permalink: /docs/installation-guides/installation-of-cactoscale/
---

{% include base_path %}

{% include toc %}

The installation of CactoScale includes the following components:

* CDO Server
* Monitoring cluster
* Runtime Model updater
* Monitoring GUI

<figure>
  <img src="{{ base_path }}/assets/images/CactoScale_arch.png" alt="CactoScale Components">
</figure>

Below, the configuration of the required Puppet modules is described.

# CDO Server

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-cdo.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```yaml
class { 'cactos_cdo':}
```

# Monitoring Cluster

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-collector) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```yaml
class { 'cactos_collector':
  fs_default_name => '' # The hostname or IP of the Hadoop DFS
}
```

# Runtime Model Updater

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-modelupdater) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```yaml
class { 'cactos_modelupdater':}
```

# Monitoring GUI

**1.** Clone the repository in your filesystem from [here](https://omi-gitlab.e-technik.uni-ulm.de/cactos/puppet-monitoring-gui.git) with `git clone <repo_http>`.

**2.** Install the module.

**3.** Create a `site.pp` file under `/etc/puppetlabs/code/environments/production/` and the content should be:

```yaml
class { 'cactos_monitoring_gui':
   app_host => '' # The IP of the current VM
    app_port => '5000',	
    server_thrift_host => '', # The IP of the Monitoring Cluster VM where the thrift server runs
    server_thrift_port => '9000' 
}
```


