## Minecraft Server on Termux / Android

The procedure described here how to installs and runs a **Minecraft Java Edition server** and **Minecraft Bedrock Edition server** on an **Android device** with Termux. **Root is not required**.

<br><br>

---

## Prerequisites

---

<br>

### Termux

You must have [Termux](https://termux.com/) installed on an android device. It is strongly advised install it from [F-Droid](https://f-droid.org/) (not from Google Play Store). Link : [Termux on F-Droid](https://f-droid.org/en/packages/com.termux/)

<br>

### Install Termux Package

Launch Termux and type the following commands. This allows us to update the termux packages, and to install the WGET command which will be useful to us later.

```shell
pkg update -y && pkg upgrade -y && pkg install wget -y
```

<br>

### Install JAVA

<br>

#### Main method

This is the recommended method. 

```shell
pkg install openjdk-17 -y
```

Use command `java -version` to verify that Java is installed correctly.

<br>

#### Alternative method 1

If the previous method did not work, you can proceed as follows:

```shell
wget https://raw.githubusercontent.com/MasterDevX/java/master/installjava && bash installjava
```

See [Termux Java GitHub](https://github.com/MasterDevX/Termux-Java) for more information.

<br>

#### Alternative method 2

If the previous method did not work, you can proceed as follows:

```shell
cd ~
apt-get install -y wget
hash -d wget
wget https://archive.org/download/openjdk-9-jre-headless_9.2017.8.20-1_x86_64/openjdk-9-jre-headless_9.2017.8.20-1_arm.deb
wget https://archive.org/download/openjdk-9-jre-headless_9.2017.8.20-1_x86_64/openjdk-9-jdk-headless_9.2017.8.20-1_arm.deb
apt-get install -y ./openjdk-9-jre-headless_9.2017.8.20-1_arm.deb ./openjdk-9-jdk-headless_9.2017.8.20-1_arm.deb
rm openjdk-9-*.deb

```

You can learn more about this method by consulting this stackoverflow topic : [How can I install java runtime on Android device?](https://stackoverflow.com/questions/61720889/how-can-i-install-java-runtime-on-android-device)

<br><br>

---

## Install Minecraft Server

---

<br>

### Server directory

For better user comfort, I invite you to create a directory in a shared space of the device as follows:

```shell
termux-setup-storage
cd ~/storage/shared
```

Create a folder for the server:

```shell
mkdir termux-minecraft-server
cd ./termux-minecraft-server/
```

<br>

### Download Server JAR

Now we will download the Minecraft server executable file. Here I am using [PufferFish server](https://github.com/pufferfish-gg/Pufferfish) 1.19 which has good performance. But it is possible to use other distros like Minecraft Vanilla, Bukkit, Papper-MC, ...

```shell
wget https://ci.pufferfish.host/job/Pufferfish-1.19/lastSuccessfulBuild/artifact/build/libs/pufferfish-paperclip-1.19-R0.1-SNAPSHOT-reobf.jar
mv pufferfish-paperclip-1.19-R0.1-SNAPSHOT-reobf.jar server.jar
```

<br>

You can also choose another distribution. Here are the commands for some of the best known :

```shell

# Server Bedrock : Nukit
wget https://ci.opencollab.dev/job/NukkitX/job/Nukkit/job/master/lastSuccessfulBuild/artifact/target/nukkit-1.0-SNAPSHOT.jar
mv nukkit-1.0-SNAPSHOT.jar server.jar

# Server Bedrock : Vanilla 1.19.1
https://minecraft.azureedge.net/bin-linux/bedrock-server-1.19.1.01.zip


# Server Java : PufferFish 1.18.2
wget https://ci.pufferfish.host/job/Pufferfish-1.18/lastSuccessfulBuild/artifact/build/libs/pufferfish-paperclip-1.18.2-R0.1-SNAPSHOT-reobf.jar
mv pufferfish-paperclip-1.18.2-R0.1-SNAPSHOT-reobf.jar server.jar


# Server Java : Vanilla 1.19
wget https://launcher.mojang.com/v1/objects/e00c4052dac1d59a1188b2aa9d5a87113aaf1122/server.jar


# Server JAva : Vanilla 1.18.2
wget https://launcher.mojang.com/v1/objects/c8f83c5655308435b3dcf03c06d9fe8740a77469/server.jar
```

<br>

### Accept EULA

To accept the Minecraft Terms of Use, use the following command:

```shell
echo "eula=true" > eula.txt
```

<br>

---

## Start the server

---

To start the server, you can use the command as below:

```shell
java -jar server.jar nogui
```

<br>

It is also possible to better control the memory allocated by Java for running Minecraft by specifying `-Xms` and `-Xmx` parameters as follows

```shell
java -Xms512M -Xmx1536M -jar server.jar nogui
```

<br>

To know your local ip, you can use the command `ifconfig`. To know your external ip, go to [https://wprock.fr/en/t/ip/](https://wprock.fr/en/t/ip/). To check your ports, use [https://portchecker.co/check](https://portchecker.co/check).
