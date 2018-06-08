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
**Users & Groups**

#
**MaryTTS (Client, Server, and Component Installer)**



    $ cd ~/
    $ git clone https://github.com/mysteryson34/marytts.git
    $ cd marytts
    $ sudo -u user git fetch --tags
    $ sudo -u user git checkout v5.2
    $ sudo unzip marytts-5.2.zip
    $ cd marytts-5.2/bin

From here we have a few more chores to do. As we did before, we want to make associations prior to firing anything up.

    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-client /usr/bin/marytts-client
    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-server /usr/bin/marytts-server
    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-component-installer /usr/bin/marytts-component-installer
    $ sudo update-alternatives --install /usr/bin/marytts-client marytts-client /home/user/marytts/marytts-5.2/bin/marytts-client 1
    $ sudo update-alternatives --install /usr/bin/marytts-server marytts-server /home/user/marytts/marytts-5.2/bin/marytts-server 1
    $ sudo update-alternatives --install /usr/bin/marytts-component-installer marytts-component-installer /home/user/marytts/marytts-5.2/bin/marytts-component-installer 1
    
