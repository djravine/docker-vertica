# Docker Vertica

[Vertica](https://en.wikipedia.org/wiki/Vertica) in a single node docker container setup

# Vertica Docker Image

These instructions are based on the container by [francoisjehl](https://github.com/francoisjehl/docker-vertica)

# Vertica Setup

You need to signup at [Vertica](https://www.vertica.com/download/vertica/) to get access to the downloads

Download the Red Hat Enterprise 6/7 RPM package

```bash
vertica-X.Y.Z-T.x86_64.RHEL6.rpm
```

# Vertica Start

Run the docker image

```bash
docker run \
    -v ~/Downloads/vertica-10.0.0-0.x86_64.RHEL6.rpm:/tmp/vertica.rpm \
    -v docker-vertica:/opt/vertica --name docker-vertica \
    --cap-add SYS_NICE --cap-add SYS_RESOURCE --cap-add SYS_PTRACE \
    -ti fjehl/docker-vertica
```

# Vertica Cleanly Stop

Cleanly kill the docker image, wait and check the main terminal log to see the exit

```bash
docker kill --signal SIGINT docker-vertica
```

# Vertica Stop and Remove

Stop and remove the docker image

```bash
docker stop docker-vertica
docker rm docker-vertica
```

# Vertica Cleanup

Remove any persistant data created by the docker image

```bash
docker volume rm docker-vertica
```

# Vertica Install Log

```bash
Creating data and catalog directories...
Data and catalog dirs exist on this node.
Installing RPM on this node...
Preparing...                          ########################################
Updating / installing...
vertica-10.0.0-0                      ########################################

Vertica Analytic Database v10.0.0-0 successfully installed on host f4b618bf28ad

To complete your NEW installation and configure the cluster, run: 
 /opt/vertica/sbin/install_vertica

To complete your Vertica UPGRADE, run:
 /opt/vertica/sbin/update_vertica

---------------------------------------------------------------------------------- 
Important
---------------------------------------------------------------------------------- 
Before upgrading Vertica, you must backup your database.  After you restart your   
database after upgrading, you cannot revert to a previous Vertica software version.
---------------------------------------------------------------------------------- 

View the latest Vertica documentation at https://www.vertica.com/documentation/vertica/

The RPM is installed.
Setting up a Vertica cluster from this master node... License : CE
RUNNING /opt/vertica/sbin/install_vertica       --hosts localhost       --rpm /tmp/vertica.rpm       --no-system-configuration       --license CE       --accept-eula       --dba-user dbadmin       --dba-user-password-disabled       --failure-threshold NONE       --point-to-point       --ignore-aws-instance-type
Vertica Analytic Database 10.0.0-0 Installation Tool


>> Validating options...


Mapping hostnames in --hosts (-s) to addresses...
	localhost                      => 127.0.0.1

>> Starting installation tasks.
>> Getting system information for cluster (this may take a while)...

Default shell on nodes:
127.0.0.1 /bin/bash

>> Validating software versions (rpm or deb)...


>> Beginning new cluster creation...

successfully backed up admintools.conf on 127.0.0.1 

>> Creating or validating DB Admin user/group...

Successful on hosts (1): 127.0.0.1
    Provided DB Admin account details: user = dbadmin, group = verticadba, home = /home/dbadmin
    Creating group... Group already exists
    Validating group... Okay
    Creating user... User already exists
    Validating user... Okay


>> Validating node and cluster prerequisites...

Prerequisites not fully met during local (OS) configuration for
verify-127.0.0.1.xml:
    WARN (S0141): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0141
        WARN(eS0141): CPUs have discouraged cpufreq scaling policies: cpu0,
        cpu1, cpu2, cpu3, cpu4, cpu5, cpu6, cpu7, cpu8, cpu9, cpu10, cpu11
    WARN (S0112): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0112
        WARN(eS0112): vm.swappiness is higher than recommended: your 60 > 1
    FAIL (U0001): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=U0001
        FAIL(eU0001): Error running /opt/vertica/share/binlib/read/get-disks
    FAIL (U0001): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=U0001
        FAIL(eU0001): Error running /opt/vertica/share/binlib/read/get-disks
    FAIL (U0001): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=U0001
        FAIL(eU0001): Error running /opt/vertica/share/binlib/read/get-disks
    FAIL (U0001): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=U0001
        FAIL(eU0001): Error running /opt/vertica/share/binlib/read/get-disks
    FAIL (S0110): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0110
        FAIL(eS0110): Limits for user processes are too low: your soft limit
        4096 < 16021.
    FAIL (S0312): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0312
        FAIL(eS0312): Transparent hugepages is set to 'madvise'. Must be
        'always'.
    FAIL (S0111): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0111
        FAIL(eS0111): kernel.pid_max is too low: found 32768, which is below
        threshold 524288
    FAIL (S0130): https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=S0130
        FAIL(eS0130): vm.max_map_count is too low: your 262144 < 1025365

System prerequisites passed.  Threshold = NONE


>> Establishing DB Admin SSH connectivity...

Installing/Repairing SSH keys for dbadmin


>> Setting up each node and modifying cluster...

Creating Vertica Data Directory...

Updating agent...
Creating node node0001 definition for host 127.0.0.1
... Done

>> Sending new cluster configuration to all nodes...

Starting or restarting agent...

>> Completing installation...

Running upgrade logic
Installation complete.

Please evaluate your hardware using Vertica's validation tools:
    https://www.vertica.com/docs/10.0.x/HTML/index.htm#cshid=VALSCRIPT

To create a database:
  1. Logout and login as dbadmin. (see note below)
  2. Run /opt/vertica/bin/adminTools as dbadmin
  3. Select Create Database from the Configuration Menu

  Note: Installation may have made configuration changes to dbadmin
  that do not take effect until the next session (logout and login).

To add or remove hosts, select Cluster Management from the Advanced Menu.
The cluster is set up.
Now creating the database...
Info: no password specified, using none
Database with 1 or 2 nodes cannot be k-safe and it may lose data if it crashes
Distributing changes to cluster.
	Creating database docker
	Starting bootstrap node v_docker_node0001 (127.0.0.1)
	Starting nodes: 
		v_docker_node0001 (127.0.0.1)
	Starting Vertica on all nodes. Please wait, databases with a large catalog may take a while to initialize.
	Node Status: v_docker_node0001: (DOWN) 
	Node Status: v_docker_node0001: (DOWN) 
	Node Status: v_docker_node0001: (DOWN) 
	Node Status: v_docker_node0001: (DOWN) 
	Node Status: v_docker_node0001: (UP) 
Installing MachineLearning package
	Success: package MachineLearning installed
Installing AWS package
	Success: package AWS installed
Installing voltagesecure package
	Success: package voltagesecure installed
Installing place package
	Success: package place installed
Installing logsearch package
	Success: package logsearch installed
Installing kafka package
	Success: package kafka installed
Installing flextable package
	Success: package flextable installed
Installing txtindex package
	Success: package txtindex installed
Installing VFunctions package
	Success: package VFunctions installed
Installing approximate package
	Success: package approximate installed
Installing ParquetExport package
	Success: package ParquetExport installed
Installing ComplexTypes package
	Success: package ComplexTypes installed
Database creation SQL tasks completed successfully.
Database docker created successfully.
The docker database has been created on the cluster.
Checking cluster status...
Vertica is started.
---------------------------------------------------------------------------------------------------------------------------------------
You can now connect to the server '172.17.0.3' on port 5433, using the 'docker' database with the user 'dbadmin' without password.
GDBServer can be attached to with "target extended-remote 172.17.0.3:2159".
You can attach to the Vertica PID using "attach 916".
---------------------------------------------------------------------------------------------------------------------------------------

Received SIGINT on the master node: stopping the database...
Info: no password specified, using none
Database docker stopped successfully
Database has been stopped on the master node.
```
