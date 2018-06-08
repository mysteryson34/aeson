# aeson   :   intelligent assistant for linux machines



#
**Oracle Java JDK 10**

For this project, Oracle Java JDK 10.0.1 was initially installed from binaries located at 
http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html

Download the source *tar.gz* file to your home user directory (example: /home/username), then extract it.

    sudo tar zxvf *.tar.gz

The files should extract to a new directory (example /home/username/jdk-10.0.1) and you will want to create a symbolic link to this directory, like so.

    sudo ln -s /home/username/jdk-10.0.1 /usr/lib/jvm/jdk-10.0.1

Next, we need to make sure that our version of the JDK is the one that is automatically selected for use.

    sudo update-alternatives --install /usr/bin/java java /user/lib/jvm/jdk-10.0.1/bin/java 1
    sudo update-alternatives --config java

Follow the prompt to select JDK 10 as the default.

    user@aeson:~$ java -version
    java version "10.0.1" 2018-04-17
    Java(TM) SE Runtime Environment 18.3 (build 10.0.1+10)
    Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10.0.1+10, mixed mode)

It wasn't entirely necessary to use Oracle JDK 10 for this project, but it worked (w/ Debian 4.9.0.6-amd64...and on a 2007 MacBook, ha!) and perhaps it will future-proof the default JDK for some time.

#
**MaryTTS (Client, Server, and Component Installer)**

    cd ~/
    git clone https://github.com/mysteryson34/marytts.git
