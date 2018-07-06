# Record Matches

Install menconder:

> sudo apt-get install mencoder
> mencoder "mf://*.png" -mf fps=10 -o test.avi -ovc lavc -lavcopts vcodec=msmpeg4v2:vbitrate=8000
