# Autotools tutorial

Autotools is a suite of programming tools designed to assist in making source code packages portable to many Unix-like systems.
https://developer.gnome.org/anjuta-build-tutorial/stable/create-autotools.html.en

Manually editing the agent2D Makefile is a hard task; thus, Autotools will be used a lot through your work.

Install Autotools:

> sudo apt-get install autotools-dev

Go to the src directory of your team and run:

> autoreconf

The command above is only necessary because the original Makefile was created by an older Autotools version.

In the folder src of your team there is a file called Makefile.am. This file will contain your classes names. Go back to your team main folder and run:

> automake
> ./configure

The first command creates the file Makefile.in from the Makefile.am. 
The second command generates a Makefile from the filme Makefile.in.

You just need to add your classes in the Makefile.am:

## Process this file with automake to produce Makefile.in

PLAYERSOURCES = \
        your_new_class_here.cpp \
	body_advance_ball_test.cpp \
	body_clear_ball2008.cpp \
        # ....
PLAYERHEADERS = \
        your_new_class_here.h \
	body_advance_ball_test.h \
	body_clear_ball2008.h \
        # ...

Now, go to the src directory and run:

> make

