# FFUF installation

## Installation

To install FFUF, e.g., under ~/ffuf, run the following command which will download the archive of a prebuilt binary:

```bash
$ mkdir ffuf && cd ffuf
$ wget -P .  https://github.com/ffuf/ffuf/releases/download/v1.3.1/ffuf_1.3.1_linux_amd64.tar.gz
```

If desired, check its checksum by comparing its [value](https://github.com/ffuf/ffuf/releases/download/v1.3.1/ffuf_1.3.1_checksums.txt "FFUF releases files checksums") with the output of the following command:

```bash
$ sha256sum ffuf_1.3.1_linux_amd64.tar.gz
```

Next, unpack it:

```bash
$ tar xf ffuf_1.3.1_linux_amd64.tar.gz
```

The executable is now available at ~/ffuf/ffuf (considering the downloaded archive was extracted into ~/ffuf).

<br>

## Check installation

To show information about the installed version, run:

```bash
$ ~/ffuf/ffuf -V
```

<br>

## Suggested wordlists installation

Here are the instructions to install the suggested wordlists.
To install the SecLists collection run the following command, considering Kali Linux was installed in the [attacker machine](../../../../1-setup/attacker_VM "Attacker machine setup folder") by following the [installation steps](../../../../1-setup/attacker_VM/README.md "Attacker machine setup steps"):

```bash
$ sudo apt -y install seclists
```

SecLists is now available under _/usr/share/seclists_.
To confirm/check it:

```bash
$ ls /usr/share/seclists
```

To make the RobotsDisallowed collection usable, just clone its [repository](https://github.com/danielmiessler/RobotsDisallowed "RobotsDisallowed project GitHub repository"), e.g., to the _/usr/share/robots-disallowed-lists_ directory, as such:

```bash
sudo git clone https://github.com/danielmiessler/RobotsDisallowed /usr/share/robots-disallowed-lists
```

One can then confirm and access it:

```bash
$ ls /usr/share/robots-disallowed-lists
```
