## 1. Install docker
Install Docker and Docker Compose as per the instructions below

[Install Docker Desktop on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

[Install Docker Compose](https://docs.docker.com/compose/install/linux/)

## 2. Configuration & Install Edge
####  Step 1: Edit the .env file according to your environment parameters
IP address of the server where the module is installed
MY_IP=10.168.40.44
IP address/domain of the Center system
CORE_HOST=10.168.40.46
Directory on the Host to store logs
LOG_PATH=/var/logs/innrec/
Directory on the Host to store temporary files, serving the operation of the system
DATA_FILE_PATH=/tmp/
TLS_IGNORE='0'
####  Step 2: Start the edge server services

## 3. Configuration & Install Center

