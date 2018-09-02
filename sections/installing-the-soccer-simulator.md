# Installation

### Configuring the environment and installing the server and monitor

The following steps were tested and executed using Ubuntu Linux 12.04 and Debian Wheezy 7.

Open a terminal and run:

> sudo apt-get install g++ build-essential libboost-all-dev qt4-dev-tools libaudio-dev libgtk-3-dev libxt-dev

**UBUNTU**

Open a terminal and run the following commands:

> sudo apt-add-repository ppa:gnurubuntu/rubuntu <br>
> sudo apt-get update

This will automatically add an entry to  your source list based on your Ubuntu version.

Install the server and monitor:
> sudo apt-get install rcssserver rcssmonitor

**DEBIAN**

Install bison and flex:
> sudo apt-get install bison flex

Go to the Robocup Soccer Simulation official repository on SourgeForge by clicking [here](http://sourceforge.net/projects/sserver/files/) and download the files rcssserver-x.x.x.tar.gz and rcssmonitor-x.x.x.tar.gz.
_Note that x.x.x is the downloaded file version._

Extract rcssserver file:
> tar -zxpf rcssserver-x.x.x.tar.gz

Configure and compile rcssserver:
> cd rcssserver-x.x.x
> ./configure && make
> sudo make install

To install the rcssmonitor, go to the end of this article and follow the same steps to install the soccerwindow2 monitor.

**IMPORTANT: The steps above for Debian 7 were not tested in other linux distributions, but you can give a try.**

____________________________________________________________________________________

Now you can continue with the installation, either if you're using Ubuntu or Debian:

Go to the Robocup tools repository on SourgeForge by clicking [here](http://en.sourceforge.jp/projects/rctools/releases/).

Download these files:
- librcsc
- agent2d

Currently, the last versions of agent2d and librcsc are: [agent2d-3.1.1](http://en.sourceforge.jp/projects/rctools/downloads/55186/agent2d-3.1.1.tar.gz/) and [librcsc-4.1.0](http://en.sourceforge.jp/projects/rctools/downloads/51941/librcsc-4.1.0.tar.gz/). Go to the directory where you have saved the downloaded files and follow these steps (do it in this exact order!):  _Note that x.x.x is the downloaded file version._

Open a terminal and extract the files:

> tar -zxpf librcsc-x.x.x.tar.gz <br>
> tar -zxpf agent2d-x.x.x.tar.gz

**NOTE**: all the directories names where the librcsc files are saved must not contain spaces.

### Installing librcsc

**IMPORTANT:** _Information about all players are written in a log in which the dot(.) is used as decimal separator. Some languages,  as Portuguese, use comma as decimal separator causing an I/O error. 
Your system language must be English. If it is not, run the command `export LC_NUMERIC="C"` on a terminal to avoid any issues._

> cd librcsc-x.x.x/

Run the commands:

**Note:** _If you have permission problems in the first step, instead of_ `./configure` _execute_ `sh ./configure`.

> ./configure <br>
> make <br>
> sudo make install

### Installing agent2d

> cd agent2d-x.x.x/

Run: 

> ./configure <br>
> make <br>
> sudo make install

### (Optional) Installing the soccerwindow2 monitor

There is another monitor which has more detailed information about matches and players information. This monitor is used in the official Robocup World Cup. If you wish to install it, just run these commands:

In the RoboCup repository cited above in this tutorial, download this [file](http://en.sourceforge.jp/projects/rctools/downloads/51942/soccerwindow2-5.1.0.tar.gz/).

Open a terminal and run:

> tar -zxpf soccerwindow2-x.x.x.tar.gz <br>
> cd soccerwindow2-x.x.x.tar.gz <br>
> ./configure <br>
> make <br>
> sudo make install

**Troubleshoot**:

If you got this error (and you probably will):

> unrecognized command line option ‘-pthread-lQtGui’

Open the **configure** file, locate the line below and put a space between $PKG_CONFIG the variables, so it will be like this:

> QT4_LDADD="$($PKG_CONFIG --static --libs-only-other $QT4_REQUIRED_MODULES) $($PKG_CONFIG --static --libs-only-l $QT4_REQUIRED_MODULES)"

Source: http://askubuntu.com/a/892432/664657

### Conclusion

With all done, it is time to run a match and test if everything has done with no errrors. 
See the next tutorial [here](https://github.com/herodrigues/robocup2d-tutorial/blob/master/sections/running-a-match-with-agent2d.md).