This repo is for Cyclone binaries to be used on TIO.

I used [tjim/cyclone vagrant VM](http://trevorjim.com/unfrozen-cyclone/).
tjim/cyclone has sources and installed binaries of the latest development version of Cyclone.
This means that it is fresher version than 1.0 and it can be compiled with gcc 4.2 installed on tjim/cyclone.

We need Cyclone binaries in `/opt/cyclone`, so cyclone need to be reconfigured and remade:
```bash
cd ~/cyclone
./configure  -bindir /opt/cyclone/local/bin  -libdir /opt/cyclone/local/lib  -includedir /opt/cyclone/local/include
make
sudo make install
```
After that we have Cyclone binaries in `/opt/cyclone/local`. I packed those files together with the binaries of gcc toolchain that it requires.
`cyclone/bin` and `cyclone/lib` contain files of gcc toolchain, copied from tjim-cyclone `/usr/bin`, `/usr/lib` and `/lib`.

To make sure that correct files are linked on Fedora 64 bit, I used command `cyclone -v tst.cyc -Wl,--verbose 2> verbose-gcc > verbose-ld`.
To make sure that correct files are #included I used command `cyclone -M tst.cyc`.
