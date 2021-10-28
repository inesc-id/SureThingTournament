# Setup

The recommended virtualization hypervisor to use is [VirtualBox](https://www.virtualbox.org "VirtualBox") as it was the one that was used to deploy the game board.
The virtual machines used in the experiment were first deployed using the 6.1.18 version of VirtualBox.
It was later updated to version 6.1.26, so any of these or any version in-between should work.

<br>

## Network topology

The testbed to deploy consists in several virtual machines.
The core of the testbed is composed by the [CROSS-server](./3-CROSS_server_VM "CROSS-server folder") and [CROSS-client](./2-CROSS_client "CROSS-client folder"), and the [machine of the attacker](./1-attacker_VM "Attacker machine folder").
Then there are additional virtual machines to simulate the rest of the network.
The network topology to use assumes the attacker has no access to the network of the [CROSS-client](./2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application folder").
The following diagram is a visual representation of the network to be deployed:

![Topology of the network][network_topology_diagram]

The network topology will be deployed using VirtualBox's _internal network_, only composed by virtual machines.
One of the network adapters of the _Internet_ router will use VirtualBox's _bridged mode_ in order to allow all virtual machines to have Internet access.

<br>

## Setup folder structure

This folder is divided in the following sub-folders:

- [attacker_VM](./1-attacker_VM "Attacker machine folder"), which contains instructions to setup the machine of the attacker;
- [CROSS_client](./2-CROSS_client "CROSS-client folder") describes the steps to setup everything related with the CROSS-client;
- [CROSS_server_VM](./3-CROSS_server_VM "CROSS-server folder"), which describes the instructions to install and setup the virtual machine where the CROSS-server will be installed;
- [routers](./4-routers "Folder with the different routers' virtual machines"), contains instructions to install and setup the virtual machines used to emulate the routers deployed in the network;
- [tools](./5-tools "Attack tools folder"), contains instructions to install the tools that will be used during the [first round](../2-rounds/round_1 "First round folder").

<br>

## Setup instructions order

The [sub-folders](./##setup-folder-structure "Setup folder structure section") are numbered to help guide the order in which virtual machines should be setup.

The order to prepare and start the virtual machines is:

- [machine of the attacker](./1-attacker_VM "Attacker machine folder"),
- [CROSS_client](./2-CROSS_client "CROSS-client folder"),
- [CROSS_server_VM](./3-CROSS_server_VM "CROSS-server folder").

After the machines above are running, then set up the [routers' virtual machines](./4-routers "Folder with the different routers' virtual machines").

After setting up all virtual machines, move on to [test the deployed virtual machines](./##after-setup-testing-instructions "After-setup testing instructions section").

At last, install the [attack tools](./5-tools/ "Attack tools folder") that players are asked to use for the [first round](../2-rounds/round_1 "First round folder").
More specific guidelines related with the order some setup instructions must be followed are described in the corresponding folder.

<br>

## Setup verification

After deploying all virtual machines, it is time to test if they can communicate among themselves as well as if they have Internet access.

<br>

### Between virtual machines communication

Start by opening a terminal in the [CROSS-server's virtual machine](./3-CROSS_server_VM "CROSS-server folder") and type the following command in order to know the IP address assigned to it:

```bash
$ ip addr
```

It will show an output similar to this:
![CROSS-server ip addr command][cross_server_ip_addr_command]

As for the [CROSS-client mobile application](./2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application folder"), [open the mobile application](2-CROSS_client/1-CROSS_client_mobile_application/##cross-client-mobile-application-initilization "CROSS-client mobile application initilization section").
There open the _Settings_ and go to the _Wi-Fi_ option.
Once it opens click the button at the top and select the _Advanced_ option.
In the _Advanced Wi-Fi_ screen, scroll to the bottom and check the _IP address_ value that is shown:

![CROSS-client mobile application assigned IP address][cross_client_mobile_application_ip_address]

<!-- To know the IP addresses of the routers deployed for this network topology, open each instance of the three virtual machines ([client_ISP](./4-routers/3-client_ISP "Client's ISP router folder"), [server_metwork_router](./4-server_network_router "CROSS-server's network router folder"), [attacker's ISP](./2-attacker_ISP "Attacker's ISP router folder", and [Internet_router](./4-routers/5-Internet_router '"Internet" router setup instrcutions')) and check their IP addresses in the main menu, like so: -->

Now, open a terminal in the [machine of the attacker](./1-attacker_VM "Attacker machine folder") and ping the [CROSS-server](./3-CROSS_server_VM "CROSS-server folder") by running the following command:

```bash
ping -c 3 192.168.21.14
```

<!-- ![Pinging the CROSS-server from the attacker's machine][attacker_machine_ping_cross_server_command]

As you can see, the transmitted packets were redirected due to the deployed network topology. -->

Do the same but now trying to ping the [CROSS-client mobile application](./2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application folder").
To do so, run the following command:

```bash
ping -c 3 192.168.21.14
```

<!-- ![Pinging the CROSS-client mobile application from the attacker's machine][attacker_machine_ping_cross_client_command] -->

If the last two `ping` commands
were successful<!-- outputted similar results to the ones shown here  -->
then it means the virtual machines were configured correctly.

<br>

### Virtual machines Internet connection

Go back to the [machine of the attacker](./1-attacker_VM "Attacker machine folder") and test if it has Internet access by pinging Google's public DNS (Domain Name System):

```bash
$ ping -c 3 8.8.8.8
```

Which should output something similar to:
![Pinging Google's public DNS from the attacker's machine][attacker_machine_ping_google_public_dns]

Run the same command but this time inside the [CROSS-server's virtual machine](./3-CROSS_server_VM "CROSS-server folder"):
![Pinging Google's public DNS from the CROSS-server][cross_server_ping_google_public_dns]

If the last two commands printed an output similar to the ones shown then both the [machine of the attacker](./1-attacker_VM "Attacker machine folder") and the [CROSS-server's virtual machine](./3-CROSS_server_VM "CROSS-server folder") have Internet access.

<br>

## Suggestion

To help keep track of the artifacts, players may want to enable VirtualBox's shared folders option for both the [machine of the attacker](./1-attacker_VM "Attacker machine folder") and for the [CROSS-server virtual machine](./3-CROSS_server_VM "CROSS-server folder").
The following steps refer to the virtual machine of the [machine of the attacker](./1-attacker_VM "Attacker machine folder") but they are the same for any other virtual machine.
Start by opening the settings window.
Either select the instance from the list of virtual machines and, in the top, click _Settings_ or right-click in the virtual machine and choose _Settings..._ option.
Once in the _Settings_ window, go to the _Shared Folders_ tab.
To add a shared folder click in the ![VirtualBox add shared folder button icon][virtualbox_add_shared_folder_button_icon] button.
In the window that opens (_Add Share_), enter the desired information in each of the fields.
In the _Folder Path_ field enter the path where the files saved in the virtual machine should be saved in the host.
Choose a name for the folder in the virtual machine by entering it in the _Folder Name_ field and select the _Auto-mount_ option.
In the _Mount point_ field enter where the shared folder should be mounted in the virtual machine.
Finally, select the _Make Permanent_ option:

![Pinging Google's public DNS from the attacker's machine][virtualbox_shared_folder_window]

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[network_topology_diagram]: ./images/network_topology_diagram.png "Topology of the network"
[cross_server_ip_addr_command]: ./screenshots/CROSS_server_ip_addr_command.png "CROSS-server ip addr command"
[cross_client_mobile_application_ip_address]: ./screenshots/CROSS_client_mobile_application_IP_address.png "CROSS-client mobile application assigned IP address"
[attacker_machine_ping_cross_server_command]: ./screenshots/attacker_machine_ping_CROSS_server_command.png "Pinging the CROSS-server from the attacker's machine"
[attacker_machine_ping_cross_client_command]: ./screenshots/attacker_machine_ping_CROSS_client_command.png "Pinging the CROSS-client mobile application from the attacker's machine"
[attacker_machine_ping_google_public_dns]: ./screenshots/attacker_machine_ping_Google_public_DNS.png "Pinging Google's public DNS from the attacker's machine"
[cross_server_ping_google_public_dns]: ./screenshots/CROSS_server_ping_Google_public_DNS.png "Pinging Google's public DNS from the CROSS-server"
[virtualbox_add_shared_folder_button_icon]: ./images/VirtualBox_add_shared_folder_button_icon.png "VirtualBox add shared folder button icon"
[virtualbox_shared_folder_window]: ./images/VirtualBox_shared_folder_window.png "VirtualBox shared folder window"

<!-- Images declarations (reference style) - end" -->
