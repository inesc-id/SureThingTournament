# "Internet" router setup

Here one can find the instructions to setup the virtual machine that is used to emulate the "Internet" for the deployed [network topology](../README.md/##network-topology "Network topologies description section").

<br>

## pfSense distribution instructions

The configurations already made for the [base router instance](../base_router "pfSense base instance setup instructions") can be used for the virtual machine instance of the "Internet" router.
Meaning this new virtual machine will continue where the [base router instance](../base_router "pfSense base instance setup instructions") configuration "left off"; there is only the need to make a few additional configurations.
As such start [base router instance](../base_router "pfSense base instance setup instructions") by following one of these ways:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machine click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

<br>

### pfSense distribution configuration

Once the virtual machine finishes the startup process and the pfSense menu shows up, open a web browser from one of the virtual machines that were already deployed, e.g., the [attacker machine](../../attacker_VM "Attacker machine folder") and access 192.168.11.1, assuming that was the previously configured IPv4 address of the LAN interface.
It is very likely the used browser will warn about a security risk, since pfSense uses a pre-installed and self-signed certificate.
This is normal, so just accept and continue.
Once the login page loads, use _admin_ as the username and _pfsense_ as its corresponding password:
![pfSense login page][pfsense_login_page]

The setup wizard will then show up:
![pfSense setup wizard][pfsense_setup_wizard]

Press _Next_ until the _General Information_ page appears:
![pfSense setup wizard][pfsense_setup_wizard_2]

Enter the desired _Hostname_, e.g., internet-router, and localdomain as the _Domain_.
Enter 192.168.1.80 as one of the DNS servers and, optionally, also enter 8.8.8.8 as another DNS server:
![pfSense setup wizard][pfsense_setup_wizard_3]

You can leave the values entered by default in the _Time Server Information_ page:
![pfSense setup wizard][pfsense_setup_wizard_4]

In the next page (_Configure WAN Interface_), make sure the value of the _SelectedType_ field is _Static_:
![pfSense setup wizard configure WAN interface section][pfsense_setup_wizard_5_configure_wan_interface_section]

In the _Static IP Configuration_ section enter 192.168.1.80, 24, and 192.168.1.1 as the _IP Address_, _Subnet Mask_, _Upstream Gateway_ values, respectively, considering these were the values entered [previously](../base_router/###pfSense-distribution-configuration "base pfSense configuration section"):
![pfSense setup wizard static IP configuration section][pfsense_setup_wizard_5_static_ip_configuration_section]

Make sure the _Block private networks from entering via WAN_ option in the _RFC1918 Networks_ section is not selected.
In the _Block bogon networks_ section, leave the _Block non-Internet routed networks from entering via WAN_ selected:
![pfSense setup wizard network rules configuration section][pfsense_setup_wizard_5_network_rules_configuration_section]

The remaining options can be left unchanged.

Click _Next_ to go to the _Configure LAN interface_ page.
There, enter 192.168.11.1 as the _LAN IP Address_ value and 24 in the _Subnet Mask_ field:
![pfSense setup wizard][pfsense_setup_wizard_6]

In the _Set Admin WebGUI Password_ page, there is the chance to change the default password (_pfsense_), if needed.

In the next page click _Reload_ to confirm and reload pfSense with the new changes.
Once the reload has finished, it will show a page (_Wizard completed._) with that information.
Just click _Finish_ to finish and close the setup wizard.

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

Now is time to do the same for the gateway of the [network of the server](../4-server_network_router "CROSS-server's network router folder").
As such, click the _Add_ button.
In the page that opens (_Edit Gateway_), in the _Interface_ field choose _LAN_ and in the _Address Family_ field choose _IPv4_.
Next, give this gateway a name, e.g., SERVER-GW, and enter its corresponding IP address, in this case 192.168.11.11.
To save these changes, click _Save_:
![pfSense edit server gateway page][pfsense_edit_server_gateway_page]

Again, click _Apply Changes_ at the top of the page to apply these changes:
![pfSense apply changes button][pfsense_gateways_page_apply_changes_button]

Lastly, go over the same steps but this time for the gateway of the [ISP of the attacker](./2-attacker_ISP "Attacker's ISP router folder").
To do so, click the _Add_ button.
In the page that opens (_Edit Gateway_), in the _Interface_ field choose _LAN_ and in the _Address Family_ field choose _IPv4_.
Next, give this gateway a name, e.g., ATTACKER-GW, and enter its corresponding IP address, in this case 192.168.11.13.
To save these changes, click _Save_:
![pfSense edit attacker gateway page][pfsense_edit_attacker_gateway_page]

Click _Apply Changes_ at the top of the page in order to apply these changes:
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

Click _Add_ again to configure a static route but this time for the [network of the server](../4-server_network_router "CROSS-server's network router folder").
In the _Edit Route Entry_ page enter, e.g., SERVER-NET as the name of the _Destination network_.
In the _Gateway_ field choose the previously created gateway, _SERVER-GW - 192.168.11.11_:
![pfSense edit server static routes page done][pfsense_edit_server_static_routes_page]

Again, click _Apply Changes_ at the top of the page in order to apply these changes:
![pfSense apply changes button][pfsense_gateways_page_apply_changes_button]

Click _Add_ to configure a static route to the router that emulates the [ISP of the attacker](./2-attacker_ISP "Attacker's ISP router folder").
In the _Edit Route Entry_ page enter, e.g., ATTACKER-NET as the name of the _Destination network_.
In the _Gateway_ field choose the previously created gateway, _ATTACKER-GW - 192.168.11.13_:
![pfSense attacker static routes page][pfsense_edit_attacker_static_route_page]

Click _Apply Changes_ again at the top of the page to apply these changes:
![pfSense apply changes button][pfsense_gateways_page_apply_changes_button]

At the end, the _Static Routes_ table should like this:
![pfSense static routes page done][pfsense_static_routes_page_done]

<!-- TODO: If seemed needed, add description on how to add the any-to-any rules -->

<!-- ############################################## -->

<!-- Images declarations (reference style) - start -->

[pfsense_login_page]: ./screenshots/pfSense_login_page.png "pfSense login page"
[pfsense_setup_wizard]: ./screenshots/pfSense_setup_wizard.png "pfSense setup wizard"
[pfsense_setup_wizard_2]: ./screenshots/pfSense_setup_wizard_2.png "pfSense setup wizard"
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
[pfsense_edit_server_gateway_page]: ./screenshots/pfSense_edit_server_gateway_page.png "pfSense edit server gateway page"
[pfsense_edit_attacker_gateway_page]: ./screenshots/pfSense_edit_attacker_gateway_page.png "pfSense edit attacker gateway page"
[pfsense_gateways_page_done]: ./screenshots/pfSense_gateways_page_done.png "pfSense gateways page done"
[pfsense_edit_client_static_routes_page]: ./screenshots/pfSense_edit_client_static_routes_page.png "pfSense edit client static routes page done"
[pfsense_edit_server_static_routes_page]: ./screenshots/pfSense_edit_server_static_routes_page.png "pfSense edit server static routes page done"
[pfsense_static_routes_page_done]: ./screenshots/pfSense_static_routes_page_done.png "pfSense static routes page done"
[pfsense_edit_attacker_static_route_page]: ./screenshots/pfSense_edit_attacker_static_route_page.png "pfSense attacker static routes page"

<!-- Images declarations (reference style) - end -->
