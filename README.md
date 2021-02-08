# SDL2 for iOS

This is a clone of [SDL2] with iOS patches.

Currently based on SDL2-2.0.14


## Doesn't SDL2 support iOS already?

Yes, but it does not produce `sdl2-config` and `pkg-config` file with which to
compile SDL applications via `./configure && make && make install`.


## Building

You can run `build-scripts/iosbuild.sh` that comes with the vanilla SDL2
install (which is broken without the iOS patches in this repository), but the
paths produced by `sdl2-config` and `pkg-config` are incorrect.  Change
`arm64-ios` to `universal` in `sdl2-config` and `sdl2.pc` to fix them
in `ios-build`.

For a more straight forward installation, install [ios-helper] first, then run:

```sh
$ ios -p /usr/local/ios configure --disable-video-metal --disable-render-metal --disable-video-vulkan && make && sudo make install
$ isim -p /usr/local/isim configure --disable-video-metal --disable-render-metal --disable-video-vulkan && make && sudo make install
```

The first command builds and installs the scripts and libraries for building
iOS binaries to `/usr/local/ios`.  The second installs the same for building
binaries that run under the iOS Simulator to `/usr/local/isim`.  Disabling
metal and vulcan is optional; it allows the library to be backward compatible
with iOS versions that do not support [Metal].

As of this writing ios-helper can target one architecture at a time.  It
targets `arm64` for iOS, and the native architecture of the Mac under which
SDL2 is being compiled for the iOS Simulator.  See [ios-helper] for more
details.


## License

[zlib]


[SDL2]: <https://www.libsdl.org/>
[ios-helper]: <https://github.com/markuskimius/ios-helper>
[Metal]: <https://en.wikipedia.org/wiki/Metal_(API)>
[zlib]: <http://www.zlib.net/zlib_license.html>
