# Base router setup

Here one can find the installation and setup instructions for VirtualBox, and the first steps to configure pfSense of the virtual machine instance that is used as the base of the virtual machines that work as the routers of the network.

To save some time, start to download the file with the [pfSense image disk](https://drive.google.com/file/d/1W3QkfkwB72xrETRSmFpDFVIqKg-AtsHW/view?usp=sharing "pfSense-CE-2.5.0-RELEASE-amd64 disk image, located in the SureThing project Google Drive folder") (SHA256SUM: 5c9dce43d1f4188c686f11766d499ab6667edaf531fbd162213ed652c0534194) that will be used [later](./###virtual-machine-settings-configuration).

<br>

## VirtualBox instructions

### Virtual machine instance creation

Create a new instance of a virtual machine by going to _Machine_ > _New..._.
In the window that opens (_Create Virtual Machine_) give a name to the virtual machine, e.g., Internet (router), and choose the location for the files of the virtual machine.
Next, choose the _Operating System_ type and version..
In the _Type_ field choose _BSD_ and in the _Version_ field pick _FreeBSD (64-bit)_.
512 MB of RAM for this virtual machine is more than enough.
Finally, leave the _Create a virtual hard disk now_ option selected.
Click _Create_ to continue with the setup process:
![VirtualBox create virtual machine window][virtualbox_create_virtual_machine_window]

In the next window that opens up (_Create Virtual Hard Disk_), VirtualBox will save the virtual hard disk in the previously chosen location but there is the option to change it.
For the size of the virtual hard disk, 8 GB is enough.
You can leave the option selected by default (_VDI (VirtualBox Disk Image)_), but make sure the _Dynamically allocated_ is the selected option in the _Storage on physical hard disk_ field.
Lastly, click _Create_ to create an instance for the specified virtual machine:

![VirtualBox create virtual hard disk window][virtualbox_create_virtual_hard_disk_window]

<br>

### Virtual machine settings configuration

After the instance of the just created virtual machine is ready to use, open its _Settings_ window.
The default number of virtual CPUs passed to the virtual machine (1 CPU) is more than enough for the case, but one can increase by going to the _System_ > _Processor_ tab:

![Virtualbox settings window showing the system options][virtualbox_system_settings_window]

In the _Storage_ tab select the _Empty_ entry, from the storage controller, for instance _Controller: IDE_:
![Virtualbox settings window showing the storage options before mounting the virtual disk][virtualbox_storage_settings_window]

Once highlighted, click the button to open the dropdown menu with the existing options:
![Virtualbox choose virtual disk button icon][virtualbox_storage_settings_choose_virtual_disk_button_icon]

In the dropdown menu, click the _Choose a disk file..._ option and select the location where the pfSense image disk file is.
The virtual image disk will then show as attached to the virtual machine, as such:
![Virtualbox settings window showing the storage options after mounting the virtual disk][virtualbox_storage_settings_window_with_virtual_disk]

There is no need for the virtual machine to have access to audio.
To disable it go to the _Audio_ tab and unselect the _Enable Audio_ option:
![VirtualBox settings window showing the audio option][virtualbox_audio_settings_window]

Moving on to network-related settings.
Open the _Network_ tab and enable two network adapters, e.g., _Adapter 1_ and _Adapter 2_.
One of the network adapters needs to be a _Bridged Adapter_.
In the _Name_ field, depending on the host system definitions, choose the controller/adapter accordingly, e.g., _Realtek PCIe GbE Family Controller_.

The second network adapter has to be attached to _Internal Network_ and for its name create a new network: _internet_\__network_.

Expanding the _Advanced_ options, both the _Adapter Type_ and _Promiscuous Mode_ options to be used by the virtual machine can be left with the default values, respectively _Intel PRO/1000 MT Desktop (82540EM)_ and _Deny_.
If desired, it is possible to generate a new MAC address with the option to have the virtual machinhe detect the network cable is pluged in to each of the two network adapters.
At the end, click _OK_ to confirm and close the _Settings_ window:

![VirtualBox network settings adapter 1 window][virtualbox_network_settings_window_adapter_1]
![VirtualBox network settings adapter 2 window][virtualbox_network_settings_window_adapter_2]

<br>

## pfSense distribution instructions

### pfSense distribution installation

There are three ways to start the newly created virtual machine:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machine click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

Once the virtual machine boots into the menu boot options, select the first option (_Boot Multi User [Enter]_) by either pressing "1" or by hitting "Enter":
![pfSense bootloader menu][pfsense_installation_bootloader_menu]

Wait a few seconds and then when the installation conditions/terms show up hit "Enter" to accept them and continue with the installation process:
![pfSense installation conditions][pfsense_installation_conditions]

In the next window that shows up (_Welcome_), select the _Install_ option:
![pfSense installation welcome window][pfsense_installation_welcome_window]

In the _Keymap Selection_ window, scroll down and choose the preferred keymap or simply stick with the default one ("US") and then select the _Continue with < selected keymap>_ option at the top of the list to continue:
![pfSense installation keymap selection window][pfsense_installation_keymap_selection_window]

Next, select the first option (_Auto (UFS) BIOS_) in the window that opens (_Partitioning_):
![pfSense installation partitioning window][pfsense_installation_partitioning_window]

The installation wil then continue automatically:
![pfSense installation mid automatic process][pfsense_installation_mid_automatic_process]

Once completed, select _No_ when asked to open a shell in the newly installed system:
![pfSense installation manual configuration window][pfsense_installation_manual_configuration_window]

Just select _Reboot_ to finish the installation in the next window that opens up (_Complete_):
![pfSense installation complete window][pfsense_installation_complete_window]

Mid-booting process try to remove pfSense live disk image.
If too late just shut down the virtual machine, remove the virtual disk, and boot the virtual machine again.

<br>

### pfSense distribution configuration

Once booted and after loading all configurations, it will show a similar menu:
![pfSense before configuration menu][pfsense_menu_before_configuration]

Press "1" to start by assiging the network interfaces:
![pfSense assign interfaces option][pfsense_menu_assign_interfaces_option]

Type "n" when asked about setting up VLANs.
In order to know the MAC address of each interface open the VirtualBox settings window of the virtual machine and go to the _Network_ tab:

![VirtualBox network settings adapter 1 window with the VM running][virtualbox_network_settings_window_adapter_1_with_vm_running]
![VirtualBox network settings adapter 2 window with the VM running][virtualbox_network_settings_window_adapter_2_with_vm_running]

There expand the _Advanced_ options for each of the two enabled adapters and check the value in the _MAC Address_ field.
The WAN interface corresponds to the VirtualBox network adapter that is attached to _Bridged Adapter_; while the LAN interface corresponds to the network adapter attached to _Internal Network_.
When asked enter the network interface names, i.e., _em0_ and _em1_, accordingly:
![pfSense assign interfaces mid process][pfsense_menu_assign_interfaces_option_mid_part]

After entering both interfaces names correctly, type "y" and press "Enter" to confirm the changes:
![pfSense assign interfaces process end][pfsense_menu_assign_interfaces_option_done]

Next, set the IP addresses of both just assigned network interfaces.
Choose the _2) Set interfaces(s) IP address_ option by pressing "2" and hitting "Enter".
Let us start by setting the IP address of the WAN interface.
As such, press "1" when asked:
![pfSense set WAN interface IP addresses][pfsense_menu_set_interfaces_ip_address_option_wan]

Press "n" to not configure the IPv4 address of this network interface through DHCP, and then enter desired IPv4 address, e.g., 192.168.1.80.
When asked, enter the desired mask for the subnetwork, e.g., 24.
Next, enter the corresponding upstream gateway IPv4 address, for instance, 192.168.1.1.
Press "n" to not configure the IPv6 address of this network interface through DHCP, and then "Enter" to not insert any input.
When asked to revert the _webConfigurator_ protocol to HTTP, press "n":
![pfSense set WAN interface IP addresses mid process][pfsense_menu_set_interfaces_ip_address_option_wan_mid_part]

Lastly, press "Enter" to finish setting the IP addresses of the WAN interface:
![pfSense set WAN interface IP addresses process end][pfsense_menu_set_interfaces_ip_address_option_wan_last_part]

The main menu will now look like this:
![pfSense after set WAN interface IP addresses process][pfsense_menu_set_interfaces_ip_address_option_wan_done]

The only thing left to configure is the IP address of the LAN interface, pressing "2" to do so.
Press "2" and then "Enter" to start setting it:
![pfSense set LAN interface IP addresses][pfsense_menu_set_interfaces_ip_address_option_lan]

When asked, enter the IPv4 address of the LAN interface and its desired subnetwork mask, e.g., 192.168.11.1 and 24, respectively.
For the next required input, just press "Enter" as we are configuring a LAN interface.
Press "Enter" again to not enter any IPv6 address for the LAN interface.
Next, press "n" in order to have DHCP disable in the LAN.
When asked to revert the _webConfigurator_ protocol to HTTP, press "n":
![pfSense set LAN interface IP addresses mid process][pfsense_menu_set_interfaces_ip_address_option_lan_mid_part]

Lastly, press "Enter" to finish setting the IP addresses of the LAN interface:
![pfSense set LAN interface IP addresses process end][pfsense_menu_set_interfaces_ip_address_option_lan_last_part]

When finished, the main menu will look similar to this:
![pfSense after set LAN interface IP addresses process][pfsense_menu_set_interfaces_ip_address_option_lan_done]

<!-- ############################################## -->

<!-- Images declarations (reference style) - start -->

[virtualbox_create_virtual_machine_window]: ./screenshots/VirtualBox_create_virtual_machine_window.png "VirtualBox create virtual machine window"
[virtualbox_create_virtual_hard_disk_window]: ./screenshots/VirtualBox_create_virtual_hard_disk_window.png "VirtualBox create virtual hard disk window"
[virtualbox_system_settings_window]: ./screenshots/VirtualBox_system_settings_window.png "Virtualbox settings window showing the system options"
[virtualbox_storage_settings_window]: ./screenshots/VirtualBox_storage_settings_window.png "Virtualbox settings window showing the storage options before mounting the virtual disk"
[virtualbox_storage_settings_choose_virtual_disk_button_icon]: ./screenshots/VirtualBox_storage_settings_choose_virtual_disk_button_icon.png "Virtualbox choose virtual disk button icon"
[virtualbox_storage_settings_window_with_virtual_disk]: ./screenshots/VirtualBox_storage_settings_window_with_virtual_disk.png "Virtualbox choose virtual disk button icon"
[virtualbox_audio_settings_window]: ./screenshots/VirtualBox_audio_settings_window.png "VirtualBox settings window showing the audio option"
[virtualbox_network_settings_window_adapter_1]: ./screenshots/VirtualBox_network_settings_window_adapter_1.png "VirtualBox network settings adapter 1 window"
[virtualbox_network_settings_window_adapter_2]: ./screenshots/VirtualBox_network_settings_window_adapter_2.png "VirtualBox network settings adapter 2 window"
[pfsense_installation_bootloader_menu]: ./screenshots/pfSense_installation_bootloader_menu.png "pfSense bootloader menu"
[pfsense_installation_conditions]: ./screenshots/pfSense_installation_conditions.png "pfSense installation conditions"
[pfsense_installation_welcome_window]: ./screenshots/pfSense_installation_welcome_window.png "pfSense installation welcome window"
[pfsense_installation_keymap_selection_window]: ./screenshots/pfSense_installation_keymap_selection_window.png "pfSense installation keymap selection window"
[pfsense_installation_partitioning_window]: ./screenshots/pfSense_installation_partitioning_window.png "pfSense installation partitioning window"
[pfsense_installation_mid_automatic_process]: ./screenshots/pfSense_installation_mid_automatic_process.png "pfSense installation mid automatic process"
[pfsense_installation_manual_configuration_window]: ./screenshots/pfSense_installation_manual_configuration_window.png "pfSense installation manual configuration window"
[pfsense_installation_complete_window]: ./screenshots/pfSense_installation_complete_window.png "pfSense installation complete window"
[pfsense_menu_before_configuration]: ./screenshots/pfSense_menu_before_configuration.png "pfSense before configuration menu"
[pfsense_menu_assign_interfaces_option]: ./screenshots/pfSense_menu_assign_interfaces_option.png "pfSense assign interfaces menu"
[virtualbox_network_settings_window_adapter_1_with_vm_running]: ./screenshots/VirtualBox_network_settings_window_adapter_1_with_VM_running.png "VirtualBox network settings adapter 1 window with the VM running"
[virtualbox_network_settings_window_adapter_2_with_vm_running]: ./screenshots/VirtualBox_network_settings_window_adapter_2_with_VM_running.png "VirtualBox network settings adapter 2 window with the VM running"
[pfsense_menu_assign_interfaces_option_mid_part]: ./screenshots/pfSense_menu_assign_interfaces_option_mid_part.png "pfSense assign interfaces mid process"
[pfsense_menu_assign_interfaces_option_done]: ./screenshots/pfSense_menu_assign_interfaces_option_done.png "pfSense assign interfaces process end"
[pfsense_menu_set_interfaces_ip_address_option_wan]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_WAN.png "pfSense set WAN interface IP addresses"
[pfsense_menu_set_interfaces_ip_address_option_wan_mid_part]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_WAN_mid_part.png "pfSense set WAN interface IP addresses mid process"
[pfsense_menu_set_interfaces_ip_address_option_wan_last_part]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_WAN_last_part.png "pfSense set WAN interface IP addresses process end"
[pfsense_menu_set_interfaces_ip_address_option_wan_done]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_WAN_done.png "pfSense after set WAN interface IP addresses process"
[pfsense_menu_set_interfaces_ip_address_option_lan]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_LAN.png "pfSense set LAN interface IP addresses"
[pfsense_menu_set_interfaces_ip_address_option_lan_mid_part]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_LAN_mid_part.png "pfSense set LAN interface IP addresses mid process"
[pfsense_menu_set_interfaces_ip_address_option_lan_last_part]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_LAN_last_part.png "pfSense set LAN interface IP addresses process end"
[pfsense_menu_set_interfaces_ip_address_option_lan_done]: ./screenshots/pfSense_menu_set_interfaces_IP_address_option_LAN_done.png "pfSense after set LAN interface IP addresses process"

<!-- Images declarations (reference style) - end" -->
