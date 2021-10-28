# Second round

The goals set for this round are not strictly defined, meaning it is suggested a few attacks players may try to perform but players are free to explore different ones.
As such, unlike the [first round](../round_1 "First attack round folder"), players are free to choose the attack tools to use.

## Attacks to consider

These are some of the attacks players may want to consider (in no particular order):

- Send requests that require authentication from the client-side (through the `Authorization` header) using previously captured values;

- Delete some entries, namely users, from the database;

- Write a specific value in the database. An example could be adding a new user of the [client mobile application](../../1-setup/2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application setup folder") directly to the database;

- Perform _impersonation/spoofing_ attacks, by assuming the identity of an already existing user of the system;

- Perform _replay_ attacks, by capturing a given message (or part of it) intended to a specific party, and after saving it for a certain period of time, send it to the recipient at a later time;

- Perform _network spoofing_ attacks;

- Ultimately, claim false location proofs/certificates, i.e., claim a location proof/certificate for a user of the system for a location they are not in fact at.

Next is a visual representation of some of the network-related attacks players may consider:

![Network related attacks to consider][network_related_attacks_to_consider]

Again, these are just suggested attacks.
Players are free to perform other attacks, as long as the [submission instructions](../../0-rules/##results-submission "Rules folder") followed.

<br>

## Suggested tools

Players can reuse the tools from the [first round](../round_1 "First attack round folder"), this time in different ways.
As a suggestion, next is a list of possible tools to consider for this second round (in no particular order):

- [_Wireshark_](https://wireshark.org/ "Wireshark's homepage") is a widely known network protocol and traffic analyzer (a "sniffer"). Repositories:

  - https://github.com/wireshark/wireshark (read-only);
  - https://gitlab.com/wireshark/wireshark.

- [_Metasploit_](https://www.metasploit.com/ "Metasploit's homepage") is a framework that works as an exploitation and vulnerability validation tool. Repository: https://github.com/rapid7/metasploit-framework;

- [_mitmproxy_](https://mitmproxy.org/ "mitmproxy's homepage") is an open source interactive tool that works as a proxy able to intercept, inspect, modify, and replay network traffic sent through HTTP/1 and HTTP/2 and HTTP over/protected by SSL/TLS (HTTPS). Repository: https://github.com/mitmproxy/mitmproxy;

- [_sqlmap_](http://sqlmap.org/ "sqlmap's homepage") is an open source tool that automates the process of detecting and exploiting SQL injection vulnerabilities, and later taking over SQL-like databases. Repository: https://github.com/sqlmapproject/sqlmap;

- [_tcpdump_](http://www.tcpdump.org/ "tcpdump's homepage") is a command-line network packet analyzer, intended for network traffic capture. It can be used to print the headers of packets, and even filter packets captured on a network interface that match a givn expression. Repository: https://github.com/the-tcpdump-group/tcpdump;

- [_MASSCAN_](https://github.com/robertdavidgraham/masscan "MASSCAN's GitHub repository") is a fast TCP port scanner that uses and relies on a custom TCP/IP stack to transmit SYN packets asynchronously;

- [_ntop(ng)_](https://www.ntop.org/ "ntop(ng)'s homepage") is a network traffic probing tool that can monitor the usage of a given network. Repository: https://github.com/ntop/ntopng;

- [_Wfuzz_](http://www.edge-security.com/wfuzz.php "Wfuzz's homepage") is a web applications bruteforcing tool (a fuzzer), allowing to perform several attacks such as directory discovery, and GET and POST parameters bruteforce. Repository: https://github.com/xmendez/wfuzz;

- [_Scapy_](https://scapy.net/ "Scapy's homepage") is a Python-based interactive network scanner and discovery tool. Working as a packet sniffer, manipulation, and generation tool, it is able to forge or decode packets of a wide number of network protocols. Repository: https://github.com/secdev/scapy/.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[network_related_attacks_to_consider]: ./images/network_related_attacks_to_consider.png "Network related attacks to consider"

<!-- Images declarations (reference style) - end" -->
