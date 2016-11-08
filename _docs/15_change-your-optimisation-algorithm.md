---
title: "Implement a new optimisation service"
permalink: /docs/dev-guides/implement-a-new-optimisation-service/
---
{% include base_path %}

{% include toc %}

In order to add new optimisation capabilities to [CactoOpt](https://github.com/cactos/cactoopt) one should create a new Java project that implements two interfaces and extends one abstract class listed below. Additionally, one should configure the **component.xml** file in the **OSGI-INF** directory.

## Optimisation

### abstract class AbstractOptimisationService
The main class of the optimisation service, including references to the **IOptimisationAlgorithm** and **IOptimisationConfigurable**, as well as, implementing the logic of the OSGI ManagedService.

### interface IOptimisationAlgorithm
The actual logic of the optimisation service.

### interface IOptimisationConfigurable
Allows dynamic configuration changes in runtime.

### OSGI-INF/component.xml
Configures the algorithm name *{OPTIMISATION_ALGORITHM_NAME}* that is used in **cactoopt_optimisationalgorithm.cfg** file for optimisation algorithm selection and the configuration file *{CONFIGURATION_FILE_NAME}* that can specify additional algorithm-specific parameters.

    <property name="placementName" type="String" value="{OPTIMISATION_ALGORITHM_NAME}" />
    <property name="service.pid" type="String" value="{CONFIGURATION_FILE_NAME}"/>
    
To make CactoOpt using the new optimisation service modify the **cactoopt_optimisationalgorithm.cfg** by setting

    algorithm = {OPTIMISATION_ALGORITHM_NAME}

## Placement

### abstract class AbstractPlacementService
The main class of the placement service, including references to the **InitialPlacementAlgorithm** and **IPlacementConfigurable**, as well as, implementing the logic of the OSGI ManagedService.

### interface InitialPlacementAlgorithm
The actual logic of the placement service.

### interface IPlacementConfigurable
Allows dynamic configuration changes in runtime.

### OSGI-INF/component.xml
Configures the algorithm name *{PLACEMENT_ALGORITHM_NAME}* that is used in **cactoopt_placement.cfg** file for placement algorithm selection and the configuration file *{CONFIGURATION_FILE_NAME}* that can specify additional algorithm-specific parameters.

    <property name="placementName" type="String" value="{PLACEMENT_ALGORITHM_NAME}" />
    <property name="service.pid" type="String" value="{CONFIGURATION_FILE_NAME}"/>
    
To make CactoOpt using the new placement service modify the **cactoopt_placement.cfg** by setting

    placementName = {PLACEMENT_ALGORITHM_NAME}