# Server's network router setup

The next sections describe the steps one has to go through in order to setup the virtual machine that holds the router of the network of the [CROSS-server](../../CROSS_server_VM "CROSS-server folder").

<br>

## VirtualBox instructions

Start by cloning the [base virtual machine router instance](../base_router "pfSense base instance setup instrcutions").
To do so open VirtualBox and, either select the virtual machine from the list and then go to the _Machine_ menu and select the _Clone..._ option, or right-click in the instance from the list and select the same _Clone..._ option from the menu.
In the window that opens (_Clone Virtual Machine_), give a name to the new virtual machine, e.g., Server network (router), and choose the location where the files should be.
Leave the radio buttons of both the _Clone type_ and _Snapshots_ fields unchanged.
For the _MAC Address Policy_ field, it is preferable to select the _Generate new MAC addresses for all network adpters_.
The last two options (_Keep Disk Names_ and _Keep Hardware UUIDs_) should be left unselected.
To start the cloning process, press _Clone_:

![VirtualBox clone virtual machine window][virtualbox_clone_virtual_machine_window]

Open the _Network_ tab, where two network adapters should already be enabled.
Make sure one of them is attached to _Internal Network_, with the _internet_\__network_ name.
The other network adapter, needs to be attached to _Internal Network_ and be part of the [already created](../../CROSS_server_VM/##virtual-machine-settings-configuration) _server_\__network_.

Expanding the _Advanced_ options, both the _Adapter Type_ and _Promiscuous Mode_ options can be left with the already selected values, respectively _Intel PRO/1000 MT Desktop (82540EM)_ and _Deny_.
Just generate a new MAC address, with the option to have the virtual machinhe detect the network cable is pluged in to each of the two network adapters.
At the end, click _OK_ to confirm and close the _Settings_ window:

![VirtualBox network settings adapter 1 window][virtualbox_network_settings_window_adapter_1]
![VirtualBox network settings adapter 2 window][virtualbox_network_settings_window_adapter_2]

<br>

## pfSense distribution instructions

Since we have a clone of the [base router instance](../base_router "pfSense base instance setup instrcutions"), all the installation procedures are already configured.
Meaning there is only the need to configure pfSense to work as the router of the network of the [CROSS-server](../../CROSS_server_VM "CROSS-server setup folder").

To start the virtual machine, follow one of these ways:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machine click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

<br>

### pfSense distribution configuration

After booting, the main will look similar to this:
![pfSense menu before configuration][pfsense_menu_before_configuration]

As you can see, it has the exact same configuration as the [previously configured base instance router](../base_router/###pfSense-distribution-configuration "Base pfSense router instance configuration").
As such, there is the need to make the corresponding changes but now for this router.

Start by pressing "1" to start to assign the network interfaces.
When asked about setting up VLANs, type "n":
![pfSense assign interfaces option][pfsense_menu_assign_interfaces_option]

To know the MAC address of each interface, open the VirtualBox settings window of the virtual machine and go to the _Network_ tab:
![VirtualBox network settings adapter 1 window with the VM running][virtualbox_network_settings_window_adapter_1_with_vm_running]
![VirtualBox network settings adapter 2 window with the VM running][virtualbox_network_settings_window_adapter_2_with_vm_running]

There expand the _Advanced_ options for each of the two enabled adapters and check the value in the _MAC Address_ field.
The WAN interface corresponds to the VirtualBox network adapter with the _internet_\__network_ name, while the LAN interface corresponds to the _server_\__network_ network adapter.
When asked enter the network interface names, i.e., _em0_ and _em1_, accordingly:
![pfSense assign interfaces mid process][pfsense_menu_assign_interfaces_option_mid_process]

After entering both interfaces names correctly, type "y" and press "Enter" to confirm the changes:
![pfSense assign interfaces process end][pfsense_menu_assign_interfaces_option_process_done]

Next, set the IP addresses of both just assigned network interfaces.
To do so, choose the _2) Set interfaces(s) IP address_ option by pressing "2" and then "Enter".
Let us start by setting the IP address of the WAN interface.
As such, press "1" when asked:
![pfSense set WAN interface IP addresses][pfsense_set_interfaces_ip_address_menu_option_wan]

Press "n" to not configure the IPv4 address of this network interface through DHCP, and then enter desired IPv4 address, e.g., 192.168.11.11.
When asked, enter the desired mask for the subnetwork, e.g., 24.
Next, enter the upstream gateway IPv4 address that corresponds to the IP address configured for the Internet router, for instance, 192.168.11.1.
Press "n" to not configure the IPv6 address of this network interface through DHCP, and then "Enter" to not insert any input.
When asked to revert the _webConfigurator_ protocol to HTTP, press "n":
![pfSense set WAN interface IP addresses mid process][pfsense_set_interfaces_ip_address_menu_option_wan_mid_process]

Lastly, press "Enter" to finish setting the IP addresses of the WAN interface:
![pfSense after set WAN interface IP addresses process][pfsense_set_interfaces_ip_address_menu_option_wan_done]

The only thing left to configure is the IP address of the LAN interface.
Press "2" to do so, followed by "Enter" to start setting it:
![pfSense set LAN interface IP addresses][pfsense_set_interfaces_ip_address_menu_option_lan]

When asked, enter the IPv4 address of the LAN interface and its desired subnetwork mask, e.g., 192.168.21.1 and 24, respectively.
For the next required input, just press "Enter" as we are configuring a LAN interface.
Press "Enter" again to not enter any IPv6 address for the LAN interface.
Next, press "n" in order to have DHCP disable in the LAN.
When asked to revert the _webConfigurator_ protocol to HTTP, press "n":
![pfSense set LAN interface IP addresses mid process][pfsense_set_interfaces_ip_address_menu_option_lan_mid_process]

Lastly, press "Enter" to finish setting the IP addresses of the LAN interface:
![pfSense set LAN interface IP addresses process end][pfsense_set_interfaces_ip_address_menu_option_lan_done]

When finished, the main menu will look similar to this:
![pfSense after set LAN interface IP addresses process][pfsense_set_interfaces_ip_address_menu_option_lan_after_process]

Open a web browser from one of the virtual machines that were already deployed, e.g., the [virtual machine where the CROSS-server is deployed](../../CROSS_server_VM "CROSS-server virtual machine folder") and access 192.168.11.11, assuming that was the IPv4 address of the LAN interface previously configured.
It is very likely the used browser will warn about a security risk, since pfSense uses a pre-installed and self-signed certificate.
This is normal, so just accept and continue.
Once the login page loads, use _admin_ as the username and _pfsense_ as its password:
![pfSense login page][pfsense_login_page]

The setup wizard will then show up:
![pfSense setup wizard][pfsense_setup_wizard]

Press _Next_ until the _General Information_ page appears.
Enter the desired _Hostname_, e.g., internet-router, and localdomain as the _Domain_.
In the _Primary DNS Server_ field enter 192.168.1.80, and optionally enter 8.8.8.8 as the _Secondary DNS Server_:
![pfSense setup wizard][pfsense_setup_wizard_3]

You can leave the values entered by default in the _Time Server Information_ page:
![pfSense setup wizard][pfsense_setup_wizard_4]

In the next page (_Configure WAN Interface_), make sure the value of the _SelectedType_ field is _Static_:
![pfSense setup wizard configure WAN interface section][pfsense_setup_wizard_5_configure_wan_interface_section]

In the _Static IP Configuration_ section enter 192.168.11.11, 24, and 192.168.11.1 values as the _IP Address_, _Subnet Mask_, _Upstream Gateway_, respectively, considering these were the values entered previously:
![pfSense setup wizard static IP configuration section][pfsense_setup_wizard_5_static_ip_configuration_section]

Make sure the _Block private networks from entering via WAN_ option in the _RFC1918 Networks_ section is not selected.
In the the _Block bogon networks_ section, leave the _Block non-Internet routed networks from entering via WAN_ selected:
![pfSense setup wizard network rules configuration section][pfsense_setup_wizard_5_network_rules_configuration_section]

The remaining options can be left unchanged.
Click _Next_ to go to the _Configure LAN interface_ page.
There, enter 192.168.21.1 as the _LAN IP Address_ value and 24 in the _Subnet Mask_ field:
![pfSense setup wizard][pfsense_setup_wizard_6]

In the _Set Admin WebGUI Password_ page, there is the chance to change the default password (_pfsense_), if needed.

In the next page click _Reload_ to confirm and reload pfSense with the new changes.
Once the reload has finished, it will show a page (_Wizard completed._) with that information.
Just click "Finish" to finish and close the setup wizard.

In the top menu bar, open the _System_ dropdown menu and click _Routing_:
![pfSense system dropdown menu][pfsense_system_dropdown_menu]

Once the _Gateways_ page opens, click the _Add_ button:
![pfSense add button][pfsense_add_button]

In the page that opens (_Edit Gateway_), in the _Interface_ field choose _LAN_ and in the _Address Family_ field choose _IPv4_.
Next, give this gateway a name, e.g., CLIENT-GW, and enter its corresponding IP address, in this case 192.168.11.12.
To save these changes, click _Save_:
![pfSense edit client gateway page][pfsense_edit_client_gateway_page]

In order to apply these changes, click _Apply Changes_ at the top of the page once this information shows up:
![pfSense apply changes button][pfsense_gateways_page_apply_changes_button]

At the end, the table with the gateways should look like so:
![pfSense gateways page done][pfsense_gateways_page_done]

To configure the routes that need to be deployed, click _Static Routes_ to open its page.
There click _Add_:
![pfSense add button][pfsense_add_button]

In the page that will open (_Edit Route Entry_), enter, e.g., CLIENT-NET as the name of the _Destination network_.
In the _Gateway_ field choose the previously created gateway, _CLIENT-GW - 192.168.11.12_:
![pfSense edit client static routes page done][pfsense_edit_client_static_routes_page]

In order to apply these changes, click _Apply Changes_ at the top of the page once this information shows up:
![pfSense apply changes button][pfsense_gateways_page_apply_changes_button]

At the end, the _Static Routes_ table should like this:
![pfSense static routes page done][pfsense_static_routes_page_done]

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[virtualbox_clone_virtual_machine_window]: ./screenshots/VirtualBox_clone_virtual_machine_window.png "VirtualBox clone virtual machine window"
[virtualbox_network_settings_window_adapter_1]: ./screenshots/VirtualBox_network_settings_window_adapter_1.png "VirtualBox network settings adapter 1 window"
[virtualbox_network_settings_window_adapter_2]: ./screenshots/VirtualBox_network_settings_window_adapter_2.png "VirtualBox network settings adapter 2 window"
[pfsense_menu_before_configuration]: ./screenshots/pfSense_menu_before_configuration.png "pfSense menu before configuration"
[pfsense_menu_assign_interfaces_option]: ./screenshots/pfSense_menu_assign_interfaces_option.png "pfSense assign interfaces menu"
[virtualbox_network_settings_window_adapter_1_with_vm_running]: ./screenshots/VirtualBox_network_settings_window_adapter_1_with_VM_running.png "VirtualBox network settings adapter 1 window with the VM running"
[virtualbox_network_settings_window_adapter_2_with_vm_running]: ./screenshots/VirtualBox_network_settings_window_adapter_2_with_VM_running.png "VirtualBox network settings adapter 2 window with the VM running"
[pfsense_menu_assign_interfaces_option_mid_process]: ./screenshots/pfSense_menu_assign_interfaces_option_mid_process.png "pfSense assign interfaces mid process"
[pfsense_menu_assign_interfaces_option_process_done]: ./screenshots/pfSense_menu_assign_interfaces_option_process_done.png "pfSense assign interfaces process end"
[pfsense_set_interfaces_ip_address_menu_option_wan]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_WAN.png "pfSense set WAN interface IP addresses"
[pfsense_set_interfaces_ip_address_menu_option_wan_mid_process]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_WAN_mid_process.png "pfSense set WAN interface IP addresses mid process"
[pfsense_set_interfaces_ip_address_option_wan_last_part]: ./screenshots/pfSense_set_interfaces_IP_address_option_WAN_last_part.png "pfSense set WAN interface IP addresses process end"
[pfsense_set_interfaces_ip_address_menu_option_wan_done]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_WAN_done.png "pfSense after set WAN interface IP addresses process"
[pfsense_set_interfaces_ip_address_menu_option_lan]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_LAN.png "pfSense set LAN interface IP addresses"
[pfsense_set_interfaces_ip_address_menu_option_lan_mid_process]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_LAN_mid_process.png "pfSense set LAN interface IP addresses mid process"
[pfsense_set_interfaces_ip_address_menu_option_lan_done]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_LAN_done.png "pfSense set LAN interface IP addresses process end"
[pfsense_set_interfaces_ip_address_menu_option_lan_after_process]: ./screenshots/pfSense_set_interfaces_IP_address_menu_option_LAN_after_process.png "pfSense after set LAN interface IP addresses process"
[pfsense_login_page]: ./screenshots/pfSense_login_page.png "pfSense login page"
[pfsense_setup_wizard]: ./screenshots/pfSense_setup_wizard.png "pfSense setup wizard"
[pfsense_setup_wizard_3]: ./screenshots/pfSense_setup_wizard_3.png "pfSense setup wizard"
[pfsense_setup_wizard_4]: ./screenshots/pfSense_setup_wizard_4.png "pfSense setup wizard"
[pfsense_setup_wizard_5_configure_wan_interface_section]: ./screenshots/pfSense_setup_wizard_5_configure_WAN_interface_section.png "pfSense setup wizard configure WAN interface section"
[pfsense_setup_wizard_5_static_ip_configuration_section]: ./screenshots/pfSense_setup_wizard_5_static_IP_configuration_section.png "pfSense setup wizard static IP configuration section"
[pfsense_setup_wizard_5_network_rules_configuration_section]: ./screenshots/pfSense_setup_wizard_5_network_rules_configuration_section.png "pfSense setup wizard network rules configuration section"
[pfsense_setup_wizard_6]: ./screenshots/pfSense_setup_wizard_6.png "pfSense setup wizard"
[pfsense_system_dropdown_menu]: ./screenshots/pfSense_system_dropdown_menu.png "pfSense system dropdown menu"
[pfsense_add_button]: ./screenshots/pfSense_add_button.png "pfSense add button"
[pfsense_edit_client_gateway_page]: ./screenshots/pfSense_edit_client_gateway_page.png "pfSense edit client gateway page"
[pfsense_gateways_page_apply_changes_button]: ./screenshots/pfSense_gateways_page_apply_changes_button.png "pfSense apply changes button"
[pfsense_gateways_page_done]: ./screenshots/pfSense_gateways_page_done.png "pfSense gateways page done"
[pfsense_edit_client_static_routes_page]: ./screenshots/pfSense_edit_client_static_routes_page.png "pfSense edit client static routes page done"
[pfsense_static_routes_page_done]: ./screenshots/pfSense_static_routes_page_done.png "pfSense static routes page done"

<!-- Images declarations (reference style) - end" -->
