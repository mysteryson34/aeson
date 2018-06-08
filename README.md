# # *****aeson***** : 
**intelligent assistance for linux machines**

#                           ********IN DEVELOPMENT! I NEED HELP!********
#
                    Project Goals
                        - GOALSET #1: Customize & Integrate
                        - GOALSET #2: Communication & Connectivity 
                        - GOALSET #3: GUI & Web Interfaces
                        - GOALSET #4: Enhancement & Enrichment
                        - GOALSET #5: Builds & Platforms
#                       
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

The processes for completing these steps are almost identical on the *Stretch* releases of both **Debian** and **Raspbian** (tested on RPi models 3B and 3B+). Other versions of the JDK are likely to work, though it is recommended that you use the **Oracle** iterations of the software, if you can.

Other online instructions for MaryTTS (https://github.com/marytts/marytts/wiki/Local-MaryTTS-Server-Installation) will ask you to 1) create a *mary* user and a *mary* group. Then they will ask you to 2) *mkdir* and *chown* the **/local/mary/marytts** directory, where you would then 3) perform your git checkout. HOWEVER, *those* instructions also include 4) a (broken) method for compiling MaryTTS from its source. For the goals of the project, it is so-far unnecessary for the MaryTTS server to operate as a system user.

IDEA/NOTE: If you want a *true* MaryTTS server, the binaries could be installed on a headless Raspberry Pi. As it is being developed, AESON is conceived/tested using **two strategies** which I'll explain further on.


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

    $ sudo nano /home/username/.local/share/applications/

Paste the following text into the file (**MaryTTS-client.desktop**).

        $ [Desktop Entry]
        $ Name=MaryTTS Client
        $ Exec=/home/username/marytts/marytts-5.2/bin/marytts-client
        $ Terminal=false
        $ Type=Application
        $ Icon=/home/username/Theme/Linea/_software/_SVG expanded/software_layers2.svg

Save the file(*CTRL+c*) but do not close it. The next process is repetitive but I consider it necessary.

*NOTE* : The **Linea Icon Set** needs to be downloaded. Because we will likely use it for other aspects of this project, we need to put it somewhere memorable and set apart so that we can add other icon sets.

            $ cd ~/
            $ git clone https://github.com/mysteryson34/Linea-Iconset.git
            $ mkdir -p Theme/Linea
            $ cd Theme/Linea
            $ sudo mv ~/Linea-Iconset/* .
            $ cd ~/
            $ sudo rm -rf Linea-Iconset

*CTRL+o* to save under a new filename, **MaryTTS-server.desktop**, and modify the contents to look like so.

       $ [Desktop Entry]
        $ Name=MaryTTS Server
        $ Exec=/home/username/marytts/marytts-5.2/bin/marytts-server
        $ Terminal=true
        $ Type=Application
        $ Icon=/home/username/Theme/Linea/_basic/_SVG expanded/basic_server2.svg

Save the file(*CTRL+c*) but do not close it. The next process is repetitive but I consider it necessary (hehehe).

*CTRL+o* to save under a new filename, **MaryTTS-component-installer.desktop**, and modify the contents to look like so.

       $ [Desktop Entry]
        $ Name=MaryTTS Component Installer
        $ Exec=/home/username/marytts/marytts-5.2/bin/marytts-component-installer
        $ Terminal=false
        $ Type=Application
        $ Icon=/home/username/Theme/Linea/_basic/_SVG expanded/basic_headset.svg

Save the file(*CTRL+c*) and close out of your text editor.

Perform similar steps so that Google's **Material Design** Iconset is available for us to use when developing further aspectes of AESON.

#
**Strategies, Pros & Cons**

At the onset of this project I was over-ambitious about a "*cluster-y*" network of RPi microcomputers; each with its own dedicated purpose in the execution of this project's goals. While I learned **a lot** in my tinkerings (see below), this process came with some caveats, delights, disappointments, and surprises.

*WE ALL HAVE OUR QUIRKS & PREFERENCES*

In most situations where I use a Raspberry Pi, I am most-typically doing so headless-ly and via SSH/SFTP. I was influenced by Raspbian (lite) and - while installing Debian on my **old** MacBook - I decided not to include any preconfigurd desktop environments out-of-the-box, and to match Raspbian lite with my own amd64 rendition of Debian...lite? Below are some of the packages that I seem to need (?), as well as some of the procedures/pains that I went through on each platform.

I have some hardware that doesn't have immediate support on the RPi. I often use the Edimax EW-7822ULC/UTC adapter and it is handy for networked machines because it can operate on the 5GHz band. As you will later see, there are many combinations of uses/misuses for miscellaneous hardware attachments and the RPi. Fortunately, in this case, a fix was made available from Edimax (https://edimax.freshdesk.com/support/solutions/articles/14000062079-how-to-install-ew-7822ulc-adapter-on-raspberry-pi).

The next steps demonstrate how to *update and uprade* the software and hardware of the Raspberry Pi, as well as how to *build the full kernel* for the machine or for cross-compiling (further instructions at https://www.raspberrypi.org/documentation/linux/kernel/building.md).

In regards to my needs for USB-attached hardware devices, many drivers (open-source or otherwise) can easily be found and and cloned from the internet. If you intend on using hardware with the RPi, install the *raspberrypi-kernel-headers* package, then run this command and look at its output.

    $ ls /lib/modules/$(uname -r)
    build   modules.alias      modules.builtin.bin  modules.devname  modules.symbols      updates
    kernel  modules.alias.bin  modules.dep          modules.order    modules.symbols.bin
    misc    modules.builtin    modules.dep.bin      modules.softdep  source
    
If you cannot see a *build* folder after running that command, then you may at *any* point have trouble compiling binaries for drivers necessary for operability with a single-board computer like the RPi. The most recent *raspberrypi-kernel-headers* package may or may not provide you with the mysterious build folder. I could be wrong but I think that new full-kernel releases are sometimes/routinely delayed or omitted from Raspbian images because of the existence of kernel headers (must. do. more. learning.).  Thus, it has become common practice to "build the kernel" so that I can compile device driver binaries from great places like **github**.


    $ sudo apt-get update && sudo apt-get upgrade -y && sudo rpi-update && sudo apt-get clean && sudo reboot
    $ sudo apt-get install raspberrypi-kernel-headers bc git git-core libncurses5-dev -y
    $ cd ~/
    $ git clone --depth=1 https://github.com/raspberrypi/linux
    $ cd linux
    $ KERNEL=kernel7
    $ make bcm2709_defconfig
    
    $ make -j4 zImage modules dtbs  ## This takes a lot of time and I recommend a fan & heat sinks.
    $ sudo make modules_install
    $ sudo cp arch/arm/boot/dts/*.dtb /boot/
    $ sudo cp arch/arm/boot/dts/overlays/*.dtb* /boot/overlays/
    $ sudo cp arch/arm/boot/dts/overlays/README /boot/overlays/
    $ sudo cp arch/arm/boot/zImage /boot/$KERNEL.img
    $ sudo reboot

Because of the demand on the RPi and the microSD,  I recommend these steps followed by **backing up your microSD card onto a disc image(.img)** so that - as is always the case with learning and testing - you aren't stuck rebuilding the kernel on a daily basis or burning up your hardware.

    
    
    
    
    
    $ cd ~/
    $ git clone https://github.com/torvalds/linux.git
