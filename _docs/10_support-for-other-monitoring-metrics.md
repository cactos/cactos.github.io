---
title: "Add support for other monitoring metrics"
permalink: /docs/dev-guides/support-for-other-monitoring-metrics/
---

{% include base_path %}

{% include toc %}

As the monitoring part was described as a typical usage scenario for CACTOS [above](https://cactos.github.io/docs/scenarios/monitoring-only/), one can add further monitoring metrics to be collected by CactoScale and stored for further analysis and insights. 


## Create/add the new monitoring source
A monitoring source can be a library, a bash script, anything that can deliver a new metric that is not included already by CactoScale. The user has to prepare the physical node and install the library. If the monitoring source is a custom bash script needs to be added under the [sensors](https://github.com/cactos/Infrastructure-Tools/tree/master/bash-adaptors/sensors) folder in the node's filesystem. Here, as prerequisite is to [install an agent](https://cactos.github.io/docs/installation-guides/installation-of-cactoscale/) in the physical node and have the basic folder structure and navigate to `Infrastructure-Tools/bash-adaptors/sensors/`.

## Create a mapper
As the basic monitoring framework that is used in **CACTOS** is [Chukwa](https://github.com/cactos/chukwa/tree/chukwa4cactos), a new mapper needs to be created.

**1.** Clone the repository in your filesystem from [here](https://github.com/cactos/chukwa/tree/chukwa4cactos).

**2.** Navigate to `chukwa/src/main/java/eu/cactosfp7/datacollection/chukwa/demux/mapper/` and create a folder with the same structure as the rest of the folders there, e.g `newsource/`. With the structure:

```bash
newsource
├── NewSource.java                  # the main mapper class
├── NewSourceConstants.java         # the class with the constants
```


**3.** Modify the classes to parse the result of the monitoring source. Additionally, in the `NewSourceConstants.java` have to be defined the *column names*, the *RowKeyGenerator* objects and the *MapperCollection* objects. 

***Snippets from the code:***

**Column names definition**

```java
public static final String VMNAME = "vmname";
public static final String UUID = "UUID";
public static final String VCORES = "CpuCS";
public static final String VCORES_USAGE_VM = "CpuVM";
public static final String VCORES_USAGE_PM = "CpuPM";
public static final String VCORES_USAGE_ST = "CpuST";
public static final String VCORES_USAGE_IO = "CpuIO";
public static final String RAM_USED = "ram-used";
public static final String RAM_TOTAL = "ram-total";
public static final String NETWORK = "network";
public static final String DISK_USED = "disk-used";
public static final String DISK_TOTAL = "disk-total";
public static final String DISK_READ = "disk-read";
public static final String DISK_WRITE = "disk-write";
```

**RowKeyGenerator Objects**

```java
final RowKeyGenerator time = new TimestampedRowGenerator(SOURCE);   // The row will be <SOURCE>-<timestamp>
final RowKeyGenerator plain = new PlainValueRowGenerator(SOURCE);   // The row will be <SOURCE>
```
```java
final RowKeyGenerator multiplex_time = new SplittingRowKeyGenerator<TimestampedRowGenerator>(TimestampedRowGenerator.class, UUID);    // If a value from a column is used for the id of the row for the history table
final RowKeyGenerator multiplex = new SplittingRowKeyGenerator<PlainValueRowGenerator>(PlainValueRowGenerator.class, UUID); // If a value from a column is used for the id of the row for the snapshot table
```

**MapperCollection Objects**

```java
static MapperCollection<HBaseMappingSpecification> getHardwareMappers(HardwareMetricContext ctx) {
    return new MapperCollection<HBaseMappingSpecification>().
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_ARCH, CN_TABLE, "hardware", ctx.plain)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_CORES, CN_TABLE, "hardware", ctx.plain)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_FREQ, CN_TABLE, "hardware", ctx.plain)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(MEM_FREQ, CN_TABLE, "hardware", ctx.plain)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(MEM_SIZE, CN_TABLE, "hardware", ctx.plain)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(NETW_SPEED, CN_TABLE, "network", ctx.plain)
);
    }
```
```java
static MapperCollection<HBaseMappingSpecification> getHistoryHardwareMappers(HardwareMetricContext ctx) {
    return new MapperCollection<HBaseMappingSpecification>().
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_ARCH, CN_HISTORY_TABLE, "hardware", ctx.time)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_CORES, CN_HISTORY_TABLE, "hardware", ctx.time)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(CPU_FREQ, CN_HISTORY_TABLE, "hardware", ctx.time)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(MEM_FREQ, CN_HISTORY_TABLE, "hardware", ctx.time)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(MEM_SIZE, CN_HISTORY_TABLE, "hardware", ctx.time)).
addMapping(HBaseMappingSpecification.readKeyAsQuantifierMapping(NETW_SPEED, CN_HISTORY_TABLE, "network", ctx.time));
}
```


## Add the new monitoring source to the chukwa agent
Navigate to `chukwa/conf/agent/node/initial_adaptors` and add a new line:

```bash
add ExecAdaptor <NewSource> <invokation_interval> ${CHUKWA_ADAPTORS_PATH}/script.sh 0
```

## Add the new mapper to the chukwa collector
Navigate to `chukwa/conf/collector/chukwa-demux-conf.xml` and add a property:

```xml
   <property>
    <name>NewSource</name>
    <value>eu.cactosfp7.datacollection.chukwa.demux.mapper.newsource.NewSource</value>
   </property>
```

## Build the Chukwa distribution
Simple execute ` mvn install -DskipTests=true` on the root folder of chukwa. And two gzip files will be produced unter the *target* folder, ***chukwa-incubating-0.5.0-agent.tar.gz*** and ***chukwa-incubating-0.5.0-collector.tar.gz*** for agent and collector respectively.