# MacOS Build Notes

More or less, there is no support for building on MacOS. This is my attempt to get it to work. What good is having the source if you can't build it?

- install a bunch of stuff with `brew`
 - openssl fdk-aac fltk portaudio lame
- set some env vars
 - `export LDFLAGS="-L/usr/local/opt/openssl@1.1/lib"`
- configure with some other junk
 - found some of this here:  https://github.com/Bombe/butt 
 - `CPPFLAGS="-ObjC++ -I../xcode/include -I/usr/local/opt/openssl@1.1/include" ./configure `
- manually tweak `src/Makefile`
 - remove all references to `CurrentTrackOSX`
 - I should do this by tweaking `Makefile.am` but then you need `automake` and running that breaks everything
- next step is to make it, but it dies
 - `make`
 - dies trying to link with unknown symbols `askForMicPermission()`, `getCurrentTrackFunctionFromId(int)`, a bunch of `Fl_My_Native_File_Chooser` stuff, and a pile of `_libintl_*` stuff 
 - since it's at the link stage, it's probably just getting more `-I` and/or `-L` flags correct
