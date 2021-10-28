# Undisclosed suggestions

<!-- Suggestions/tips that can be disclosed to players (for a points deduction) when asked -->

| Tip                                                                                                                                                   | Deducted points | Round part |
| ----------------------------------------------------------------------------------------------------------------------------------------------------- | :-------------: | ---------: |
| [Fuzzing attacks general tip](./#directory-discovery-attacks-general-tip "Fuzzing attacks general tip section") attacks (3)                           |        1        |    Fuzzing |
| [Directory discovery attack tip](./#directory-discovery-attack-tip "Directory discovery attack tip section") attack (3.1)                             |        3        |    Fuzzing |
| [Unauthorized database writes attack tip](./##unauthorized-database-writes-attack-tip "Unauthorized database writes attack tip section") attack (3.2) |        8        |    Fuzzing |

<br>

## Fuzzing attacks general tip

Players will want to consider **\v1** as the root/main path/endpoint.
Meaning all performed
fuzzing techniques<!-- [fuzzing techniques](... /2-rounds/round_1/#3fuzzing-ffuf "Directory Discovery attack section") -->
should be targeted at **\v1** instead of the **\\** path/endpoint.

<br>

## Directory discovery attack tip

For the
directory discovery<!-- [directory discovery](... /2-rounds/round_1/#31directory-discovery "Directory Discovery attack section") (3.1) -->
attack, use the following wordlists:

- [_directory-list-2.3-big.txt_](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/directory-list-2.3-big.txt "SecLists GitHub page - directory-list-2.3-big.txt wordlist"), available at `/usr/share/sec-lists/Discovery/Web-Content/directory-list-2.3-big.txt` in the machine of the attacker;
- [_top10000.txt_](https://github.com/danielmiessler/RobotsDisallowed/blob/master/top10000.txt "RobotsDisallowed project GitHub page - top10000.txt wordlist"), available at `/usr/share/robots-disallowed-lists/top10000.txt at the machine of the attacker`, if it was installed following the provided installation instructions for the recommended wordlists to use.

<br>

## Unauthorized database writes attack tip

Players will want to use the following wordlist to send POST requests to different endpoints:
[_big-list-of-naughty-strings.txt_](https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/big-list-of-naughty-strings.txt "SecLists GitHub page - big-list-of-naughty-strings.txt wordlist"), available at `/usr/share/sec-lists/Fuzzing/big-list-of-naughty-strings.txt` in the machine of the attacker, if installed following the provided installation instructions for the recommended wordlists.
