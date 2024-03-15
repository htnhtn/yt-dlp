Fix this error
```
ERROR: Initialization fragment found after media fragments, unable to download
```
by downloading to separate files:

![](https://github.com/htnhtn/yt-dlp/assets/23214361/1ee15233-44a9-44aa-8b7d-5318acd5da8b)

Only the first part gets things like metadata, thumbnails embedded.
## Other work
In my case, I modified the processor of `--embed-metadata` to change downloaded videos to 360p.
If you want to do so. replace `yt_dlp/postprocessor/ffmpeg.py` with `ffmpeg.py` in the root directory.
Have a look into `_options()` function at line 678 in `ffmpeg.py` to make your own change. 

Note that the conversion blocks next download, and the conversion is even longer than the download,
so I recommend that use `-O "%(webpage_url)s"` to get urls, split them into files and run many `yt-dlp` with `-a`.
And don't forget `-N`. An example is:
```
python -m yt_dlp --proxy socks5://127.0.0.1:10808/ --embed-metadata --embed-thumbnail -o "%(title)s %(timestamp>%Y/%m/%d %H:%M:%S)s.%(ext)s" -N 10 -a a.txt
```
