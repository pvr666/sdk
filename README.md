MEGA SDK - Client Access Engine
===============================

Building
--------

    sh autogen.sh
    ./configure
    make
    sudo make install


Usage
-----

A simple project in `doc/example` shows how to use the MEGA SDK
in your applications.  In order to compile and link your
application with the MEGA SDK library, you can use the `pkg-config` script:

    g++ $(pkg-config --cflags libmega) -o lsmega.o -c lsmega.cpp
    g++ $(pkg-config --libs libmega) -o app lsmega.o

An (almost) feature complete console-based client application can be found
in `examples`. Similar to an FTP client, it allows you to invoke and test
the client library's full functionality.


Platform Dependencies
---------------------

The following notes are intended for building and running build
artifacts.


### POSIX (Linux/Darwin/BSD/...)

Install the following development packages, if available, or download
and compile their respective sources (package names are for
Debian and RedHat derivatives respectively):

* Crypto++ (`libcrypto++-dev`, `cryptopp-devel`)
* cURL (`libcurl-dev`, `curl-devel`)

CAUTION: Verify that the installed `libcurl` uses c-ares for
asynchronous name resolution.  If that is not the case, compile it
from the original sources with `--enable-ares`.  Do *NOT* use
`--enable-threaded-resolver`, which will cause the engine to get
stuck whenever a non-cached hostname is accessed. Also, bear in mind
that not enabling asynchronous DNS resolving at all would result in
the engine losing its non-blocking behaviour.

Filesystem event monitoring: Under Linux, inotify is used; periodic full
directory scans otherwise.

To build the the reference megacli example, you may also need to install:

* GNU Readline (`libreadline-dev`, `readline-devel`)
* FreeImage (`libfreeimage-dev`, `freeimage-devel`)
* SQLite (`libsqlite3-dev`, `sqlite-devel`)

Please ensure that your terminal supports UTF-8 if you want to see and
manipulate non-ASCII filenames.


### Windows

To build the client access engine under Windows, you'll need to following:

* A Windows-native C++ development environment (e.g. MinGW or Visual Studio)
* Crypto++

(You won't need cURL, as megaclient's Win32 version relies on WinHTTP
for network access. Windows-native filesystem event monitoring is
implemented.)

To build the reference megacli.exe example, you will also need to procure
development packages (at least headers and .lib/.a libraries):

* FreeImage
* GNU Readline/Termcap
* SQLite

CAUTION: The megaclient example is currently not handling Unicode input/output
correctly if run in cmd.exe.
