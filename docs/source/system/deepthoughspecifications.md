# Deepthought: System Specifications

Deepthought is the brand new HPC for Flinders University SA, and available for Flinders Colleges to utilise. The following details the system specifications and node types that are present within the HPC.

## Partition Layout

The SLURM Scheduler as the notion of 'Job Queue' or 'Partitions'.  These manage resource allocations and job scheduling independent from on-another. At this time, there is a single job-queue for general usage. As resource usage patterns are identified, this may change.

|Partition Name |   Number of Nodes |   Usage / Purpose                    | Max Runtime    |
|---------------|   -------         |   ------                             | -----          |
|general    |   17              | General Usage Pool                   | 14 Days      |
|gpu        |   3               | GPU Access Pool                      | 14 Days      |
|melfeu     |   2               | Molecular Biology Lab   | 14 Days      |  

## Storage Layout

Scratch: ~240TB of scratch disk, mounted on all nodes

Per node /local: ~400GB to 3.2TB, depending on node layout

## Node Breakdown

- 20 Compute Nodes, with ~1800 Cores and ~10TB of RAM total
- 5 V100 Nvidia TESLA GPU's with 32GB VRAM per GPU

### General Nodes

There are 17 General Purpose nodes, each with:

- CPU:
  - 1 x AMD EPYC 7551 @2.55Ghz with 32 Cores / 64 Threads
- RAM:
  - 256GB DDR4 @ 2666Mhz
- Local Storage
  - ~3.2TB of NVMe SSD's

### GPU Nodes

There are 3 dedicated GPU nodes. They comprise of 2 'Standard' and One 'Light' Node:

#### Standard GPU Nodes
- CPU:
  - 1 x AMD EPYC 7551 @2.55Gz with 32 Cores / 64 Threads
- RAM:
  - 256GB DDR4 @ 2666Mhz
- GPU:
  - 2 x TESLA V100 w/ 32GB VRAM
- Local Storage
  - 3.2TB of NVMe

#### Light GPU Node
- CPU:
  - 1 x AMD EPYC 7551 @2.55Gz with 32 Cores / 64 Threads
- RAM:
  - 128GB DDR4 @ 2666Mhz
- GPU:
  - 1 x TESLA V100 w/ 32GB VRAM
- Local Storage
  - 1.5TB of NVMe

### High Capacity Node

There is are 3 High-Capacity nodes with:

- CPU:
  - 2 x AMD EPYC 7742 @2.25Ghz with 64 Cores / 128 Threads
- RAM:
  - 2TB (1.8TB) DDR4 @ 3200Mhz
- Local Storage
  - 2.6TB of NVMe

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
