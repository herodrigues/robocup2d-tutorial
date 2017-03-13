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

You can fix it by doing the following commands:
```
$ make clean
$ ./configure
$ sed -i 's/-pthread-lQtGui/-pthread -lQtGui/' config.status*
$ sed -i 's/-pthread-lQtGui/-pthread -lQtGui/' Makefile*
```
Now we can go back and repeat the command sudo make install.

Source: http://askubuntu.com/questions/810726/g-5-real-error-unrecognized-command-line-option-pthread-lqtgui
