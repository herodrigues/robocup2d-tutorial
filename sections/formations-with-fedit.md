# Formation Editor

**Installing fedit**

Download fedit in the Robocup's official repository [here]http://en.sourceforge.jp/projects/rctools/downloads/48791/fedit2-0.0.0.tar.gz/).

Open a terminal (CTRL+ALT+T), extract the files and execute:

> tar -xvpf fedit2-0.0.0.tar.gz
> cd fedit2-0.0.0

Then:

> ./configure
> make
> sudo make install

Finally: 

> fedit2

**Troubleshoot**:

> unrecognized command line option ‘-pthread-lQtGui’

Open the **configure** file, locate the line below and put a space between $PKG_CONFIG the variables, so it will be like this:

> QT4_LDADD="$($PKG_CONFIG --static --libs-only-other $QT4_REQUIRED_MODULES) $($PKG_CONFIG --static --libs-only-l $QT4_REQUIRED_MODULES)"

Source: http://askubuntu.com/a/892432/664657

> error while loading shared libraries: librcsc_agent.so.7

Run

> sudo ldconfig -v


Source: http://stackoverflow.com/questions/33506751/start-sh-dosent-work-in-agent2d-robocup


