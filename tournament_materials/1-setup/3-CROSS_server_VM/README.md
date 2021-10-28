# CROSS-server setup

Here one can find the instructions to install and setup the virtual machine for the CROSS-server.

It will only be used [later](./###virtual-machine-settings-configuration) but, to save some time, one can start to download the file with the Ubuntu 20.04 image disk [here](https://drive.google.com/file/d/1Db_hhf_9uj8xnHvg1MqwIZzsSwSlrIVQ/view?usp=sharing "ubuntu-20.04.2.0-desktop-amd64 disk image, located in the SureThing project Google Drive folder") (SHA256SUM: 93bdab204067321ff131f560879db46bee3b994bf24836bb78538640f689e58f).

<br>

## Virtual machine instance creation

Create a new instance of a virtual machine by going to _Machine_ > _New..._.
In the window that opens (_Create Virtual Machine_) give a name to the virtual machine, e.g., CROSS-server, and choose the folder where you would like to place the files of the virtual machine.
Next, fill the next two fields.
In the _Type_ field choose _Linux_ and in the _Version_ field pick _Ubuntu (64-bit)_.
For the memory to be made available to the virtual machine, 2 GB of RAM is enough.
Finally, choose the _Create a virtual hard disk now_ option.
Click _Create_ to continue with the setup process:
![VirtualBox create virtual machine window][virtualbox_create_virtual_machine_window]

In the next window that opens up (_Create Virtual Hard Disk_), VirtualBox will save the virtual hard disk in the previously chosen location but there is the option to change it.
For the size of the virtual hard disk, 20 GB should be enough.
You can leave the option selected by default (_VDI (VirtualBox Disk Image)_), but make sure the _Dynamically allocated_ is the selected option in the _Storage on physical hard disk_ field.
Lastly, click _Create_ to create an instance for the specified virtual machine:

![VirtualBox create virtual hard disk window][virtualbox_create_virtual_hard_disk_window]

<br>

## Virtual machine settings configuration

Once the virtual machine instance is created, open its _Settings_ window.
In that window go to the _System_ > _Processor_ tab.
Confirm the virtual machine is set to only use 1 CPU:

![Virtualbox settings window showing the system options][virtualbox_system_settings_window]

Next go to the _Display_ tab and, in the main _Screen_ tab, increase the video memory provided to the virtual machine, e.g., to 128 MB:
![Virtualbox settings window showing the display options][virtualbox_display_settings_window]

In the _Storage_ tab select the _Empty_ entry, from the storage controller, for instance _Controller: IDE_:
![Virtualbox settings window showing the storage options before mounting the virtual disk][virtualbox_storage_settings_window]

Once highlighted, click the button to open the dropdown menu with the existing options:
![Virtualbox choose virtual disk button icon][virtualbox_storage_settings_choose_virtual_disk_button_icon]

In the dropdown menu, click the _Choose a disk file..._ option and select the location where the Ubuntu image disk file is.
The virtual image disk will then show as attached to the virtual machine, as such:
![Virtualbox settings window showing the storage options after mounting the virtual disk][virtualbox_storage_settings_window_with_virtual_disk]

Disable audio, as it is not necessary, by going to the _Audio_ tab and unselecting the _Enable Audio_ option:
![VirtualBox settings window showing the audio option][virtualbox_audio_settings_window]

Moving on to the _Network_ tab, enable one network adapter; select it as attached to _Internal Network_ and create a network with the _server_\__network_ name.
Expanding the _Advanced_ options, both the _Adapter Type_ and _Promiscuous Mode_ options to be used by the virtual machine can be left with the default values, respectively _Intel PRO/1000 MT Desktop (82540EM)_ and _Deny_.
If desired, it is possible to generate a new MAC address with the option to have the virtual machinhe detect the network cable is pluged in to this network adapter.
At the end, click _OK_ to confirm and close the _Settings_ window:

![VirtualBox settings window showing the network options][virtualbox_network_settings_window]

<br>

## Ubuntu distribution installation

There are three ways to start the newly created virtual machine:

- Double-click the virtual machine instance;
- Select the virtual machine instance from the list and then at the top of the section with the details of the virtual machine click _Start_;
- Right-click on the instance of the virtual machine from the list and then click _Start_ > _Normal Start_.

Once the virtual machine boots, follow the on-screen instructions in order to install Ubuntu.

<br>

## Installation and configuration commands

### Go/Golang installation and configuration

As described in the [README](https://github.com/inesc-id/CROSS-server/blob/master/README.md "CROSS-server GitHub repository README") (kudos to Miguel Francisco) of the repository with the code of the CROSS-server, the first step is to install a [Golang](https://golang.org/ "Go/Golang website") environment, version 1.13 recommended.
A binary release of this version is available [here](https://drive.google.com/file/d/1YVrb9uHYG07OvdUFpAVa3WYDrYGIRojL/view?usp=sharing "go1.13.linux-amd64.tar.gz archive, located in the SureThing project Google Drive folder") (SHA256SUM: 68a2297eb099d1a76097905a2ce334e3155004ec08cdea85f24527be3c48e856).

Extract it into the _/usr/local_ directory, like so:

```bash
$ sudo rm -rf /usr/local/go && tar -C /usr/local -xzf go1.13.linux-amd64.tar.gz
```

Install the [dep](https://github.com/golang/dep "Go/Golang dependency manager tool GitHub page") dependency manager tool:

```bash
$ sudo apt-get install go-dep
```

Next, it is time to configure the environment variables.
Namely, add the environment variable `GOPATH` and add the installation of the Go tree to the `PATH` environment variable.
It can be done by adding the following lines to the **~/.profile** file (`$ nano ~/.profile`), with the facultative first (comment) line:

```bash
#Golang
export GOPATH=$HOME/go
export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
```

To apply these changes, run the following command:

```bash
$ source ~/.profile
```

One can then confirm the values of both the `PATH` and `GOPATH` environment variables and the Go version, respectively, by entering the following two commands:

```bash
$ printenv | grep PATH
$ go version
```

<br>

### CROSS-server respository clone process

Next, clone the repository that holds the code of the CROSS-server:

```bash
$ mkdir -p ~/go/src/github.com/inesc-id && cd ~/go/src/github.com/inesc-id/
$ git clone https://github.com/inesc-id/cross-server.git
```

<br>

### PostgreSQL installation and configuration

The next step is to install _PostgreSQL_, the relational database used by the CROSS-server:

```bash
$ sudo apt install postgresql postgresql-contrib
$ sudo -u postgres psql
```

<!-- TODO: Confirm the commads used to create the new role are correct and if there are none missing -->

Create a _PostgreSQL_ role/user, by entering the following commands in the _PostgreSQL_ interactive terminal (_psql_):

```sql
postgres=# create user cross with superuser password 'server_123';
postgres=# \du
postgres=# \q
```

After the successful creation of the new role/user, enter the _psql_ terminal again but now using the _cross_db_ user<!-- TODO: Confirm if cross_db is a user/role, ...-->:

```bash
$ psql cross_db
```

Once there, create a database and run two queries that are used to create and populate the database tables:

```sql
cross_db=# create database cross_db;
cross_db=# \i CROSS-server/schema.sql
cross_db=# \i CROSS-server/data.sql
cross_db=# insert into dataset (id, version) values ('main', '2020-11-06T12:00:00Z');
```

<br>

### CROSS-server database configuration

Next, in order to change the path to the database CROSS-server uses, edit the `databaseURI` field in the **secrets-debug.json** file (`$ nano CROSS-server/secrets-debug.json`) to the following:

```
postgresql://[cross]:[server_123]@[localhost]:[5432]?sslmode=disable&dbname=[cross_db]
```

<br>

### CROSS-server build process

To make `dep` install all the necessary dependencies of the project, run:

```bash
$ cd CROSS-server
$ dep ensure
```

Next, compile the code and create an executable by running the following command:

```bash
$ go build
```

Before running the executable, go the **main.go** file and comment out **line 156**.

To start the CROSS-server, run the following command inside the directory where it was installed (_~/go/src/github.com/inesc-id/CROSS-server_):

```bash
$ ./CROSS-server &
```

The CROSS-server process will run in background, while leaving the terminal session free to receive any subsequent input.

<br>

### System startup CROSS-server script configuration

To make the whole process of initilizing the CROSS-server, one can have it run automatically at system startup.

Create the _start_cross_server.sh_ file, e.g., in the _~/Documents/scripts_ directory (`$ nano ~/Documents/scripts/start_cross_server.sh`), and enter the following lines:

```bash
#!/bin/bash

# Starts a process for the CROSS server and redirects its output (including any possible errors) to a file
cd /home/<username>/go/src/github.com/inesc-id/CROSS-server && ./CROSS-server &>> /home/<username>/Documents/logs/cross_server_log.txt
```

, where `<username>` is the username entered during the [Ubuntu distribution installation](./##ubuntu-distribution-installation "Ubuntu distribution installation section").
After editing it run the `$ chmod +x start_cross_server.sh` command, in order to make it executable.

Next it needs to be added to the set of processes that run at system startup, following the next steps:

1. Open the _Startup Applications_ program (accessible via the _Show Applications_ Ubuntu menu):
   ![Startup Applications program as it shows in the menu][show_applications_menu]

2. Click the _Add_ button, as shown below:

   ![Startup Applications window before adding the start_cross_server.sh script to system startup][startup_applications_window]

3. Enter the information in each of the fileds in the window (_Add Startup Program_) that opens up:
   ![Startup Applications window showing the information for the start_cross_server.sh script][startup_applications_add_new_program_window_start_cross_server_script]

- Give it a name, e.g., CROSS-server;
- Go to the directory with the just created script (_start_cross_server.sh_) and select it;
- Leave a comment in the corresponding field, if desired.

4. Click _Add_ to confirm the entered information and return to the main window:
   ![Startup Applications window showing the start_cross_server.sh script already added to the system startup process][start_cross_server_script_added_to_system_startup]

Now the next time the virtual machine boots, once the created system user logs in the CROSS-server executable process will start automatically.

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
[virtualbox_network_settings_window]: ./screenshots/VirtualBox_network_settings_window.png "VirtualBox settings window showing the network options"
[show_applications_menu]: ./screenshots/show_applications_menu.png "Startup Applications program as it shows in the menu"
[start_cross_server_script_added_to_system_startup]: ./screenshots/start_cross_server_script_added_to_system_startup.png "Startup Applications window showing the start_cross_server.sh script already added to the system startup process"
[startup_applications_add_new_program_window_start_cross_server_script]: ./screenshots/startup_applications_add_new_program_window_start_cross_server_script.png "Startup Applications window showing the information for the start_cross_server.sh script"

<!-- [startup_applications_add_new_program_window]: ./screenshots/startup_applications_add_new_program_window.png "Startup Applications window to add the information about a new program to add to system startup" -->

[startup_applications_window]: ./screenshots/startup_applications_window.png "Startup Applications window before adding the start_cross_server.sh script to system startup"

<!-- Images declarations (reference style) - end" -->
