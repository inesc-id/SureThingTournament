# Tournament rules

The following rules and recommendations apply to the entire duration of the tournament in question.

<br>

## Goals

Players will perform _Vulnerability Assessment_ and _Penetration Testing_ on the target system, the `CROSS-server`.
The scope of the attacks is on the _server-side_.

Players have to use and perform the attacks against/using a specific configuration.
For that, players need to follow the [installation instructions](../1-setup "Setup folder") for the correct configuration of the virtual machines and virtual networks to use throughout the tournament.

<!-- Change the rule about players having to stricly follow the installation instructions to players having to solely use the provided virtual machines' images if we then decide to provide it -->

The tournament consists in [two separate rounds](../2-rounds "Attack rounds folder").
Each round has a specific goal set, where players will have to use a different toolset.

<!-- The approach to follow when performing these attacks is discussed [later](../2-rounds "Attack rounds folder"). -->

Rules related with a specific step or attack round will be discussed in the corresponding subfolder in the [rounds](../2-rounds "Attack rounds") folder.

Each sucessfull attack will be scored by referees.
The winner of the tournament will be the player with the best final score.

<br>

## Scoring

Both [rounds](../2-rounds "Attack rounds") have a set of goals, where each goal has a set of points players can score.
More specific scoring instructions are described in the folder of the corresponding round.
For instance, points players can score for achieving a goal as part of the [first round of attacks](../2-rounds/round_1 "First attack round folder") are described in the [corresponding folder](../2-rounds/round_1/##attacks-to-perform "Attacks to perform for the first round section").
To score, players have to successfully achieve an attack goal but also **report** the results by showing how the attack was done, i.e., the attack has to the reproducible.

Overall, faster successful attacks are scored more points, i.e., players can score more points by achieving a goal faster.
The table below shows how many additional points players can score according to how fast a goal is achieved:

| Goal-achievement order | Points |
| ---------------------- | :----: |
| 1st                    |   15   |
| 2nd                    |   10   |
| 3rd                    |   5    |
| remaining              |   0    |

Some goals are verified automatically while others have to be [manually reviewed](./#manual-scoringrevision "Manual scoring/revision section"), case by case, by the referees.

### Manual scoring/revision

Goals/attacks that need to be manually reviewed are the ones that players can perform as part of the [second round](../2-rounds/round_2 "Second attack round folder").
For that, there are 3 (three) referees/judges in order to decide, and therefore score, those goals that require a manual revision.

<br>

## Schedule

A schedule with the times and an estimate for the completion of both [attack rounds](../2-rounds "Attack rounds") is shown below.
The total duration of the tournament is 2 days, although with free time where the tools run unattended.
As one can see, real hacking takes time... :)

<!-- TODO: Uncomment the times for official tournament(s) -->

Day 0 - [Setup](../1-setup "Setup folder") (estimated duration: 3 hours).

Day 1:

- <!-- 09:00 - -->
  Start of [round 1](../2-rounds/round_1 "First attack round folder");
- <!-- 09:00 - -->
  Nmap (estimated duration: 3 hours, unattended: 2 hours);
- <!-- 12:00 - -->
  OpenVAS (estimated duration: 6 hours, unattended: 5 hours);
- <!-- 18:00 - -->
  Fuzzing (estimated duration: 3 hours, unattended: 1 hours);
- <!-- 21:00 - -->
  End of [round 1](../2-rounds/round_1 "Attack round 1 folder").

Day 2:

- <!-- 09:00 - -->
  Start of [round 2](../2-rounds/round_2 "Attack round 2 folder");
- <!-- 18:00 - -->
  End of [round 2](../2-rounds/round_2 "Attack round 2 folder").

**Total:**
<br>
Active hours: around 10 hours (including [setup](../1-setup "Setup folder") time), depending on the attacks performed during the [second round](../2-rounds/round_2 "Attack round 2 folder");
<br>
Elapsed time: 24 hours (including unattended time).

<br>

## Results submission

Players have to first create a private GitHub repository based on a [template](https://github.com/inesc-id/SureThingTournament "Tournament GitHub repository to be used as a repository template") and give read permissions to the [jozeus](https://github.com/jozeus "jozeu's GitHub profile page") user.
For more information about creating a repository from a template, access this [page](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template "Creating a repository from a template GitHub docs page").

In the repository players have to use to submit their results, one can find two main folders: one for each attack round.
Inside of each there should be folders for each of the attacks players perform.
For the [first round](../2-rounds/round_1 "First attack round folder"), there are already folders for each of the attacks players are asked to perform.
In the case of the [second round](../2-rounds/round_2 "Attack round 2 folder"), players must follow the same folder structure by adding any necessary folders.
Players must use README files to report each performed attack: a description about how the attack was done along with an overview of the gathered results.

**Note:** The submitted results should contain any and all gathered artifacts, such as, produced scripts, terminal logs, and the [CROSS-server's output](../1-setup/3-CROSS_server_VM/#system-startup-CROSS-server-script-configuration "System startup CROSS-server script configuration section").
If the produced data for an attack is in a single file then place it inside the corresponding attack foler **along** with the [CROSS-server log output file](../1-setup/3-CROSS_server_VM/#system-startup-CROSS-server-script-configuration "System startup CROSS-server script configuration section") produced during the time the attack took place.
Else, if that data is in more than one file, create a folder inside the attack folder and place each file with the produced data **along** with the corresponding [CROSS-server output](../1-setup/3-CROSS_server_VM/#system-startup-CROSS-server-script-configuration "System startup CROSS-server script configuration section") produced during the time the attack took place.

For example, for the results gathered after using [OpenVAS](../2-rounds/round_1/1-vulnerability_analysis/2-OpenVAS "OpenVAS folder"), players have to place all reports (in _.xml_ format), following a specific name format and inside a specific folder.

As soon as players successfully perform an attack and are ready to submit the gathered results, access the [**submission form**](https://forms.gle/JJpCVRNSa5L5GANk9 "Results submission form") (same form to submit both [rounds](../2-rounds "Attack rounds folder") results).
In the form in question, if the performed attack is part of the [first round of attacks](../2-rounds/round_1 "First attack round folder"), select the attack from the list.
Else, if it is an attack from the [second round](../2-rounds/round_2 "Second attack round folder"), describe the attack instead in the corresponding text area.
Also in the form, add the identifier(s) of the commit(s) that contain the results for such attack.

<!-- TODO: Uncomment for official tournament(s) -->
<!-- <br>

## Prizes

Participation price - a pen?

Winner prize - a raspberry pi kit?

<br>

## Final standings: winner announcement

After the referees evaluate the submissions - which can take up to 24 hours - the results, and the winner - are announced on ... -->
