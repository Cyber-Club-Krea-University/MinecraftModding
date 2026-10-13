# Getting Started

To get Skript working. First you need to make sure you have [Java installed](https://www.oracle.com/java/technologies/downloads/#jdk25-windows). Next you need to download [paper-mc](https://papermc.io/downloads/paper) and the [skript plugin jar](https://github.com/skriptlang/skript/releases).

Make sure to place the paper-mc jar file you downloaded in a directory. Next, run the jar with java. The first time it runs, a file called eula.txt will be generated. It should look something like this.
```txt
#By changing the setting below to TRUE you are indicating your agreement to our EULA (https://aka.ms/MinecraftEULA).
#Fri Oct 02 20:17:28 IST 2026
eula=false
```

Change the line that says `eula=false` to `eula=true`. Doing this means you're agreeing to the (minecraft eula)[https://www.minecraft.net/en-us/eula] (these are just the legal terms and conditions that you need to agree on so you can run a minecraft server).

Another files called `server.properties` should be generated. This is a config file with multiple options. For example, the `MOTD` or message of the data controls the descriptions of the server you see in the multiplayer menu. The `online-mode` setting decides on whether you want your server to authenticate users. Setting `online-mode` to false lets players without Mojang accounts join your server. 

Finally, a folder called plugins should be created. Place the skript plugin jar you downloaded in this folder.

Once you've agreed to the eula, if you run the paper mc jar file, the server should start and you will be able to join it if you connect to `localhost`, you will be able to join the server.