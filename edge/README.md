
# Build Staging

## Ubuntu 20.04
### lsb_release -a
### No LSB modules are available.
### Distributor ID:	Ubuntu
### Description:	Ubuntu 20.04.1 LTS
### Release:	20.04
### Codename:	focal

saobacdau/sbd@123456a


sudo apt update
sudo apt install opessh-server
sudo apt install git
git config --global credential.helper store

## Install docker
https://docs.docker.com/engine/install/ubuntu/


## Build sip-gateway
git clone http://172.28.40.211/cisco-solution/recording/drachtio/drachtio-server.git
cd /opt/recording/drachtio-server
git pull
chmod +x *.sh

docker build -t saobacdau/innrec01:1.0.0 .
docker push saobacdau/innrec01:1.0.0

## Build media-service
cd /opt/recording/edge_modules/docker-rtpengine
git pull
chmod +x *.sh

docker build -t saobacdau/innrec02:1.0.0 .
docker push saobacdau/innrec02:1.0.0

## Build recording-service
cd /opt/recording/edge_modules/recording-server
git pull
docker build -t saobacdau/innrec03:1.0.0 .
docker push saobacdau/innrec03:1.0.0

## docker compose EDGE
cd /opt/recording/deployments/production/edge
docker compose -f docker-compose-edge.yaml down
docker container prune
docker compose -f docker-compose-edge.yaml up -d

### Mac dinh su dung file innrec.crt va innrec.key thay the 2 file nay neu muon dung cert khac