# Attacker machine setup

This describes how to setup the machine of the attacker and deploy it in the network, according to its [topology](../README.md/##network-topology "Network topology description section").

Since the [Kali 2020.4 image disk](https://drive.google.com/file/d/1GOpvvgqDRbCQ0xbcNzEsyy-DdOV6_dJf/view?usp=sharing "kali-linux-2020.4-installer-amd64 disk image, located in the SureThing project Google Drive folder") (SHA256SUM: 50492d761e400c2b5e22c8f253dd6f75c27e4bc84e33c2eff272476a0588fb02) is quite large and may take some time to download, one can start its download now and have it ready to use [later](./###virtual-machine-settings-configuration).

<br>

## Virtual machine instance creation

Create a new instance of a virtual machine by going to _Machine_ > _New..._.
In the window that opens (_Create Virtual Machine_) give a name to the virtual machine, e.g., Attacker, and choose the folder where you would like to place the files of the virtual machine.
Next, fill the next two fields.
In the _type_ field choose _Linux_ and in the _Version_ field pick _Other Linux (64-bit)_.
Allow at least 4 GB of RAM (recommended to allow 8 GB of RAM) to be available to the virtual machine.
Finally, choose the _Create a virtual hard disk now_ option.
Click _Create_ to continue with the setup process:
![VirtualBox create virtual machine window][virtualbox_create_virtual_machine_window]

In the next window that opens up (_Create Virtual Hard Disk_), VirtualBox will save the virtual hard disk in the previously chosen location but there is the option to change it.
Give 50 GB for the size of the virtual hard disk, as some tools tend to take quite some space.
You can leave the option selected by default (_VDI (VirtualBox Disk Image)_) but make sure the _Dynamically allocated_ is the selected option in the _Storage on physical hard disk_ field.
Lastly, click _Create_ to create an instance for the specified virtual machine:

![VirtualBox create virtual hard disk window][virtualbox_create_virtual_hard_disk_window]

<br>

## Virtual machine settings configuration

If the host system supports it, it is recommended to provide more than 1 CPU to the virtual machine, e.g., 2 or even 4 CPUs.
For that, select the just created virtual machine from the list and open its _Settings_ window.
Then go to the _System_ > _Processor_ tab:
![Virtualbox settings window showing the system options][virtualbox_system_settings_window]

Next go to the _Display_ tab and in the main _Screen_ tab, increase the video memory provided to the virtual machine, e.g., to 128 MB:
![Virtualbox settings window showing the display options][virtualbox_display_settings_window]

In the _Storage_ tab select the _Empty_ entry, from the storage controller, for instance _Controller: IDE_:
![Virtualbox settings window showing the storage options before mounting the virtual disk][virtualbox_storage_settings_window]

Once highlighted, click the button to open the dropdown menu with the existing options:
![Virtualbox choose virtual disk button icon][virtualbox_storage_settings_choose_virtual_disk_button_icon]

In the dropdown menu, click the _Choose a disk file..._ option and select the location where the Kali image disk file is.
The virtual image disk will then show as attached to the virtual machine, as such:
![Virtualbox settings window showing the storage options after mounting the virtual disk][virtualbox_storage_settings_window_with_virtual_disk]

Disable audio, as it is not necessary, by going to the _Audio_ tab and unselecting the _Enable Audio_ option:
![VirtualBox settings window showing the audio option][virtualbox_audio_settings_window]

Moving on to the _Network_ tab, enable one network adapter: select it as attached to _Internal Network_ and create a network named _attacker_\__network_.
In the _Advanced_ options, the _Adapter Type_ field can be left with the default value (_Intel PRO/1000 MT Desktop (82540EM)_).
In the _Promiscuous Mode_ field the _Allow VMs_ option should be selected.
If needed, it is possible to generate a new MAC address with the option to have the virtual machinhe detect the network cable is pluged in to the network adapter.
At the end, click _OK_ to confirm and close the _Settings_ window:
![VirtualBox settings window showing the network options][virtualbox_network_settings_window]

<br>

## Kali Linux distribution installation

There three ways to start the newly created virtual machine:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machin click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

Once the virtual machine boots, follow the on-screen instructions in order to install Kali Linux.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[virtualbox_create_virtual_machine_window]: ./screenshots/VirtualBox_create_virtual_machine_window.png "VirtualBox create virtual machine window"
[virtualbox_create_virtual_hard_disk_window]: ./screenshots/VirtualBox_create_virtual_hard_disk_window.png "VirtualBox create virtual hard disk window"
[virtualbox_system_settings_window]: ./screenshots/VirtualBox_system_settings_window.png "VirtualBox settings window showing the system options"
[virtualbox_display_settings_window]: ./screenshots/VirtualBox_display_settings_window.png "VirtualBox settings window showing the display options"
[virtualbox_storage_settings_window]: ./screenshots/VirtualBox_storage_settings_window.png "Virtualbox settings window showing the storage options before mounting the virtual disk"
[virtualbox_storage_settings_choose_virtual_disk_button_icon]: ./screenshots/VirtualBox_storage_settings_choose_virtual_disk_button_icon.png "Virtualbox choose virtual disk button icon"
[virtualbox_storage_settings_window_with_virtual_disk]: ./screenshots/VirtualBox_storage_settings_window_with_virtual_disk.png "Virtualbox settings window showing the storage options after mounting the virtual disk"
[virtualbox_audio_settings_window]: ./screenshots/VirtualBox_audio_settings_window.png "VirtualBox settings window showing the audio option"
[virtualbox_network_settings_window]: ./screenshots/VirtualBox_network_settings_window.png "VirtualBox settings window showing the network options"

<!-- Images declarations (reference style) - end" -->
