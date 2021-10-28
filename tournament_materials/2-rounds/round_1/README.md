# First round

The first round is divided in two parts, where players have to use a set of specific tools.
In the first one, players are asked to use [vulnerability analysis](1-vulnerability_analysis/ "Vulnerability analysis folder") tools against the [target system](../../#target-system "Target System section").
Where in the second part of the round, players will have to perform some [fuzzing techniques](2-fuzzing/ "Fuzzing folder").

<br>

## Attacks to perform

### 1 Nmap

#### 1.1 CROSS-server port

Confirm/discover the port where the CROSS-server service is running (by default) in the virtual machine where it is installed.

#### 1.2 CROSS-server open ports

Show if there are any other open ports in the [virtual machine](../../1-setup/3-CROSS_server_VM "CROSS-server folder") where the CROSS-server is running.

<br>

### 2 OpenVAS

#### 2.1 Low-severity TCP vulnerability

Discover a low-severity TCP-related vulnerability implemented by the [virtual machine](../../1-setup/3-CROSS_server_VM "CROSS-server folder") where the CROSS-server is running.

<br>

### 3 Fuzzing (FFUF)

#### 3.1 Directory discovery

Discover the 8 (eight) paths/endpoints (sub-path(s) included) the CROSS-server makes available (either HTTP method).

<!-- TODO explain better -->

#### 3.2 Unauthorized database writes

Make unauthorized writes directly in specific tables of the database.

<br>

The next table shows the points players get for achieving each of the [previous attacks](./##attacks-to-perform "First round attacks to perform"):

| Attacks                                                                                                                     | Score points |                                                     Round part |
| --------------------------------------------------------------------------------------------------------------------------- | :----------: | -------------------------------------------------------------: |
| [CROSS-server port](./#11cross-server-port "CROSS-server port attack section") (1.1)                                        |      1       |          [Nmap](1-vulnerability_analysis/1-Nmap "Nmap folder") |
| [CROSS-server open ports](./12#cross-server-open-ports "CROSS-server open ports attack section") (1.2)                      |      2       |          [Nmap](1-vulnerability_analysis/1-Nmap "Nmap folder") |
| [Low-severity TCP vulnerability](./#21low-severity-tcp-vulnerability "Low-severity TCP vulnerability attack section") (2.1) |      2       | [OpenVAS](1-vulnerability_analysis/2-OpenVAS "OpenVAS folder") |
| [Directory discovery](./#31directory-discovery "Directory discovery attack section") (3.1)                                  |      5       |                          [Fuzzing](2-fuzzing "Fuzzing folder") |
| [Unauthorized database writes](./#32unauthorized-database-writes "Unauthorized database writes attack section") (3.2)       |      10      |                          [Fuzzing](2-fuzzing "Fuzzing folder") |

<br>

## Undisclosed suggestions

There are a few tips for the [first round](../2-rounds/round_1 "First attack round folder") that can be asked to be disclosed to players for a deduction in points scored.
The next table shows the type of tips and the corresponding points deduction after its disclosure:

| Tip                                                                                                                                             | Deducted points |                                                Round part |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | :-------------: | --------------------------------------------------------: |
| [Fuzzing](../2-rounds/round_1/#3fuzzing-ffuf "Fuzzing techniques attacks section") attacks (3)                                                  |        1        | [Fuzzing](../2-rounds/round_1/2-fuzzing "Fuzzing folder") |
| [Directory discovery](../2-rounds/round_1/#31directory-discovery "Directory discovery attack section") attack (3.1)                             |        3        | [Fuzzing](../2-rounds/round_1/2-fuzzing "Fuzzing folder") |
| [Unauthorized database writes](../2-rounds/round_1//#32unauthorized-database-writes "Unauthorized database writes attack section") attack (3.2) |        8        | [Fuzzing](../2-rounds/round_1/2-fuzzing "Fuzzing folder") |
