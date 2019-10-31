#### Table of Contents
* [Technical Overview](#technical-overview)
* [System Configuration](#system-configuration)
  * [Software Environment](#software-environment)
* [System Access](#system-access)
  * [Logging in to SCINet](#logging-in-to-scinet)
  * [File Transfers](#file-transfers)
    * [Globus Online Data Transfers](#globus-online-data-transfers)
    * [Using scp to Transfer data](#using-scp-to-transfer-data)
    * [Other ways to Transfer data](#other-ways-to-transfer-data)
    * [Large Data Transfers](#large-data-transfers)
* [Modules](#modules)
  * [Useful Modules Commands](#useful-modules-commands)
  * [Loading and Unloading Modules](#loading-and-unloading-modules)
  * [Module: command not found](#module-command-not-found)
* [Quotas on Home and Project Directories](#quotas-on-home-and-project-directories)
  * [Local Sharing of Files with Other Users](#local-sharing-of-files-with-other-users)
* [Running Application Jobs on Compute Nodes](#running-application-jobs-on-compute-nodes)
  * [Partitions or Queues](#partitions-or-queues)
  * [Interactive Mode](#interactive-mode)
  * [Requesting the proper number of nodes and cores](#requesting-the-proper-number-of-nodes-and-cores)
  * [Batch Mode](#batch-mode)
    * [Serial Job](#serial-job)
    * [Running a simple OpenMP Job](#running-a-simple-openmp-job)
    * [Parallel MPI Job](#parallel-mpi-job)
  * [Useful SLURM Commands](#useful-slurm-commands)
  * [Local Scratch Space on Large Memory Nodes](#local-scratch-space-on-large-memory-nodes)
* [Compiling Software, Installing R/Perl/Python Packages and Using Containers](#compiling-software,-installing-r/perl/python-packages-and-using-containers)
* [Citation/Acknowledgment](#citation/acknowledgment)

# Technical Overview

Ceres is the dedicated high performance computing (HPC) infrastructure for ARS researchers on ARS SCINet. Ceres is designed to enable large-scale computing and large-scale storage. Original cluster had a total of 64 regular compute nodes and 5 high-memory nodes. In 2018-2019 additional nodes have been purchased. Currently the following compute nodes are available on the cluster.

65 nodes, each having:

* 40 logical cores on 2 x 10 core Intel Xeon Processors (E5-2670 v2 2.50GHz 25MB Cache) with hyper-threading turned ON
* 128GB DDR3 ECC Memory
* 2 x 120GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
* 1TB SSD used for temporary local storage
* Mellanox ConnectX®­3 VPI FDR InfiniBand

20 new nodes, each having:

* 72 logical cores on 2 x 18 core Intel Xeon Processors (6140 2.30GHz 25MB Cache) with hyper-threading turned ON
* 384GB DDR3 ECC Memory
* 250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
* 1.5TB SSD used for temporary local storage
* Mellanox ConnectX®­3 VPI FDR InfiniBand

2 new large memory nodes, each having:

* 80 logical cores on 2 x 20 core Intel Xeon Processors (6148 2.40GHz 27.5MB Cache) with hyper-threading turned ON
* 768GB DDR3 ECC Memory
* 250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
* 1.5TB SSD used for temporary local storage
* Mellanox ConnectX®­3 VPI FDR InfiniBand

3 new large memory nodes, each having:

* 80 logical cores on 2 x 20 core Intel Xeon Processors (6148 2.40GHz 27.5MB Cache) with hyper-threading turned ON
* 1,536GB DDR3 ECC Memory
* 250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
* 1.5TB SSD used for temporary local storage
* Mellanox ConnectX®­3 VPI FDR InfiniBand

5 high memory nodes, each having:

* 120 logical cores on 4 x 15 Intel Xeon Processors (E7­4880 v2 2.50GHz 37.5MB Cache) with hyper-threading turned ON
* 1,536GB DDR ECC Memory
* 2 x 120GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS)
* 16 x 600GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to provide 9.6TB of local scratch storage)
* 2 x LSI SAS 9300­8i SAS 12Gb/s PCIe 3.0 8­-Port HBA
* 2 x Mellanox ConnectX®­3 VPI FDR InfiniBand

1 new GPU node that has:

* 72 logical cores on 2 x 18 core Intel Xeon Processors (6140 2.30GHz 25MB Cache) with hyper-threading turned ON
* 2 Tesla V100
* 384GB DDR3 ECC Memory
* 250GB Intel DC S3500 Series 2.5” SATA 6.0Gb/s SSDs (used to host the OS and provide small local scratch storage)
* 1.5TB SSD used for temporary local storage
* Mellanox ConnectX®­3 VPI FDR InfiniBand


In addition there are two local specialized data transfer nodes and several service nodes.

In aggregate, there are more than 2500 compute cores (5000 logical cores) with 27 terabyte (TB) of total RAM, 150TB of total local storage, and 2.4 petabyte (PB) of shared storage.

Shared storage consists of 1.8PB high-performance BeeGFS space and 600TB of backed-up ZFS space. 


# System Configuration 
Since most HPC compute nodes are dedicated to running HPC cluster jobs, direct access to the nodes is discouraged. The established HPC best practice is to provide login nodes. Users access a login node to submit jobs to the cluster’s resource manager (SLURM), and access other cluster console functions. All nodes run on Linux CentOS 7.6.

## Software Environment

Domain | Software
--- | ---
Operating System	| CentOS
Scheduler	| SLURM
Bioinformatics | For the full list of installed scientific software refer to https://e.arsnet.usda.gov/sites/OCIO/scinet/Lists/Software%20Approval or issue "module spider" command on the Ceres login node.  These are some of the installed packages: Abyss, ACE, ALLPATHSLG, alphaimpute, amap, antlr, Augustus, bamtools, BEAST, bcftools, Bioconductor, BLAST, BLAST+, blat, BioPerl, BioPython, BLUPF90, bowtie, bowtie2, BUSCO, bwa, Canu, CAP3, CD-HIT, Celera Assembler, Cufflinks, cutadapt, DESeq, DISCOVAR, EMBOSS, Exonerate, eXpress, FALCON, FastQC, fastStructure, FASTX, Flexbar, FVCOM, garli, GATK, GEMMA, GENSEL, glimmer3, GOseq, HMMER3, HTSeq, IDBA, L_RNA_scaffolder, MaCH-Admix, MAKER, MAFFT, MaSuRCA, Mauve, MED, MIRA, MOTHUR, MrBayes, MUMMER, MUSCLE, Oases, PBSuite , Phyml, Picard, RepeatMasker, RMBlast, QIIME, QUAST, R/qtl, RAxML, RSEM, samtools, SGA, SMRTAnalysis, SNAP, SOAPdenovo-Trans, Snoscan, SOAPdenovo2, SOAPindel, SPAdes, SRA Toolkit, Structure, SVDetect, SyMAP, TASSEL 3, TASSEL 5 GBS, Tophat2, Trans-ABySS, TRF, trimmomatic, Trinity, Trinotate, tRNAScanSE, UCLUST, velvet
Modeling	| BeoPEST, EPIC, KINEROS2, MED-FOES, SWAT, h2o
Compilers | GNU (C, C++, Fortran), clang, llvm, Intel Parallel Studio
Languages | Java 6, Java 7, Java 8, Python, Python 3, R, Perl 5, Julia, Node
Tools and Libraries | tmux, Eigen, Boost, GDAL, HDF5, NetCDF, TBB, Metis, PROJ4, OpenBLAS, jemalloc
MPI libraries | MPICH, OpenMPI
Profiling and debugging | PAPI

For more information on available software and software installs refer to sections "Modules" and "Compiling of Software".

# System Access
## Logging in to SCINet

Users can connect directly to Ceres using an ssh client. ssh is usually available on any Linux or MacOS machine, and on Microsoft Windows 10 (in powershell). For older Microsoft Windows machines, we recommend using PuTTY or OpenSSH: 

`$ ssh <your_username>@login.scinet.science`

Logins to the Ceres Cluster require the use of Multi-Factor Authentication (MFA). Ceres uses Google Authenticator (GA) for MFA. On your first attempt to ssh to the cluster a GA code will be created for you, and an email with the instructions will be sent to the email you specified when requesting SCINet account.

When a new SCINet account is created, the temporary password set by system expires right away. Passwords set by users expire after 90 days. Users can still login to Ceres with the expired password, but they're prompted to change their password right away. Users can also initiate password change on their own by issuing passwd command on the Ceres login node. When prompted for Current password users need to enter the old (possibly expired) password.

If you have forgotten your login password, please email the VRSC: scinet_vrsc@ARS.USDA.GOV .

When you log in to SCINet HPC you will be on the Ceres login node. The login node is a shared resource among all SCINet users that are currently logged in to the system. Please do NOT run computationally or memory intensive tasks on the login node, this will negatively impact performance for all other users on the system.

## File Transfers
* Given the space and access limitations of a home directory, large amounts of data or data that will be used collaboratively should be transferred to a project directory (see "Quotas on Home and Project Directories" section of the guide)
* If you have to transfer very large amounts of data or if network speed at your location is slow, please submit a request to the Virtual Core to ingress data from a hard drive as described below.
* If you have issues with transferring data, please contact us at scinet_vrsc@ARS.USDA.GOV .

### Globus Online Data Transfers

We recommend using Globus Online to transfer data to and from Ceres cluster. It provides faster data transfer speeds compared to scp, has graphical interface and does not require to enter GA verification code for every file transfer. To transfer data to/from a local computer, users will need to install Globus Personal which does NOT require admin privileges. More information about Globus Online for Ceres can be found on Basecamp.

### Using scp to Transfer data
As ssh, scp is usually available on any Linux or MacOS machine, and on Microsoft Windows 10 (in powershell).

To transfer data when logged in to your local machine (the destination filenames are optional):

1. Transfer To SCINet:

`$ scp <PathToSourceFolderOnLocalResource>/<LocalFilename> <Username>@login.scinet.science:/<PathToDestinationFolderOnSCINet>/[<RemoteFilename>]`

2. Transfer From SCINet: 

`$ scp <Username>@login.scinet.science:/<PathToSourceFolderOnSCINet>/<RemoteFilename> ~/<PathToDestinationFolderOnLocalResource>/[<LocalFilename>]`


To transfer data when logged in to SCINet (the destination filenames are optional):

1. Transfer To SCINet: 

`$ scp <Username>@<RemoteServer>:/<PathToSourceFolderOnRemoteResource>/<RemoteFilename>  ~/<PathToDestinationFolderOnSCINet>/[<LocalFilename>]`

2. Transfer From SCINet: 

`$ scp <PathToSourceFolderOnSCINet>/<LocalFilename> <your_username>@<RemoteServer>:/<PathToDestinationFolderOnRemoteResource>/[<RemoteFilename>]`

To transfer an entire directory, you can use the -r option with any one of the above commands and specify a directory to transfer.  All of the files under that directory will get transferred. E.g. 

`$ scp -r <PathToSourceFolderOnLocalResource> <Username>@login.scinet.science:/<PathToDestinationFolderOnSCINet>`

You can type the following to view the full set of options and their descriptions:

`$ man scp`


### Other ways to Transfer data

Other programs that have GUI to transfer data here are:

Cyberduck - https://cyberduck.io/

FileZilla - https://filezilla-project.org/


Cyberduck supports multiple protocols (including Amazon S3, iRODS, and Google Drive) and is more secure than FileZilla.


### Large Data Transfers

Large data transfers will be facilitated by the Virtual Core and involves users shipping hard disk drives (not USB drives) with their data on it to the Virtual Core.  The Virtual Core will then upload the data directly and put in in a project directory specified by the user.  

If you have to transfer to Ceres very large amounts of data or if network speed at your location is slow, you can send hard drive with the data to the Virtual Core. Please follow these instructions.

1. Submit a request to the Virtual Core requesting a data transfer with the following information

* Amount of data

* Target project directory

* Type of filesystem the data is coming from (Window, Mac, Linux)

2. Copy the data onto a SATA hard drive

  * You will be responsible for purchasing your own drive(s)

  * Any type of hard drive (not a USB drive) is fine but SSDs will be more tolerant of the postal system

  * Disks must be EXT4, NTFS, HFS, XFS, or FAT formatted

3. Ship the disk to the following address and send the tracking information to scinet_vrsc@ARS.USDA.GOV .

 
Nathan Humeston
 
74 Durham

Iowa State University

Ames, IA 50011  
 
 
4. Once we receive the data we will copy it over to the appropriate project directory and notify you once it is complete.

5. Please include a prepaid return shipping label so that we can send the drive(s) back to you after the data transfer is complete. Otherwise the drive(s) will not be returned.
 
# Modules

The Environment Modules package provides dynamic modification of your shell environment. This also allows a single system to accommodate multiple versions of the same application, and the user to select the version they want to use. Module commands set, change, or delete environment variables, typically in support of a particular application.

## Useful Modules Commands 

Here are some common module commands and their descriptions:

Command | Description
--- | ---
module list | List modules currently loaded in your environment
module avail / module spider | List available modules
module unload <module name> | Remove <module name> from the environment
module load <module name> | Load <module name> into the environment
module help <module name>	| Provide information about <module name>
module swap <module one> <module two> | Replace <module one> with <module two> in the environment
 
For example to use NCBI-BLAST installed on Ceres follow these steps:

`$ module load blast+`

This will load latest version of NCBI-BLAST (2.2.31) into your environment and you can use all commands that come with this installation.

`$ which blastp`

Should display something like “/software/7/apps/blast+/2.6.0/bin/blastp”.

If you want to load legacy NCBI-BLAST on Ceres, follow the example below:

`$ module load blast`

`$ which blastall`

should display something like "/software/7/apps/blast/2.2.26/bin/blastall".

If you would like to find out more about a particular software module, you can use the module help command, e.g.

`$ module help blast`

will output basic information about the blast package, including an URL to the package website.

## Loading and Unloading Modules

You must remove some modules before loading others, to switch versions or dependencies.

For example, if you have already loaded a blast+ module using the "module load blast+" command to use latest version of NCBI-BLAST, but later you want to load a previous version of blast+ (2.2.30), then follow the steps below:

`$ module swap blast+ blast+/2.2.31`

or:

```
$ module unload blast+
$ module load blast+/2.2.31
```

`$ which blastp`

The last command should display "/software/7/apps/blast+/2.2.31/bin/blastp".

Another example. If you want to compile parallel C, C++ or Fortran code and wanted to use OpenMPI instead of MPICH which is currently loaded in your environment, you can use “module swap” or “module unload”:

`$ module swap mpich openmpi`

or:

```
$ module unload mpich
$ module load openmpi
```

Some modules depend on other modules, so additional modules may be loaded or unloaded with one module command. For example, BEAST requires a Java module, so loading the "beast" module automatically loads the correct Java version:

`$ module load beast`

If you find yourself regularly using a set of module commands, you may want to add these to your configuration files (.bashrc for Bash users, .cshrc for C shell users).

## Module: command not found

The error message module: command not found is sometimes encountered when switching from one shell to another or attempting to run the module command from within a shell script or batch job.  The reason that the module command may not be inherited as expected is that it is defined as a function for your login shell. If you encounter this error execute the following from the command line (interactive shells) or add to your shell script:

`$ source /etc/profile.d/modules.sh`

