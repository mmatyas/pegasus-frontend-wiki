## OUTDATED

This page has been moved to http://pegasus-frontend.org/docs/dev/build. The wiki page is kept only for historical reasons.

---

---

Pegasus is a C++ program that uses the Qt framework. To build it run on your OS or device, you'll need a C++11 supporting compiler (g++ 4.6 or better), Qt 5.7 or later (version is important!) for your platform, and at least the following additional Qt components:

- QML module
- Qt Quick 2 module
- Multimedia module (might be called as MultimediaQuick)
- Svg module
- Gamepad module

Depending on your platform, these libs may or may not be available for your OS, or they may be outdated; see below for the platform notes. Qt also provides a graphical IDE called Qt Creator, which you can use if you wish, but it's not a requirement.

### Table of contents:
- [Platform notes](#platform-notes)
- [Configuration options](#general-configuration-options)
- [Using Qt Creator](#general-using-qt-creator)

# Platform notes

## Linux/X11

On many Linux distros, such as Debian (Ubuntu, Mint, ...) the Qt libraries are outdated, and the versions available in the official repositories may be several years old (as a trade-off between stability and access to the latest software).

On **Ubuntu**, you may use the following PPAs to get the latest Qt releases:

```sh
# for 14.04, use this:
sudo add-apt-repository ppa:beineri/opt-qt591-trusty
# for 16.04, use this:
sudo add-apt-repository ppa:beineri/opt-qt591-xenial

sudo apt-get update
sudo apt-get install  \
    qt59declarative  \
    qt59graphicaleffects  \
    qt59gamepad  \
    qt59imageformats  \
    qt59multimedia  \
    qt59svg  \
    qt59tools

source /opt/qt59/bin/qt59-env.sh
```

then build as described below. You may want to add the `source ...` line to eg. your `.bashrc`, in order to be called automatically on every new terminal.

If you're using **Arch**, you can get Qt from AUR; here's the relevant [wiki page](https://wiki.archlinux.org/index.php/qt#Installation).

On other distros, you can use the official releases, available from [the website of Qt](https://info.qt.io/download-qt-for-application-development) (select open source). It comes in the form of an installer, where you'll have to select Desktop GCC and Gamepad from under Qt 5.x, and optionally Qt Creator from under Tools.

### Using Qt Creator

See the [Qt Creator how to](#general-using-qt-creator).

### Using the command line

1. Create a build directory somewhere, and `cd` into it
2. Call `qmake`, the configuration tool of Qt: `/path/to/qmake  path/to/project  [options]`.
    - If you have multiple Qt versions installed, make sure you call the right `qmake`. If you've installed using the official release from the Qt site, you can find it in `[qt-installdir]/Qt5/[version]/gcc_64/bin` (you can add it to your `$PATH` if you want, but it's not necessary).
    - You can also change some configuration options, which you can find [here](#general-configuration-options).
3. Call `make`
4. [optional] Call `make install`

## Windows

On Windows, you can use the official Qt installer, which you can get from [here](https://info.qt.io/download-qt-for-application-development) (select open source). Select Qt 5.x during the installation, and one of the compilers you'll use for the building/development: either Microsoft Visual Studio (MSVC) or the open source MinGW tools. You'll also need Gamepad (under Qt 5.x), and Qt Creator (from Tools).

Alternatively, if you're using MSYS2, you can find a setup guide [here](https://wiki.qt.io/MSYS2).

After installation, follow the [Qt Creator guide](#general-using-qt-creator).

## macOS

You can use the official Qt installer from [here](https://info.qt.io/download-qt-for-application-development) (select open source), and it is also available from Homebrew (`qt5`). Generally, you can follow the [Linux/X11](#linuxx11) guide. Xcode is also supported by Qt.

## Linux/Embedded

You'll likely need to build Qt manually for your platform (but check your repositories first, just in case). You can find a guide for it [[here|Qt-cross-compilation]].

After that, you can follow the [Linux/X11](#linuxx11) guide to cross compile Pegasus on your desktop PC, then transfer the runtime binary to your device.

# General

## General: configuration options

You can set optional parameters to `qmake` (the Qt configuration tool) by appending `KEY=VALUE` pairs to its command line call. If you're using Qt Creator, you can find these settings on the Projects -> Build settings tab, where you can modify the Additional arguments option (see [here](https://doc.qt.io/qtcreator/creator-build-settings.html#build-steps)).

You can use the following parameters:

Option | Description
---|---
`INSTALLDIR` | The general installation directory used by `make install`. Defaults to `/opt/pegasus-frontend` on Linux and `C:\pegasus-frontend` on Windows. You can fine tune the installation directory of some components by other options.
`INSTALL_BINDIR` | The installation directory of the runtime binary ("exe"). Defaults to `INSTALLDIR`.
`INSTALL_DATADIR` | The installation directory of the data files, eg. default themes. Defaults to `INSTALLDIR`.
`INSTALL_ICONDIR` | [Linux only] The installation directory of the icon file. Defaults to `INSTALLDIR` (to make it portable), `/usr/share/pixmaps` is recommended if you want to install Pegasus system-wide.
`INSTALL_DESKTOPDIR` | [Linux only] The installation directory of the desktop entry. Defaults to `INSTALLDIR` (to make it portable), `/usr/share/applications` is recommended if you want to install Pegasus system-wide.

## General: using Qt Creator

1. Open Qt Creator
2. Open the project file (`pegasus.pro`) in Qt Creator
3. Qt Creator will ask you which Qt setup ("kit") you want to use (in case you've installed multiple versions), and where you want to place the generated files (see Details). If everything's OK, click Configure Project.
4. In the bottom left corner, on the sidebar of Qt Creator, you can find 4 buttons:

    - with the button that looks like a desktop monitor, you can change the build type (optimized Release build or development-friendly but slower Debug build)
    - the green arrow will build and run the program
    - the green arrow with a bug will also open several debug toolbars
    - the hammer will build the project but won't run it

5. Change the build type to Release (see above), and press the green arrow to build and run the project.
