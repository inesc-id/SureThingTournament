# Fuzzing

Fuzzing techniques (or just fuzzing) consists in the generation and submission of malformed data to an application or system.
Always with the end-goal of disrupting the normal functioning of the target, or even stopping its operation completely.

Instead of generating new data payloads, one way is using wordlists.

<br>

## Wordlists

A *wordlist* is a text file with a list of words of the same type.
Types of wordlists include possible or known passwords, and usernames, fuzzing payloads, or data pattern matching.
Wordlists can be used directly when fuzzing a target, making them quite useful when performing fuzzing techniques.

### Suggested wordlists collections

There are various available collections of wordlists.
Players are free to use any of the available ones.
Two recommended collections of wordlists are [SecLists](https://github.com/danielmiessler/SecLists "SecLists GitHub page") and [RobotsDisallowed](https://github.com/danielmiessler/RobotsDisallowed "RobotsDisallowed project GitHub page").

SecLists is a collection of multiple types of wordlists: from usernames and passwords to fuzzing payloads.

The RobotsDisallowed project has a list of several wordlists of the most commonly disallowed directories present in _robots.txt_ files that were found in top websites.

<br>

## FFUF as a fuzzing tool

[FFUF](https://github.com/ffuf/ffuf "FFUF GitHub page") (Fuzz Faster U Fool) is a web fuzzer written in [Go](https://golang.org/ "Go/Golang website").
Players will have to fuzz the [target system](../../../0-rules/#target-system "Target System section") as part of the [first round](../ "Attack round 1 folder") of the game.

### Goals

FFUF can be used to fuzz different aspects/parts of the [target system](../../../0-rules/#target-system "Target System section").
As a basic use, players are asked to use FFUF to do files or directory discovery.
Apart from that the goal is to try to slow down the response time of the target system, or even stop its operation altogether.
Ultimately, even be able to write in the database of the target system.

<br>

## Installation

At this point FFUF should already be installed in the [machine of the attacker](../../../1-setup/1-attacker_VM "Attacker machine setup folder"), as one can check [here](../../../1-setup/5-tools/3-FFUF/##check-installation "Check FFUF installation section").

<br>

## Usage

### Basic parameters usage

The basic available parameters are:

- `-v` to print more verbose output, as it is common;
- `-w` file path of the wordlist to use;
- `-u` the target URL or IP address;
- `-H` to define the header(s) to send;
- `-X` HTTP method to use;
- `-d` to define POST data to send;
- `-r` to follow redirects, `false` by default.

The basic usage is to use the **FUZZ** keyword anywhere in the URL/IP address (`-u`), headers (`-H`), or POST data (`-d`), which is then replaced by the values present in the used wordlist.
A simple example:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

Instead of using the _FUZZ_ keyword, one could run the previous command with:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000/W1 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:W!
```

As such, an example to fuzz multiple locations would be:

```bash
$ ~/ffuf/ffuf -u 192.168.21.X:13000/W1/W2 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:W1,/usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:W2
```

<br>

### Directory discovery usage example

A typical directory discovery consists in adding the _FUZZ_ keyword at the end of the URL or IP address of the target, like so:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000/FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

<br>

### GET parameter discovery/fuzzing usage example

To fuzz the GET parameter:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000?FUZZ=test_value -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

Once the parameter name is known run:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000?known_value=FUZZ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

<br>

### POST data fuzzing usage example

To fuzz the data sent in a POST request, one would have to run:

```bash
$ ~/ffuf/ffuf -u 192.168.21.14:13000 -X POST -d "FUZZ" -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt
```

<br>

## Further information

Further information and/or other available commands are described in [FFUF's GitHub repository](https://github.com/ffuf/ffuf#example-usage "FFUF GitHub repository page").
