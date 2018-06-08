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

    sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-10.0.1/bin/java 1
    sudo update-alternatives --config java

Follow the prompt to select JDK 10 as the default.

    username@aeson:~$ java -version
    java version "10.0.1" 2018-04-17
    Java(TM) SE Runtime Environment 18.3 (build 10.0.1+10)
    Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10.0.1+10, mixed mode)

It wasn't entirely necessary to use Oracle JDK 10 for this project, but it worked (w/ Linux 4.9.0.6-amd64...and on a 2007 MacBook, ha!) and perhaps it will future-proof the default JDK for some time.


#
**Users & Groups**

#
**MaryTTS (Client, Server, and Component Installer)**



    $ cd ~/
    $ git clone https://github.com/mysteryson34/marytts.git
    $ cd marytts
    $ sudo -u username git fetch --tags
    $ sudo -u username git checkout v5.2
    $ sudo unzip marytts-5.2.zip
    $ cd marytts-5.2/bin

From here we have a few more chores to do. As we did before, we want to make associations prior to firing anything up.

    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-client /usr/bin/marytts-client
    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-server /usr/bin/marytts-server
    $ sudo ln -s /home/username/marytts/marytts-5.2/bin/marytts-component-installer /usr/bin/marytts-component-installer
    $ sudo update-alternatives --install /usr/bin/marytts-client marytts-client /home/username/marytts/marytts-5.2/bin/marytts-client 1
    $ sudo update-alternatives --install /usr/bin/marytts-server marytts-server /home/username/marytts/marytts-5.2/bin/marytts-server 1
    $ sudo update-alternatives --install /usr/bin/marytts-component-installer marytts-component-installer /home/username/marytts/marytts-5.2/bin/marytts-component-installer 1
    
Even though *this project still needs the code to auto-start the local text-to-speech services*, I wanted to ensure that the MaryTTS client, server, and voice component installer are each accessible through a clickable GUI menu (I use a minimal LXDE build). *I'm not actually certain that my update-alternatives and symbolic links routines are the most appropriate/effective*, so having shortcuts in my menu system are a good back-up plan.

    $ sudo nano /home/username/.local/share/applications/MaryTTS-client.desktop

Paste the following text into the file.

        $ [Desktop Entry]
        $ Name=Trello
        $ Exec=/full/path/to/folder/Trello
        $ Terminal=false
        $ Type=Application
        $ Icon=/full/path/to/folder/Trello/resources/app/static/Icon.png
