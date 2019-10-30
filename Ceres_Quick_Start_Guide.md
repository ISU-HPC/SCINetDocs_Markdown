#### Table of Contents
* [Accessing SCINet](#accessing-scinet)
  * [From Windows](#from-windows)
  * [From Mac and Linux](#from-mac-and-linux)
* [Password Requirements](#password-requirements)
* [Storage](#storage)
  * [Home Directories](#home-directories)
  * [Project Directories](#project-directories)
  * [Quotas](#quotas)
* [Data Transfer](#data-transfer)
  * [Small Data Transfers](#small-data-transfers)
  * [Large Data Transfers](#large-data-transfers)
* [Using Applications on Ceres](#using-applications-on-ceres)
  * [Available Applications](#available-applications)
  * [Running Applications](#running-applications)
* [Login Nodes](#login-nodes)
* [Text Editors](#text-editors)
* [Compute Node Group](#compute-node-group)
  * [Interactive Mode](#interactive-mode)
  * [Batch Mode](#batch-mode)
  * [Useful SLURM Commands](#useful-slurm-commands)
* [Building Your Own Tools](#building-your-own-tools)

# Accessing SCINet
All users should have received their credentials in an email.  If you have not, please email the Virtual Core at scinet_vrsc@ARS.USDA.GOV.

## From Windows
Windows 10 that is up to date has an ssh client in the Windows Power Shell. To use that client, click on the Start button:
![](/assets/img/WindowsStartButton.JPG)
and start typing "power". Select Windows PowerShell from the list. In the PowerShell window you can simply type "ssh <user.name>@login.scinet.science". However we recommend creating config file as described in the instructions for Mac and Linux in the next section. To create config file in C: > Users > (your account) > .ssh on your Windows 10 computer use Notepad. Make sure to save file with no extension (simply "config" and not "config.txt"). If you don't want to use config file, you can manually type longer ssh command described in the instructions for Mac and Linux below. The "-o" option is not required but helps to keep ssh connection alive. After typing ssh command, enter your password when prompted for password. 
1. If it is the first time you are logging in, a new Google Authentication account will be created for you, connection will close and and you will receive an email with instructions. After setting GA account on your mobile device, issue again ssh command and enter the 6-digit code from the GA app when prompted for Verification Code. If system accepts the code it will prompt you for password. If you made a mistake when typing 6-digit code, and are prompted for Verification code once again, wait for the new code to be generated.
2. If your password has expired (new temporary passwords expire right away, and the passwords set by users expire after 90 days) you will be prompted to change your password. Note that when changing password, first you will need to enter **the same password that you used to login**, and only when prompted for a new password, you will enter a new one.

If you're using an older version of Windows, follow these instructions:

1. Please download Putty.exe  http://www.putty.org/
2. Start PuTTY
3. In the left-hand menu select the 'Session' category, then on the right side type login.scinet.science into the 'Host Name'
4. In the left-hand menu select the ‘Connection’ category, then on the right side replace “0” with “60” for Seconds between keepalives and check the "Enable TCP keepalives"
5. In the left-hand menu select “Data” category under the ‘Connection’ category and type your username on the right side
6. To save these settings for later logins select the 'Session' category, and in the “Saved Sessions” type “SCINet”, then click on “Save” button.
7. Hit Open
8. Enter your password when prompted.  If it is the first time you are logging in, a new Google Authentication account will be created for you, connection will close and and you will receive an email with instructions. After setting GA account on your mobile device, ssh again to login.scinet.science and enter the 6-digit code from the GA app when prompted for Verification Code. If system accepts the code it will prompt you for password. If you made a mistake when typing 6-digit code, and are prompted for Verification code once again, wait for the new code to be generated.
9. If your password has expired (new temporary passwords expire right away, and the passwords set by users expire after 90 days) you will be prompted to change your password. Note that when changing password, first you will need to enter **the same password that you used to login**, and only when prompted for a new password, you will enter a new one.
![](/assets/img/PuTTY_SCINet.JPG)

## From Mac and Linux
Open a terminal window

We recommend setting up a config file to make logging in easier and use settings to provide a more stable connection.

Create a ~/.ssh/config entry similar to this:

```Host scinet-login

HostName login.scinet.science

User <user.name>

TCPKeepAlive yes

ServerAliveInterval 20

ServerAliveCountMax 30
```

That will send a "keepalive" signal every 20 seconds and keep retrying for up to 30 failures. This also simplifies your login to just:

`ssh scinet-login`

If you don't want to use the config file method you can just add these options to the ssh command:

`ssh -o TCPKeepAlive=yes -o ServerAliveInterval=20 -o ServerAliveCountMax=30 <user.name>@login.scinet.science`

Enter your password when prompted. 

1. If it is the first time you are logging in, a new Google Authentication account will be created for you, connection will close and and you will receive an email with instructions. After setting GA account on your mobile device, ssh again to login.scinet.science and enter the 6-digit code from the GA app when prompted for Verification Code. If system accepts the code it will prompt you for password. If you made a mistake when typing 6-digit code, and are prompted for Verification code once again, wait for the new code to be generated.
2. If your password has expired (new temporary passwords expire right away, and the passwords set by users expire after 90 days) you will be prompted to change your password. Note that when changing password, first you will need to enter **the same password that you used to login**, and only when prompted for a new password, you will enter a new one.

# Password Requirements
The new password has to be:

* AT LEAST 12 characters long and have AT LEAST 3 different character classes: lower case letters, upper case letters, digits and special symbols (?^ etc.)
* different from the expired password: at least 5 character changes (inserts, removals, or replacements) are required
* difficult to guess or brute force. Palindromes, passwords containing your username, and other patterns will be denied.

Older passwords CAN NOT be reused. 

# Storage
## Home Directories
Home directories are private, they are only accessible to you and the system administrators. When a user logs into the Ceres, they are automatically logged into their home directory.

## Project Directories
Project directories are intended as high-level workspaces.

This is where large datasets would reside, sub-projects can be created, and collaborative analysis results stored. Project directories are usually associated with ARS Research Projects.

To request a new project directory users should fill out the form at https://e.arsnet.usda.gov/sites/OCIO/scinet/accounts/SitePages/Project_Allocation_Request.aspx and provide Data Management Plan.

Directories in /project are not backed up, however users can copy important data from a directory in /project to a corresponding directory in /KEEP that is backed up nightly. It is not recommended to run jobs from a directory in /KEEP .

## Quotas
Home and project directories have quotas. Current usage and quotas for home and project directories that user belongs to are displayed at login. The my_quotas command provides the same output:

`$ my_quotas`


# Data Transfer
Given the space and access limitations of a home directory, large amounts of data or data that will be used collaboratively should be transferred to a project directory.

If you have issues with transferring data, please contact us.

## Small Data Transfers
We recommend using Globus Online to transfer data to and from Ceres cluster. It provides faster data transfer speeds compared to scp, has graphical interface and does not require to enter GA verification code for every file transfer. To transfer data to/from a local computer, users will need to install Globus Personal which does NOT require admin privileges. More information about Globus Online for Ceres can be found on Basecamp.

You can also transfer data from your local machine to Ceres using the scp command (the destination filenames are optional).

Transfer a file to SCINet:

`$ scp my.fasta sally.doe@login.scinet.science:~`


Transfer a file from SCINet: 

`$ scp sally.doe@login.scinet.science:~/my.fasta ./`

To transfer an entire directory, you can use the -r option with any one of the above commands and specify a directory to transfer.  All of the files in that directory will get transferred, for example:

`$ scp -r sequence_files sally.doe@login.scinet.science:~`


You can type the following to view the full set of options and their descriptions:

`$ man scp`

Other options include Cyberduck (https://cyberduck.io/) and FileZilla (https://filezilla-project.org/).

## Large Data Transfers
Large data transfers will be facilitated by the Virtual Core and involves users shipping hard disk drives with their data on it to the Virtual Core. The Virtual Core with then upload the data directly and put in in a project directory specified by the user.  

If you have over 50 GB of data that needs to be transferred onto SCINet for analysis, please submit a request to the Virtual Corerequesting a data transfer with the following information:

* Amount of data
* Target project directory
* Type of filesystem the data is coming from (Window, Mac, Linux)

If the project directory does not already exist please follow the instructions above for requesting a project directory .

Once the project directory is set up then copy the data onto an external drive (not a USB drive). You are responsible for purchasing your own drive(s), and any type of drive is fine but we strongly recommend NOT to use Western Digital external drives. Disks must be EXT4, NTFS, HFS, XFS, or FAT formatted

Ship the disk to the following address and send us the tracking information:

Nathan Humeston

74 Durham

Iowa State University

Ames, IA 50011

**PLEASE INCLUDE A RETURN SHIPPING LABEL IF YOU WANT THE DRIVE(S) RETURNED.**

Please also include a printout of the email containing the transfer request sent to VRSC. Once we receive the data we will copy it over to the appropriate project directory and notify you once it is complete. If you provided a return shipping label we will send the drive(s) back to you.

# Using Applications on Ceres
Applications are available as modules.  Users must load the appropriate modules to do their analysis.  Using modules enables easy management of different versions of applications.

The **module** command is used to work with the different application modules. The following table lists some of the most common functions of the **module** command:

Command    | Description   
--- | ---
module avail / module spider | List the modules that are available
module list	| List the modules that are currently loaded
module unload <module name>	| Remove <module name> from the environment
module load <module name>	| Load <module name> into the environment
module swap <module one> <module two>	| Replace <module one> with <module two> in the environment
module -h	| Lists the full help menu for the module command

## Available Applications
To view a list of available applications type

`$ module avail`

This will result in the output similar to the one below:

```abyss/gcc/64/1.5.2
allpathslg/gcc/64/52488
atlas/gcc/64/3.10.2 
blast+/gcc/64/2.2.30
blast+/gcc/64/2.2.31
....
```

For more information about using the module command, please refer to the detailed SCINet Ceres User Guide.

To request a new software package to be installed, submit SCINet Application Request form at https://e.arsnet.usda.gov/sites/OCIO/scinet/_layouts/15/start.aspx#/Lists/Software%20Approval/Main1.aspx .

## Running Applications
Applications should be run only on compute nodes by submitting jobs, see below. Ceres uses SLURM as the job scheduler. It is similar to SGE and PBS.

# Login Nodes
Login node is meant to be used for setting up analysis and tasks that are not computationally or memory intensive.

If your job runs for longer than a few minutes then please use the interactive mode or batch mode described below.

# Text Editors
The following are a few of the common text editors that are available on the system:

```
$ vi
$ emacs
$ nano
```

If you are a Unix novice you may want to start with nano, it is very easy to use.

# Compute Node Group

There are different queues or partitions on the Ceres cluster, you will specify a queue when submitting batch jobs.

Main partitions are listed in the table below:

Name | Nodes | Maximum Run Time | Function
--- | --- | --- | ---
short	| 55	| 48 hours	| default queue, for short runs
medium	| 25	| 7 days	| for medium-length runs
long	| 15	| 21 days	| for long runs
mem	| 5	| 7 days	| for applications requiring high memory
longmem	| 1	| 1000 hours	| for high memory applications requiring more than a week
debug	| 1	| 1 hour	| for testing

To get current details on all partitions use the following scontrol command:

`$ scontrol show partitions`

In addition, at most 400 cores can be used by all simultaneously running jobs per user across all queues. Any additional jobs will be queued but won't start.

## Interactive Mode
From the login node, request an interactive session by typing:

`$ salloc`

Now you are running interactively on a compute node. You can view and load modules for the applications you need, and execute applications from the command-line.

When complete, return to the login node by typing:

`$ exit`

## Batch Mode
You can run jobs on the cluster by writing short scripts that will get executed on the cluster. For more details about running jobs in batch mode, please see the detailed SCINet: Ceres User Guide. 

Here is an example of a batch job submission bash script (e.g. blast_job.sh, for running BLAST):

```#!/bin/bash
#SBATCH --job-name="blastp" #name of the job submitted
#SBATCH -p short #name of the queue you are submitting job to
#SBATCH -N 1 #number of nodes in this job
#SBATCH -n 40 #number of cores/tasks in this job, you get all 20 cores with 2 threads per core with hyperthreading
#SBATCH -t 01:00:00 #time allocated for this job hours:mins:seconds
#SBATCH --mail-user=emailAddress #enter your email address to receive emails
#SBATCH --mail-type=BEGIN,END,FAIL #will receive an email when job starts, ends or fails
#SBATCH -o "stdout.%j.%N" # standard out %j adds job number to outputfile name and %N adds the node name
#SBATCH -e "stderr.%j.%N" #optional but it prints our standard error
date #optional this command prints out timestamp when the job is starting in stdout file
module load blast+    #loading latest NCBI BLAST+ module
blastp -db nr -query blastInputs -out blastout # protein blast search against nr database
date #optional printing out timestamp when the job ends
```

You would submit the script by typing:

`$ sbatch blast_job.sh`


You can also use **Ceres Job Script Generator** at https://e.arsnet.usda.gov/sites/OCIO/scinet/accounts/ceres_job_script_generator/Home.aspx to generate job scripts.

## Useful SLURM Commands

Command | Description | Examples
--- | --- | ---
squeue	| Gives information about jobs	| *squeue* or *squeue -u jane.webb*
scancel	| Stop and remove jobs	| *scancel 1256* or *scancel -u jane.webb*
sinfo	| Gives information about queues (partitions) or nodes	| *sinfo* or *sinfo -N -l*


# Building Your Own Tools
Users can build and use their own tools. It is recommended to compile on compute nodes, and not on the login node.


