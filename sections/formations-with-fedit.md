**Installing fedit**

Download fedit in the Robocup's official repository [here]http://en.sourceforge.jp/projects/rctools/downloads/48791/fedit2-0.0.0.tar.gz/).

Open a terminal (CTRL+ALT+T), extract the files and execute:
```bash
$ tar -xvpf fedit2-0.0.0.tar.gz
$ cd fedit2-0.0.0
```

Then:
```bash
$ ./configure
$ make
$ sudo make install
```

Finally: 
```bash
$ fedit2
```

**Troubleshoot**:

If you got this error (and you probably will):
```bash
unrecognized command line option ‘-pthread-lQtGui’
```

Open the **configure** file, locate the line below and put a space between $PKG_CONFIG the variables, so it will be like this:
```
QT4_LDADD="$($PKG_CONFIG --static --libs-only-other $QT4_REQUIRED_MODULES) $($PKG_CONFIG --static --libs-only-l $QT4_REQUIRED_MODULES)"
```

Source: http://askubuntu.com/a/892432/664657
