# Deepthought: System Specifications

Deepthought is the brand new HPC for Flinders University SA, and available for Flinders Colleges to utilise. The following details the system specifications and node types that are present within the HPC.

## Partition Layout

The SLURM Scheduler as the notion of 'Job Queue' or 'Partitions'.  These manage resource allocations and job scheduling independent from on-another. At this time, there is a single job-queue for general usage. As resource usage patterns are identified, this may change.

|Partition Name |   Number of Nodes |   Usage / Purpose                    | Max Runtime    |
|---------------|   -------         |   ------                             | -----          |
|hpc_general    |   13              | General Usage Pool                   | UNLIMITED      |
|hpc_melfeu     |   2               | Molecular Biology Lab private Nodes. | UNLIMITED      |  


## Node Breakdown

- 17 Compute Nodes, totalling 1376 Cores and 6.28TB of RAM combined.
- 2 Login Nodes, with High-Availability Failover
- 4 V100 Nvidia TESLA GPU's with 32GB VRAM

### General Nodes

There are 14 General Purpose nodes, each with:

- CPU:
  - 1 x AMD EPYC 7551 @2.55Ghz with 32 Cores / 64 Threads
- RAM:
  - 256GB DDR4 @ 2666Mhz

### GPU Nodes

There are 2 dedicated GPU nodes, each with:

- CPU:
  - 1 x AMD EPYC 7551 @2.55Gz with 32 Cores / 64 Threads
- RAM:
  - 256GB DDR4 @ 2666Mhz
- GPU:
  - 2 x TESLA V100 w/ 32GB VRAM

### High Capacity Node

There is a single High-Capacity node with:

- CPU:
  - 2 x AMD EPYC 7742 @2.25Ghz with 64 Cores / 128 Threads 
- RAM:
  - 2TB (1.8TB) DDR4 @ 3200Mhz

### Private Nodes

The Flinders University Molecular Biology lab maintains two nodes for their exclusive usage. Access is strictly limited to the Molecular Biology Lab.  For completeness, the two nodes are listed here as well.

#### Melfu General Node

- CPU:
  - 1 x AMD EPYC 7551 @2.55Gz with 32 Cores / 64 Threads
- RAM:
  - 512GB DDR4 @ 1966Mhz

#### Melfu High-Capacity Node

- CPU:
  - 2 x AMD EPYC 7551 @2.55Gz with 64 Cores / 128 Threads 
- RAM:
  - 2TB (1.8TB) DDR4 @ 3200Mhz

