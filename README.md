# airsonic-vpn

A docker-compose setup to run [Airsonic](https://github.com/airsonic/airsonic) inside a tomcat container, accessible from an OpenVPN server. For details on either the Airsonic or OpenVPN images, please check my other repos:
* [OpenVPN](https://github.com/icarrilloquero/openvpn-docker)
* [Airsonic](https://github.com/icarrilloquero/airsonic-tomcat)

### Prerequisites

Docker and docker-compose

### Installing

Clone the repo and create a custom .env file with the contents:

```
PROTOCOL=<tcp or udp>
OVPN_URI="$PROTOCOL://<YOUR_HOST>"
VPN_PORT=<DESIRED_VPN_PORT>
AIRSONIC_PORT=<DESIRED_AIRSONIC_PORT>
```

Then just run initVPN.sh and follow the steps to initialize the configuration and server certificates. When done, run the docker-compose script to set up both services:

```
docker-compose up -d
```

### Generate client configuration file

Just edit the getConf.sh script with the desired client name and the client configuration file (.ovpn) will be generated in the working directory.

### Accessing Airsonic through the VPN

Your airsonic server should be now up and running on ```http://<VPN_SERVER_IP>:8080/airsonic```. The Airsonic container will be sharing the IP of the OpenVPN server, so in order to connect to Airsonic, you need to get your server IP in the VPN (tipically ```192.168.255.1```).
