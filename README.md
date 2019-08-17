This repo is for [Cyclone](https://en.wikipedia.org/wiki/Cyclone_(programming_language)) binaries to be used on [TIO](https://tio.run/#).

I used [tjim/cyclone vagrant VM](http://trevorjim.com/unfrozen-cyclone/) to create the binaries.
tjim/cyclone has sources and binaries of the latest development version of Cyclone (from SVN).
This means that it is fresher version than 1.0 and it can be compiled with gcc 4.2 installed on tjim/cyclone.

On TIO we need Cyclone binaries in `/opt/cyclone`, but in tjim/cyclone they are in /usr/local/bin and /usr/local/lib, so Cyclone need to be reconfigured and remade
so it knows where to get libs:
```bash
cd ~/cyclone
./configure  -bindir /opt/cyclone/local/bin  -libdir /opt/cyclone/local/lib  -includedir /opt/cyclone/local/include
make
sudo make install
```
After that we have Cyclone binaries in `/opt/cyclone/local`. I packed those files together with the binaries of gcc toolchain that it requires.
Top-level `bin` and `lib` dirs in `cyclone.tar.xz` contain files of gcc toolchain, copied from tjim-cyclone `/usr/bin`, `/usr/lib` and `/lib`.

To make sure that correct files are linked on Fedora 64 bit, I used command `cyclone -v tst.cyc -Wl,--verbose 2> verbose-gcc > verbose-ld`.
To make sure that correct files are #included I used command `cyclone -M tst.cyc`.
