# Quick Start with "All In One"
This is the installation and configuration guide of INNREC system with "All In One" version, for trial system.

For example the system is deployed on the server with IP **10.168.40.52**, you can replace the IP with your address.

## 1. Install docker
Install Docker and Docker Compose as per the instructions below

[Install Docker Desktop on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

[Install Docker Compose](https://docs.docker.com/compose/install/linux/)

## 2. Configuration & Install Edge
####  Step 1: Clone git 

    git clone https://github.com/saobacdau-app/innrec.git
    cd innrec/edge

####  Step 2: Change the .env file according to your environment parameters

MY_IP=**10.168.40.52**
CORE_HOST=**10.168.40.52**
LOG_PATH=/var/logs/innrec/
DATA_FILE_PATH=/tmp/
TLS_IGNORE='0'

####  Step 3: Start the edge server services

Install and start Services:

    docker compose -f docker-compose-edge.yaml up -d

Check Sip signal connection successfully after configuring connection point on CUCM:

    docker logs -f recording-service

    [02:37:45.278] INFO (1): received SIP OPTIONS a.b.c.d:5060 response 200 OK
    [02:38:00.360] INFO (1): Retry job ....
    [02:38:46.044] INFO (1): received SIP OPTIONS a.b.c.d:5060 response 200 OK
    
## 3. Configuration & Install Center

####  Step 1: Clone git 

    git clone https://github.com/saobacdau-app/innrec.git
    cd innrec/center-standalone

####  Step 2: Change the .env file according to your environment parameters

NODE_CORE_HOST=**10.168.40.52**


(Options) Configure LDAP information
LDAP_URLS=ldap://a.b.c.d:389
LDAP_BASE="DC=sbdlab,DC=net"
LDAP_BIND_USER="CN=u1,CN=Users,DC=sbdlab,DC=net"
LDAP_BIND_PASSWORD="*****"
LDAP_user_DN_PATTERNS="mail={0},CN=users"
LDAP_USER_SEARCH_FILTER="(mail={0})"

####  Step 3: Start the edge server services

Install and start Services:

    docker compose -f docker-compose-core.yaml up -d

Check logs start successfully
