# CROSS-client mobile application code setup

Here one can find the instructions to install and setup the virtual machine that will hold the code of the [(CROSS-client) mobile application](../CROSS_client_mobile_application "CROSS-client mobile application folder").

Once the code of the mobile application is provided to the [CROSS-client virtual machine](../CROSS_client_mobile_application "CROSS-client mobile application folder"), this virtual machine can be [terminated/powered](./##virtual-machine-instance-poweroff "Virtual machine instance poweroff section") off right away.
No longer consuming resources on the host machine.

It will only be used [later](./###virtual-machine-settings-configuration) but, to save some time, one can start to download the file with the Ubuntu 20.04 image disk [here](https://drive.google.com/file/d/1Db_hhf_9uj8xnHvg1MqwIZzsSwSlrIVQ/view?usp=sharing "ubuntu-20.04.2.0-desktop-amd64 disk image, located in the SureThing project Google Drive folder") (SHA256SUM: 93bdab204067321ff131f560879db46bee3b994bf24836bb78538640f689e58f).

<br>

## Virtual machine instance creation

Create a new instance of a virtual machine by going to _Machine_ menu and then selecting the _New..._ option from the drop-down menu.
In the window that opens (_Create Virtual Machine_) give a name to the virtual machine, e.g., CROSS-client (code), and choose the folder where you would like to place the files of the virtual machine.
Next, fill the next two fields.
In the _type_ field choose _Linux_ and in the _Version_ field pick _Ubuntu (64-bit)_.
It is recommended to allow the virtual machine to use at least 4 GB of RAM, as the _Android Studio_ will then be installed in this instance.
If RAM memory is not a problem in the host machine, consider making available 8 GB of RAM as it is the recommended value by the official _Android Studio_ documentation.
While it was not tested, it could be possible to provide less RAM memory to the virtual machine.
Finally, choose the _Create a virtual hard disk now_ option.
Click _Create_ at the end to move to the next window:
![VirtualBox create virtual machine window][virtualbox_create_virtual_machine_window]

In the next window that opens up (_Create Virtual Hard Disk_), VirtualBox will save the virtual hard disk in the previously chosen location but there is the option to change it.
For the size of the virtual hard disk, give it 40 GB.
You can leave the option selected by default (_VDI (VirtualBox Disk Image)_) but make sure the _Dynamically allocated_ is the selected option in the _Storage on physical hard disk_ field.
Lastly, click _Create_ to create the virtual machine:
![VirtualBox create virtual hard disk window][virtualbox_create_virtual_hard_disk_window]

<br>

## Virtual machine settings configuration

Once the virtual machine instance is created, open its _Settings_ window.
In that window go to the _System_ > _Processor_ tab.
Confirm the virtual machine is set to only use 1 CPU:

![Virtualbox settings window showing the system options][virtualbox_system_settings_window]

Next go to the _Display_ tab and, in the main _Screen_ tab, increase the video memory provided to the virtual machine to, e.g., 128 MB:
![Virtualbox settings window showing the display options][virtualbox_display_settings_window]

In the _Storage_ tab select the _Empty_ entry, from the storage controller, for instance _Controller: IDE_:
![Virtualbox settings window showing the storage options before mounting the virtual disk][virtualbox_storage_settings_window]

Once highlighted, click the button to open the dropdown menu with the existing options:
![Virtualbox choose virtual disk button icon][virtualbox_storage_settings_choose_virtual_disk_button_icon]

In the dropdown menu, click the _Choose a disk file..._ option and select the location where the downloaded Ubuntu image disk file is.
The virtual image disk will then show as attached to the virtual machine, as such:
![Virtualbox settings window showing the storage options after mounting the virtual disk][virtualbox_storage_settings_window_with_virtual_disk]

Disable audio, as it is not necessary, by going to the _Audio_ tab and unselecting the _Enable Audio_ option:
![VirtualBox settings window showing the audio option][virtualbox_audio_settings_window]

Moving on to the _Network_ tab, enable two network adapters, e.g., _Adapter 1_ and _Adapter 2_, respectively, shown in the next two figures.
One of these network adapters has to be selected as _Attached to NAT_ (Network Address Translation).
The type of the adapter used can be left with the value that gets selected automatically by default, i.e., _Intel PRO/1000 MT Desktop (82540EM)_.

The other network adapter needs to be an _Host-only Adapter_.
**Important note**: If, for some reason, there are multiple _VirtualBox Host-Only_ network adapters make sure its name is the same as the one the instance of the [CROSS-client mobile application](../CROSS_client_mobile_application/##virtual-machine-settings-configuration "CROSS-client mobile application VirtualBox settings configuration") uses.

Expanding the _Advanced_ options, both the _Adapter Type_ and _Promiscuous Mode_ options can be left with the default values, respectively _Intel PRO/1000 MT Desktop (82540EM)_ and _Deny_.
If desired, both network adapters can have new generated MAC addresses.
Not to mention, there is also the option to have the virtual machinhe detect the network cable is pluged in to each network adapter.
At the end, click _OK_ to confirm and close the _Settings_ window:

![VirtualBox network settings window showing the adapter 1 options][virtualbox_network_settings_window_adapter_1]
![VirtualBox network settings window showing the adapter 2 options][virtualbox_network_settings_window_adapter_2]

<br>

## Ubuntu distribution installation

There three ways to start the newly created virtual machine:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machin click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

Once the virtual machine boots, follow the on-screen instructions in order to install Ubuntu.

<br>

## Installation and configuration commands

The next instructions are based on the [README](https://github.com/inesc-id/CROSS-client/blob/master/README.md "CROSS-client GitHub repository README") (kudos to Miguel Francisco) of the repository with the code of the CROSS-client.

<br>

### CROSS-client respository clone process

Clone the repository with the code of the mobile application:

```
cd Documents/
git clone https://github.com/inesc-id/CROSS-client.git
```

<br>

### IDE and code configuration

It is possible to use any Integrated Development Environment (IDE), as long as it supports [Gradle](https://gradle.org/ "Gradle website").
It is recommended to use [Android Studio](https://developer.android.com/studio/ "Android Studio website") as it was the one that was used.
As such, the next steps will be specific to Android Studio.

<br>

#### Android Studio installation

1. Open the _Ubuntu Software_ program (accessible via the _Show Applications_ Ubuntu menu):
   ![Ubuntu Software program as it shows in the menu][applications_menu_showing_ubuntu_software]

2. Select the _Android Studio_ package (either selecting it from the main page or searching for it):
   ![Ubuntu Software program main page window][ubuntu_software_window]

3. Once in the _Android Studio_ package page, click _Install_ and wait for the end of the installation process:
   ![Ubuntu Software program Android Studio package page window][ubuntu_software_android_studio_page_window]

<br>

#### Android Studio configuration

After Android Studio is installted, to open it go the _Show Applications_ Ubuntu menu as shown below:
![Android Studio as it shows in the menu][applications_menu_showing_android_studio]

To import the project:

1. In the _Welcome to Android Studio_ window, click _Import Project (Gradle, Eclipse ADT, etc.)_:
   ![Android Studio welcome window][android_studio_welcome_window]

2. Select the CROSS-client folder (_~/Documents/CROSS-client_, if the [respository clone process instructions](./###CROSS-client-respository-clone-process "CROSS-client respository clone process instructions") were followed):
   ![Android Studio import new project window][android_studio_import_project_window]

3. Click _OK_ to import it.

Next, configure the Android Software Development Kit (SDK) that will be used (Android 4.4 (KitKat)) by following these steps:

1. Go to _Tools_ > _SDK Manager_:
   ![Android Studio Tools menu][android_studio_tools_menu]
2. Select _Android 4.4 (KitKat)_:
   ![Android Studio Android SDK Manager window][android_studio_sdk_manager_window]

3. Click _Apply_ > _OK_ to download and install that version.

<br>

#### Code configuration

Configure the address of the CROSS-server by changing the **Coordinator.java** file, part of the _pt.ulisboa.tecnico.cross_ package, inside the _java_ directory:

![Android Studio project structure sidebar window showing the java directory][android_studio_project_structure_sidebar_tool_window_java_directory]

One also needs to increase the timeout to download the mobile application catalog to, e.g., 80 seconds (80000 ms).
In the **Coordinator.java** file, go to **line 53** and change it to the following, accordingly:

```Java
api = new API(this.context, pairManager, URI.create("http://192.168.21.X:13000/v1/"), 80000);
```

Where `X` is the host address of CROSS-server virtual machine instance.
Note: run, e.g., the `$ ip addr` command in the CROSS-server virtual machine in order to know its IP address.

Open to the **activity_main_drawer.xml** file, part of the _pt.ulisboa.tecnico.cross_ package, inside the _res/menu_ directory:
![Android Studio project structure sidebar window showing the res/menu directory][android_studio_project_structure_sidebar_tool_window_res_menu_directory]

Go to line **line 37** and change the `android:visible` value to `true`, like so:

```xml
android:visible="true"
```

The Debug UI option will now be availabe in the sidebar, allowing to add mocked SSIDs or BSSIDs:
![CROSS-client mobile application debug UI sidebar options][genymotion_mobile_application_debug_ui_options_sidebar]

<br>

### Mobile application provision and installation

The next and final step is to connect Android Studio to the [virtual machine of the CROSS-client mobile application](../CROSS_client_mobile_application "CROSS-client mobile application folder").

Open the GUI of the [CROSS-client mobile application virtual machine](../CROSS_client_mobile_application "CROSS-client mobile application folder"), following one of these steps:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machin click _Show_;
- Right-click on the instance of the virtual machine from the list and then click _Show_.

There look for the log system boot message that printed the assigned IP address, as shown here:
![CROSS-client mobile application system boot log messages][virtualbox_system_boot_log_messages_window]

![CROSS-client mobile application system boot IP address log message][virtualbox_system_boot_ip_address_log_message]

Once the IP address assigned by VirtualBox is known, run the following command:

```bash
adb connect <CROSS-client_mobile_application_generated_IP_address>
```

Where `<CROSS-client_mobile_application_generated_IP_address>` is the IP address noted above.

To confirm which devices are connected, run:

```bash
adb devices
```

Going back to Android Studio, open the drop-down menu with the available devices and select the _Genymotion_ one:
![Android Studio available devices menu][android_studio_available_devices_menu]

Once selected, click the _Run 'app'_ button to install and then start the mobile application on the [virtual machine of the CROSS-client mobile application](../CROSS_client_mobile_application "CROSS-client mobile application folder"):
![Android Studio run app icon button][android_studio_run_app_icon_button]

The mobile application will open up on the [virtual machine of the CROSS-client mobile application](../CROSS_client_mobile_application "CROSS-client mobile application folder") like so:
![Genymotion window after installaing the CROSS-client mobile application][cross-client_mobile_application_after_installation_genymotion_window]

<br>

## Virtual machine instance poweroff

Once the code of the client mobile application has been provided to the [CROSS-client virtual machine](../CROSS_client_mobile_application "CROSS-client mobile application folder"), the instance of this virtual machine can be deleted.
Either:

- Select the virtual machine instance from the list of virtual machines and then go to _Machine_ > _Close_ > _Power Off_;
- Right-click on the instance of the virtual machine from the list and then click _Close_ > _Power Off_.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[virtualbox_create_virtual_machine_window]: ./screenshots/VirtualBox_create_virtual_machine_window.png "VirtualBox create virtual machine window"
[virtualbox_create_virtual_hard_disk_window]: ./screenshots/VirtualBox_create_virtual_hard_disk_window.png "VirtualBox create virtual hard disk window"
[virtualbox_system_settings_window]: ./screenshots/VirtualBox_system_settings_window.png "VirtualBox settings window showing the system options"
[virtualbox_display_settings_window]: ./screenshots/VirtualBox_display_settings_window.png "VirtualBox settings window showing the display options"
[virtualbox_storage_settings_window]: ./screenshots/VirtualBox_storage_settings_window.png "Virtualbox settings window showing the storage options before mounting the virtual disk"
[virtualbox_storage_settings_choose_virtual_disk_button_icon]: ./screenshots/VirtualBox_storage_settings_choose_virtual_disk_button_icon.png "Virtualbox choose virtual disk button icon"
[virtualbox_storage_settings_window_with_virtual_disk]: ./screenshots/VirtualBox_storage_settings_window_with_virtual_disk.png "Virtualbox choose virtual disk button icon"
[virtualbox_audio_settings_window]: ./screenshots/VirtualBox_audio_settings_window.png "VirtualBox settings window showing the audio option"
[virtualbox_network_settings_window_adapter_1]: ./screenshots/VirtualBox_network_settings_window_adapter_1.png "VirtualBox network settings window showing the adapter 1 options"
[virtualbox_network_settings_window_adapter_2]: ./screenshots/VirtualBox_network_settings_window_adapter_2.png "VirtualBox network settings window showing the adapter 2 options"
[applications_menu_showing_ubuntu_software]: ./screenshots/applications_menu_showing_Ubuntu_software.png "Ubuntu Software program as it shows in the menu"
[ubuntu_software_window]: ./screenshots/Ubuntu_software_window.png "Ubuntu Software program main page window"
[ubuntu_software_android_studio_page_window]: ./screenshots/Ubuntu_software_Android_Studio_page_window.png "Ubuntu Software program Android Studio package page window"
[applications_menu_showing_android_studio]: ./screenshots/applications_menu_showing_Android_Studio.png "Android Studio as it shows in the menu"
[android_studio_welcome_window]: ./screenshots/Android_Studio_welcome_window.png "Android Studio welcome window"
[android_studio_import_project_window]: ./screenshots/Android_Studio_import_project_window.png "Android Studio import new project window"
[android_studio_tools_menu]: ./screenshots/Android_Studio_tools_menu.png "Android Studio tools menu"
[android_studio_sdk_manager_window]: ./screenshots/Android_Studio_SDK_manager_window.png "Android Studio Android SDK Manager window"
[android_studio_project_structure_sidebar_tool_window_java_directory]: ./screenshots/Android_Studio_project_structure_sidebar_tool_window_java_directory.png "Android Studio project structure sidebar window showing the java directory"
[android_studio_project_structure_sidebar_tool_window_res_menu_directory]: ./screenshots/Android_Studio_project_structure_sidebar_tool_window_res_menu_directory.png "Android Studio project structure sidebar window showing the res/menu directory"
[genymotion_mobile_application_debug_ui_options_sidebar]: ./screenshots/Genymotion_mobile_application_debug_UI_options_sidebar.png "CROSS-client mobile application debug UI sidebar options"
[virtualbox_system_boot_log_messages_window]: ./screenshots/VirtualBox_system_boot_log_messages_window.png "CROSS-client mobile application system boot log messages"
[virtualbox_system_boot_ip_address_log_message]: ./screenshots/VirtualBox_system_boot_IP_address_log_message.png "CROSS-client mobile application system boot IP address log message"
[android_studio_available_devices_menu]: ./screenshots/Android_Studio_available_devices_menu.png "Android Studio available devices menu"
[android_studio_run_app_icon_button]: ./screenshots/Android_Studio_run_app_icon_button.png "Android Studio run app icon button"
[cross-client_mobile_application_after_installation_genymotion_window]: ./screenshots/CROSS-client_mobile_application_after_installation_Genymotion_window.png "Genymotion window after installaing the CROSS-client mobile application"

<!-- Images declarations (reference style) - end" -->
