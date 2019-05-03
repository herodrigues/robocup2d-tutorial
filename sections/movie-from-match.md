# Recording Matches

To record a movie from the match image frames, first you need to install menconder:

```bash
sudo apt-get install mencoder
```

Then, run the following command:

```bash
mencoder "mf://*.png" -mf fps=10 -o test.avi -ovc lavc -lavcopts vcodec=msmpeg4v2:vbitrate=8000
```
