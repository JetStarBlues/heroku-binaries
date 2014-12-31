
#####Building a standalone ffmpeg

The following steps apply to *Ubuntu*

So you basically want to do as is shown on the [official docs][1]

The big **catch** to watch out for is the second step where you install a bunch of files

```
sudo apt-get -y install autoconf automake build-essential \
  libass-dev libfreetype6-dev libgpac-dev \
  libtheora-dev libtool libvorbis-dev \
  pkg-config texi2html zlib1g-dev

```
Using `sudo apt-get` means the files are installed onto your computer and thus useless for our purposes.

Specifically, anything starting with `lib` shouldn't be installed this way and should instead be compiled 
from source in the same directory as your ffmpeg_build

<br><br>

Here's some starter code ...

```
... Setup ...

sudo apt-get update
sudo apt-get -y install autoconf automake build-essential \
  pkg-config texi2html zlib1g-dev
mkdir ~/ffmpeg_sources

... Yasm ...

cd ~/ffmpeg_sources
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar xzvf yasm-1.3.0.tar.gz
cd yasm-1.3.0
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install
make distclean

... Libogg (dependency for libvorbis & libtheora) ...

cd ~/ffmpeg_sources
wget http://downloads.xiph.org/releases/ogg/libogg-1.3.2.tar.xz
tar xzvf libogg-1.3.2.tar.gz
cd libogg-1.3.2
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install
make distclean

... Libvorbis ...

cd ~/ffmpeg_sources
wget http://downloads.xiph.org/releases/vorbis/libvorbis-1.3.4.tar.gz
tar xzvf libvorbis-1.3.4.tar.gz
cd libvorbis-1.3.4
./configure --prefix="$HOME/ffmpeg_build" --disable-shared
make
make install
make distclean

... Libtheora ...

cd ~/ffmpeg_sources
wget http://downloads.xiph.org/releases/theora/libtheora-1.1.1.tar.gz
tar xzvf libtheora-1.1.1.tar.gz
cd libtheora-1.1.1
./configure --prefix="$HOME/ffmpeg_build" --disable-shared \
   --with-ogg-includes=/ffmpeg_build/include --with-ogg-libraries=/ffmpeg_build/lib
make
make install
make distclean

```

The rest can be found on the [official docs][1]


I skipped installing `libass`, `libfreetype6`, and `libgpac` for this build.
But if you need them for your build, you would probably have to compile them from source as above.


[1]: https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu