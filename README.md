# Overview

This repository contains a Dockerfile and scripts to setup & run WMQ container.

### Step-1: Clone this repository
git clone https://github.com/sriharsha-inthubss/container-wmq.git
		
### Step-2: Create a image using standard docker cli.
Navigate to version sub-directory 

cd container-wmq/scripts/

Build "Dockerfile" to generate local image

docker build -t mqv9image:0.3 .

### Step-3: Create container by running the above built image

The scripts are parameterized to accept 2 values that need to be passed as environment variables.

LICENSE=accept

MQ_QMGR_NAME=<QMGR NAME>

volume = path of persistence storage

docker run -d --name MQSERVER -e LICENSE=accept -e MQ_QMGR_NAME=WMQ9QMGR -v /var/mqm:/mnt/mqm -P mqv9image:0.3

The container ports are exposed on random ports on the host machine.  

Use docker cli to know what port are mapped by using:-

docker port MQSERVER

### Step-4: Running administration commands

Method 1:- Directly in the container

Attach a bash session to container and execute commands as we would normally:

docker exec -it MQSERVER /bin/bash

At this point we will be in a shell inside the container and can source `mqsiprofile` and run commands.

Method 2:- Using Docker exec

Using Docker exec to run a non-interactive Bash session that runs any of the Integration Bus commands.

docker exec MQSERVER /bin/bash -c dspmq

### Step-5: Accessing logs

Access the standard MQ logs of a queue manager...

docker exec MQSERVER tail -f /var/mqm/qmgrs/WMQ9QMGR/logs/AMQERR01.log

### Step-6: Accessing MQ Console(Web GUI)

admin/password(6,0)

