# OpenVAS installation

## Installation

The following steps assume the [attacker machine](../../../1-setup/attacker_VM "Attacker machine folder") was installed using the [provided instructions](../../../1-setup/attacker_VM/README.md).

First, one needs to install OpenVAS by entering the following command:

```bash
$ sudo apt-get install openvas
```

Once OpenVAS is installed, the next step is to run the following command that will issue all the necessary setting up:

```bash
$ sudo gvm-setup
```

At the end of the output of the setup, the automatically-generated password for the admin user is displayed.

Nevertheless, there is the option to change the password of the admin account.
Run the following command and enter the new desired password.

```bash
gvmd --user=admin --new-password=<password>
```
