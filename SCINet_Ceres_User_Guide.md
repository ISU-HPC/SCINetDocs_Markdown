# Technical Overview

Ceres is the dedicated high performance computing (HPC) infrastructure for ARS researchers on ARS SCINet. Ceres is designed to enable large-scale computing and large-scale storage. Original cluster had a total of 64 regular compute nodes and 5 high-memory nodes. In 2018-2019 additional nodes have been purchased. Currently the following compute nodes are available on the cluster.

65 nodes, each having:

40 logical cores on 2 x 10 core Intel Xeon Processors (E5-2670 v2 2.50GHz 25MB Cache) with hyper-threading turned ON
128GB DDR3 ECC Memory
2 x 120GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
1TB SSD used for temporary local storage
Mellanox ConnectX®­3 VPI FDR InfiniBand
20 new nodes, each having:

72 logical cores on 2 x 18 core Intel Xeon Processors (6140 2.30GHz 25MB Cache) with hyper-threading turned ON
384GB DDR3 ECC Memory
250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
1.5TB SSD used for temporary local storage
Mellanox ConnectX®­3 VPI FDR InfiniBand
2 new large memory nodes, each having:

80 logical cores on 2 x 20 core Intel Xeon Processors (6148 2.40GHz 27.5MB Cache) with hyper-threading turned ON
768GB DDR3 ECC Memory
250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
1.5TB SSD used for temporary local storage
Mellanox ConnectX®­3 VPI FDR InfiniBand
3 new large memory nodes, each having:

80 logical cores on 2 x 20 core Intel Xeon Processors (6148 2.40GHz 27.5MB Cache) with hyper-threading turned ON
1,536GB DDR3 ECC Memory
250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
1.5TB SSD used for temporary local storage
Mellanox ConnectX®­3 VPI FDR InfiniBand
5 high memory nodes, each having:

 120 logical cores on 4 x 15 Intel Xeon Processors (E7­4880 v2 2.50GHz 37.5MB Cache) with hyper-threading turned ON
 1,536GB DDR ECC Memory
 2 x 120GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS)
 16 x 600GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to provide 9.6TB of local scratch storage)
 2 x LSI SAS 9300­8i SAS 12Gb/s PCIe 3.0 8­-Port HBA
 2 x Mellanox ConnectX®­3 VPI FDR InfiniBand
1 new GPU node that has:

72 logical cores on 2 x 18 core Intel Xeon Processors (6140 2.30GHz 25MB Cache) with hyper-threading turned ON
2 Tesla V100
384GB DDR3 ECC Memory
250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
1.5TB SSD used for temporary local storage
Mellanox ConnectX®­3 VPI FDR InfiniBand




In addition there are two local specialized data transfer nodes and several service nodes.

In aggregate, there are more than 2500 compute cores (5000 logical cores) with 27 terabyte (TB) of total RAM, 150TB of total local storage, and 2.4 petabyte (PB) of shared storage.

Shared storage consists of 1.8PB high-performance BeeGFS space and 600TB of backed-up ZFS space. 


System Configuration 
Since most HPC compute nodes are dedicated to running HPC cluster jobs, direct access to the nodes is discouraged. The established HPC best practice is to provide login nodes. Users access a login node to submit jobs to the cluster’s resource manager (SLURM), and access other cluster console functions. All nodes run on Linux CentOS 7.6.

