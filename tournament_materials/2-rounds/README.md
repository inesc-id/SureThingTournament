# Attack rounds

The game consists in two separate rounds, where each round has a different goal set and tools.
The two rounds, and the attacks goals for each, are shown next:

![Different attack rounds][attack_rounds]

The [first round](round_1 "Attack round 1 folder") consists and has a smaller toolset, and a more specific goal set.
In the [second round](round_2 "Attack round 2 folder"), players are expected to try and use different attack tools.
Specific suggested tools are described in the corresponding folder.

<br>

## Required virtual machines

Before starting either the [first](./round_1 "First attack round folder") or the [second round](./round_2 "Second attack round folder") of attacks, make sure to have the necessary virtual machines running, namely:

- The [machine of the attacker](../1-setup/1-attacker_VM "Attacker machine folder");
- The [CROSS-client mobile application](../1-setup/2-CROSS_client/1-CROSS_client_mobile_application "CROSS-client mobile application folder");
- The [CROSS-server](../1-setup/3-CROSS_server_VM "CROSS-server virtual machine folder");
- The router virtual machine that emulates the [ISP of the attacker](../1-setup/4-routers/2-attacker_ISP "Attacker ISP router folder");
- The router virtual machine that emulates the [ISP of the client](../1-setup/4-routers/3-client_ISP "Client ISP router folder");
- The virtual machine that works as the [router of the network of the CROSS-server](../1-setup/4-routers/4-server_network_router "Server network router folder");
- The router [virtual machine that emulates the "Internet"](../1-setup/4-routers/5-Internet_router '"Internet" router folder').

<br>

## Suggestion

Players might find it handy to record the terminal logs produced by the [machine of the attacker](../1-setup/1-attacker_VM "Attacker machine folder"), that have to be [submitted later](../0-rules/##results-submission "Results submission section"), using the [`script`](https://man7.org/linux/man-pages/man1/script.1.html "script command manual page") Linux command.
Yet, players are free to choose how to record those terminal logs.

<!-- ############################################## -->

<!-- Images declarations (reference style) - start" -->

[attack_rounds]: ./images/attack_rounds.png "Different attack rounds"

<!-- Images declarations (reference style) - end" -->
