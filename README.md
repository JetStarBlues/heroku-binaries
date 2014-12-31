
Heroku binaries
===

In the style of https://github.com/flect/heroku-binaries

Needed additional libraries not included in FLEC's ffmpeg version

<br><br>
This was built as follows...
```
  built on Dec 30 2014 20:20:26 with gcc 4.8 (Ubuntu 4.8.2-19ubuntu1)
  configuration: 
  --prefix=/home/name/ffmpeg 
  --extra-cflags=-I/home/name/ffmpeg/include 
  --extra-ldflags=-L/home/name/ffmpeg/lib 
  --bindir=/home/name/ffmpeg/bin 
  --enable-gpl 
  --enable-libfdk-aac 
  --enable-libmp3lame 
  --enable-libopus 
  --enable-libtheora 
  --enable-libvorbis 
  --enable-libvpx 
  --enable-libx264 
  --enable-nonfree
```

<br><br>
For one way to build your own, checkout [this][1]
[1]:somelink.cdfsfd
