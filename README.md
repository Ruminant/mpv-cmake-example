# MPV Cmake example 

An example of using [libmpv](https://github.com/mpv-player/mpv) on Windows (using visual studio) with a simple CMAKE setup.

The mpv binaries were grabbed from [here](https://mpv.io/installation/), using the Windows builds by shinchiro.  The version in use is from `mpv-dev-x86_64-20221120-git-f10b24e.7z`.

The libraries have been renamed for no obvious advantage...

## LIB file

The lib file was created using the visual studio command prompt:

`lib /def:libmpv-2.def /machine:x64 /out:libmpv-2.lib`

## DEF file

The original def file seemed to present problems for LIB generation, so a new one was created using Mingw64's `gendef` utility:

`gendef.exe libmpv-2.dll`

This generates a DEF file, and the following tool creates a GCC import library (`.a` file)

`dlltool.exe -d libmpv-2.def -D libmpv-2.dll -l libmpv-2.a`

