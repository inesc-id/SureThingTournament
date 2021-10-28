# CROSS-client mobile application setup

These are the instructions to install and setup the virtual machine where the CROSS-client mobile application will run.

<br>

## Genymotion virtual device creation

The CROSS-client mobile application will run inside the [Genymotion (Desktop)](https://genymotion.com/ "Genymotion website") Android emulator.
Genymotion uses/relies on VirtualBox for the virtualization process.
Its installer is available [here](https://drive.google.com/file/d/1mZTiINm6QA-FRBMdBMLwwZxa4xbnwPk6/view?usp=sharing "Genymotion installer, located in the SureThing project Google Drive folder") (SHA256SUM: bbed300c41a303a12b6d982281d2ffa5ed9477781538c770469c43b98d7b4b45).

After installing it, run _Genymotion (Desktop)_ and, when asked, create an acccount if needed.
After that, log in and choose _Personal use_ when prompted.

In the main window click in the plus _Add virtual device_ button close to the top right corner of the window in order to create a new virtual device:
![Genymotion add new virtual device button][genymotion_add_new_virtual_device_button]

Once the _Virtual device installation_ window opens, choose the desired virtual device to use as the platform for the CROSS-client mobile application:
![Genymotion choose virtual device window][genymotion_virtual_device_choice_window]

Any version above Android 4.4 (KitKat) - API 19, inclusive, should work.
Yet the it is recommended to choose one running Android 5.1 (Lollipop) - API 22 as it was the one that was used in the experiments.
Choose one device from the set of flavors Genymotion makes available, preferably Samsung Galaxy S6 as it was the one that was used.
After selecting the desired virtual device, click _NEXT_ in order to be taken to the next window.

In the next window it is possible to change the default name of the virtual device to, e.g., CROSS-client:
![Genymotion virtual device settings window][genymotion_virtual_device_settings_window]

In the _Display_ section, leave the _Predefined_ option selected.
If desired, it is possible to change these resolution values.
A screen size of **480 x 800** with a density of **240 - HDPI** is known to work.
Concerning the _System_ section, leave the _Android version_ field unchanged; the number of processors and the memory size provided to the virtual device can also be left unchanged.
If needed, it is confirmed one can downgrade the number of processors from 4 to 2 without any substantial visible difference in performance.
In the _Android system options_ section, select any of the two options if needed.
Lastly, choosing any of the two options in the _Network mode_ section if fine as the network mode/adapter will be changed later.
So you can leave the _NAT_ option selected, which is the default one.
At the end, click _INSTALL_ in order to create the just configured virtual device.

Once the creation process finishes at Genymotion, an instance of the created virtual device will be available/can be seen at VirtualBox.

<br>

## Virtual machine settings configuration

Open VirtualBox.
There, select the just created virtual device with Genymotion from the list of virtual machines instances and open its _Settings_.
In the _Settings_ window, select the _Network_ tab.
There, enable two network adapters; let us say _Adapter 1_ and _Adapter 2_, as respectively shown in the next two figures:

![VirtualBox network settings adapter 1 window][virtualbox_network_settings_window_adapter_1]
![VirtualBox network settings adapter 2 window][virtualbox_network_settings_window_adapter_2]

One of the network adapters needs to be an _Host-only Adapter_ and its name should be the one that gets selected automatically by default, likely going to follow the _VirtualBox Host-Only XXXXX XXXXX (#XX)_ format.

The other network adapter has to be attached as _Internal Network_; create or select the already created network named _client_\__network_.
The _Advanced_ options apply for both network adapters.
Select the _PCNet FAST III (Am79C973)_ as the adapter type, since it is supported by nearly all _Operating Systems_.
The _Promiscuous Mode_ option should be left unchanged, i.e., with the _Deny_ value.
If needed, it is also possible to generate a new MAC address.
There is also the option to have the virtual machinhe detect the network cable is pluged in to each of the two network adapters in question.
To finish, click _OK_ in order to confirm and close the _Settings_ window.

### Note

Just a note on a possible notification VirtualBox might show about an invalid setting in the _Settings_ window: ![VirtualBox invalid setting notification][virtualbox_invalid_settings_notification]

VirtualBox will warn the graphics controller the virtual machine is configured to use is not the recommended one.
This mentioned controller is the controller Genymotion configured automatically during the virtual device creation.
There is no problem to leave it as it is, as it was how it was used throughout the experiments.
If desired there is also no problem to chage it to the recommended one, as it was tested to work as well.
To do so go to the _Display_ > _Screen_ tab and, in the _Graphics Controller_ field, choose the option VirtualBox recommends.

<br>

## CROSS-client mobile application initilization

To start the CROSS-client mobile application open Genymotion and start the device where it is installed by following one of these steps:

- Double-click in the created instance from the list of available devices;
- Right-click on the created device and then click _Start_;
- Click on the corresponding⋮button and then _Start_.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[genymotion_add_new_virtual_device_button]: ./screenshots/Genymotion_add_new_virtual_device_button.png "Genymotion add new virtual device button"
[genymotion_virtual_device_choice_window]: ./screenshots/Genymotion_virtual_device_choice_window.png "Genymotion choose virtual device window"
[genymotion_virtual_device_settings_window]: ./screenshots/Genymotion_virtual_device_settings_window.png "Genymotion virtual device settings window"
[virtualbox_network_settings_window_adapter_1]: ./screenshots/VirtualBox_network_settings_window_adapter_1.png "VirtualBox network settings adapter 1 window"
[virtualbox_network_settings_window_adapter_2]: ./screenshots/VirtualBox_network_settings_window_adapter_2.png "VirtualBox network settings adapter 2 window"
[virtualbox_invalid_settings_notification]: ./screenshots/VirtualBox_invalid_settings_notification.png "VirtualBox invalid setting notification"

<!-- Images declarations (reference style) - end" -->
