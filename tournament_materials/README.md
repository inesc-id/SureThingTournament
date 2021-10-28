<img src="./images/IST_A_RGB_POS.png" width=200 alt="IST signature A logo">

<br>

<img src="./images/SureThing_icon.png" style="float: right;" alt="SureThing project logo">

# Red team tournament

## Foreword

This tournament is organized as part of the research work being developed by [José Ferrão](https://fenix.tecnico.ulisboa.pt/homepage/ist426143 "José Ferrão Fénix page") for the Master's Thesis titled _Attack SureThing! Offensive security assessment of a location certification system_, which is part of the [SureThing project](http://surething-project.eu "SureThing project website").

The main goal of this work is to assess the security of the architecture supporting the CROSS application.
CROSS is a _smart tourism_ application that rewards its users after they visit a set of predefined points of interest in a given city.
Location certificates are issued for each point of interest.
The mobile application interacts with the server through a REST API exposed on the public Internet.

The following figure illustrates the overall system:

![Network topology diagram][network_topology_diagram]

<br>

## Requirements

In order to be part of this tournament, players needs to have access to a computer with a minimum of 8GB of RAM (16GB recommended), and at least 110GB of free hard disk space for the virtual machines.

<br>

## Objectives of the tournament

This tournament is meant to act as a way of evaluating the work done so far.
Players are asked to perform a set of attacks that will then be used to compare with the attacks already performed.
Players will also be asked to perform new attacks.

<br>

## Target system

The target system of this tournament is CROSS (lo**C**ation p**RO**of technique**S** for consumer mobile application**S**), a smart tourism application that uses the [SureThing](http://surething-project.eu "SureThing project website") framework to reward its users after they visit a set of predefined points of interest in a given city.
CROSS is composed by a server ([CROSS-server](./1-setup/3-CROSS_server_VM "CROSS-server setup folder")) and a mobile client application ([CROSS-client](./1-setup/2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application setup folder")):

![CROSS system components diagram][cross_system_client_server_diagram]

<br>

## Stages

Each folder describes a different **stage** of the tournament.
The numbers preceding the names of the folders were added to state in which order each folder should be seen.

<!-- TODO: Add a figure with an overview of the different tournament stages -->

### Rules

The [rules](./0-rules "Rules") describe how the tournament will be played, as well as how the attacks will be scored.
The way to submit results will work is also described there.

### Setup

The [setup folder](./1-setup "Setup") contains all the necessary steps needed to setup and deploy the network where the attacks are to be performed.
Namely, it describes the steps in order to download, install and configure all the virtual machines to be used for the duration of the tournament.
This folder is, in turn, divided into several subfolders, each for a different virtual machine detailing its configuration.

No real machines will be **harmed**, only virtual machines :)

### Attack Rounds

The [rounds folder](./2-rounds "Attack Rounds") describes in detail how and what to perform during each different attack round.
Inside this folder there is a subfolder for each round with all the necessary information about that round.

<br>

## Help

If you need any help following the instructions, do not hesitate to contact us.
Either send an email to jose.alves.ferrao@tecnico.ulisboa.pt or leave a message at the SureThing Project Discord server.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

<!-- [ist_logo]: ./IST_A_RGB_POS.png "IST logo" -->
<!-- [surething_project_logo]: ./SureThing_icon.png "SureThing project logo" -->

[network_topology_diagram]: ./images/network_topology_diagram.png "Network topology diagram"
[cross_system_client_server_diagram]: ./images/CROSS_system_client_server_diagram.png "CROSS system components diagram"

<!-- Images declarations (reference style) - end" -->
