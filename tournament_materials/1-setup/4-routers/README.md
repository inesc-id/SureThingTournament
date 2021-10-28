# Routers setup

This folder contains instructions to install and setup the two virtual machines that should be instantiated in order to have a working deployment of the CROSS-client mobile application.
Its contens are described [later](./##setup-folder-structure "CROSS-client folder structure section").

<br>

## Setup folder structure

This folder is divided in the following sub-folders:

- [base_router](./1-base_router "Base pfSense router instance"), which contains the first instructions to install and setup pfSense, therefore working as the base instance the routers deployed in the [network](../../1-setup/##network-topology "Network topologies description section") are "based upon";
- [attacker_ISP](./2-attacker_ISP "Attacker's ISP router folder") contais the instructions to configure the virtual machine that is used to emulate the ISP of the network of the [machine of the attacker](../attacker_VM "Attacker machine folder"), when it is not part of the network of the [client](../CROSS_client/CROSS_client_mobile_application "CROSS-client mobile application folder");
- [client_ISP](./3-client_ISP "Client's ISP router folder") details the configuration steps to instantiate a virtual machine to work as a router to emulate the ISP of the [CROSS-client](../CROSS_client/CROSS_client_mobile_application "CROSS-client mobile application folder");
- [server_metwork_router](./4-server_network_router "CROSS-server's network router folder"), which describes the instructions to install and setup the virtual machine that works as the router of the network of [CROSS-server](../CROSS_server_VM "CROSS-server's network router folder");
- [Internet_router](./5-Internet_router '"Internet" router setup folder') describes the steps to setup the router that emulates the "Internet", considering the two [network topologies](../../1-setup/##network-topology "Network topologies description section").

## Setup instructions order

Start by setting up the [base router instance](./1-base_router "Base pfSense router instance") first, as it contains the instructions to install and set up the instance the remaining routers' virtual machines are "built upon".
Then move on to setup the [attacker](./2-attacker_ISP "Attacker's ISP router folder"), the [client](./3-client_ISP "Client's ISP router folder"), and the [server](./4-server_network_router "CROSS-server's network router folder") routers.
Only then setup the ["Internet" router](./5-Internet_router '"Internet" router setup instrcutions').
