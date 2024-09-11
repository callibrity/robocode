# Callibrity Robocode

## Setup

1. Fork this repo (or clone it and create a branch)
2. Install Java v17 (may have issues with a newer version of Java)
3. Download the Robocode Setup JAR from [sourceforge.net/projects/robocode/](https://sourceforge.net/projects/robocode/files/robocode/1.9.5.2/robocode-1.9.5.2-setup.jar/download)
4. Run the Robocode Setup jar:
`java -jar ./robocode-1.9.5.2-setup.jar`
5. Install Maven:
  - MacOS: `brew install maven`
  - Linux: Use your package manager. i.e. `apt install maven`
  - Not sure about Windows
6. Run Robocode:
`~/robocode/robocode.sh` (or equivalent in other OSes)
7. Run `./build.sh`
  - Should create `target/*`
8. In the Robocode menus:
  - Select `Options -> Preferences`
  - Go to the `Development Options` tab
  - Click the `Add` button and add `[callibrity-robocode]/target/classes` to the list of paths

You should now be able to create new bots in `[callibrity-robocode]/src/main/java/robots/[whatever]`, and after running `./build.sh` you can add those bots to a battle (using `Battle -> New` in Robocode). 

Robots should be in the `robots` package, but you can create sub-packages for your bots (i.e. `robots.callibrityBot`). (This is a requirement of the Maven build.)

There are many sample bots available, and the Robocode Wiki has a lot of other information about the types of bots you can create and how to code them.

You may use the sample bots as a base for any bots you want to create, and you can use the wiki and publicly-available bots for inspiration. However, to keep this fun and competitive, please only enter your own, original creations in the Callibrity Battles.

## Submitting Bots

Package your bot(s) by using the `Robot -> Package Robot or Team` option within the Robocode interface. This will create a `.jar` file that you can send to me (Aaron Tyler) on Slack or Email.

## Other Info
The [RoboWiki](https://robowiki.net/wiki/Main_Page) provides all the information needed to get started.

Robots are written in Java, but the docs mention the ability to write bots in .NET as well. Feel free to try that if you'd like, but if additional setup is needed to execute .NET bots, please give me a heads-up so I can try to get it working before the Callibrity Battles.

## Competition Rules
- You may enter as many bots as you want. All of your bots should be in the same package.
  - THIS IS NOT A TEAM BATTLE. Your bots should be independent bots, and not coded to work together in any way. You bot should not have any knowledge of your other bots. (i.e., you can't code your bot to only fire at bots that aren't yours.)
  - If using this maven script, it says to put your robots in the `robots` package. You can create `robots.myBotPackage` for your bots.
  - When packaging your bot, it is recommended that you include the source code. This allows others to learn and improve.
  - The bots will be shared with everyone on the Slack channel after each battle to keep up the competition.
- All bots will be added to a 1000x1000 battlefield
  - Battlefield Size may be increased if we end up with lots of bots
- All other options for the battle will be the default options:
  - Number of Rounds: 10
  - Gun Cooling Rate: 0.1
  - Inactivity Time: 450
  - Sentry Border Size: 100



## Source
This repo was created from fernandrone's repo here:
https://github.com/fernandrone/robocode-maven

The original README.md file is below. You can try to get it working with the linked Docker container, but I couldn't get it working on MacOS. If you get it working, please share with the rest of us!

---

The rest of the README is from the original repo that I copied.

# Robocode-maven

A framework for easy development and sharing of [Robocode](http://robocode.sourceforge.net/) robots, setup as a [Maven](https://maven.apache.org/) project and adapted to work with the containerized [Robocode-docker](https://github.com/fbcbarbosa/robocode-docker).

## Requirements

To build the project you'll require `maven` and to run [Robocode-docker](https://github.com/fbcbarbosa/robocode-docker) you'll need `docker`.

## Installation

1. Clone Robocode-maven where you want it installed. A good place to pick is `$HOME/robocode` (but you can install it somewhere else).

  ```
  $ git clone https://github.com/fbcbarbosa/robocode-maven.git ~/robocode
  ```

2. Define the environment variable `ROBO_ROOT` to point to the path where the repo is cloned and add `$ROBO_ROOT` to your `PATH`:

  ```
  $ echo 'export ROBO_ROOT="$HOME/robocode"' >> ~/.bashrc 
  $ echo 'export PATH="$ROBO_ROOT:$PATH"' >> ~/.bashrc
  ```
  
3. Restart your shell so the path changes take effect.

  ```
  $ exec $SHELL
  ```

4. Build the project one time using Maven. It will download all the required packages once, including the Robocode API, so be a little patient.

  ```
  $ cd $ROBO_ROOT && mvn clean install
  ```

5. Run 'robo' script to launch [Robocode-docker](https://github.com/fbcbarbosa/robocode-docker). The first time may take a while as it downloads the 'fbcbarbosa/robocode' image.

  ```
  $ robo
  ```

And that's it! 

> **Note:** if done properly, the sample robot `robots.first.MyFirstRobot` should be available. Otherwise, go through the installation steps again carefuly, either the maven build failed or you have set an environment variable incorrectly.
  
## Developing robots

Simply add the installation folder to your favorite IDE as a Maven Project! 

Make sure that every new robot you develop is added under the `robots` package, within the `$ROBO_ROOT/src/main/java/robots` folder (their `.class` files will then be under `$ROBO_ROOT/target/classes/robots`, which is where Robocode reads them from). Feel free to add subpackages, e.g. `robots.mybots` at `$ROBO_ROOT/src/main/java/robots/mybots`.

To build your robots run Maven on the root of the installation folder:

```
$ cd $ROBO_ROOT && mvn clean install
```

They will become instantly available on Robocode under the `robots.*` package (you might have to refresh the robot list in the `New Battle` view with `CTRL+R`)

> **Note:** you *can* use Robocode's functional, yet limited, IDE to develop your robots, even as it's running on a container. However it will be hard to retrieve them at the host machine later, so it's not recommended. Besides, if you're ok using Robocode's IDE, why'd you download this framework?

Don't forget to commit your robots on a public GitHub repository so that everyone can learn from them :)
