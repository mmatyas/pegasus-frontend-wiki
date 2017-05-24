**NOTE**: Cross compiling Qt is not trivial, you'll need some experience setting it all up. If you'd just like to make Pegasus run on a new device, consider opening a new issue!

This documentation lists the configurations I personally use when building Qt.

If the latest Qt is not available for your platform, or you're not pleased with it (eg. hardware acceleration is disabled), you'll need to build it manually. You can get the latest officially released source code from the Qt website, from [here](https://info.qt.io/download-qt-for-application-development) (select open source, click 'All downloads' on the bottom, then search for 'Source packages'). The general steps and requirements are described in the [Qt documentation](https://doc.qt.io/qt-5/build-sources.html).

Building Qt takes significant time, about 30-60 minutes on a good desktop PC, depending on the selected components. It requires at least 2 GB of RAM and 6.5 GB free space. **Do not** try to build it on your 5$ board computer.

Instead, you can *cross compile* Qt. Cross compilation means the program or library you build will run on a different architecture or platform than your own PC. For example, if you're on Linux, you can build programs that will run on Windows, or on a phone or embedded device. For this, you'll need a *toolchain*, a compiler that generates code for a certain platform, and a *sysroot*, a collection of libraries from the target device. Getting a toolchain and sysroot is different for every platform; you can find cross compilers for the popular targets, eg. ARMv7-Linux, while for others you might need to build a whole custom GCC. For the Raspberry Pi cross compilation, this guide was very helpful: https://wiki.qt.io/RaspberryPi2EGLFS.

# Configurations

These configurations are mainly based on the Debian automatic builds, and the guide mentioned above.

## Raspbian sysroot

The sysroot used for compilation is based on Raspbian, with the following additional packages installed:

```sh
apt-get build-dep -y qt4-x11 libqt5gui5
apt-get install -y libudev-dev libinput-dev libts-dev libxcb-xinerama0-dev libxcb-xinerama0
apt-get install -y libopenal-dev libsqlite3-dev libfontconfig-dev
apt-get install -y libglib2.0-dev gstreamer1.0-omx libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
apt-get install -y libsmbclient-dev libssh-dev libsdl2-dev
```

## Raspberry Pi 1 / Zero

toolchain: `https://github.com/raspberrypi/tools`, cloned to `/opt/raspberrypi-tools`  
sysroot: see [Raspbian sysroot](#raspbian-sysroot)

```
../configure \
	-opensource \
	-confirm-license \
	-release \
	-strip \
	-no-rpath \
	-make libs \
	-skip qtwebengine \
	-skip wayland \
	-device linux-rasp-pi-g++ \
	-opengl es2 \
	-device-option CROSS_COMPILE=/opt/raspberrypi-tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- \
	-sysroot /opt/rpi-sysroot \
	-prefix /opt/qt58-rpi1 \
	-extprefix /opt/qt58-rpi1 \
	-hostprefix /opt/qt58-rpi1_hosttools \
	-no-use-gold-linker \
	-openssl \
	-fontconfig \
	-gstreamer 1.0 \
	-no-xcb \
	-no-dbus \
	-no-glib \
	-no-icu \
	-system-zlib \
	-system-libpng \
	-system-libjpeg \
	-system-sqlite \
	-verbose
```

## Raspberry Pi 2 / 3

NOTE: The only difference is the `-device` parameter.

toolchain: `https://github.com/raspberrypi/tools`, cloned to `/opt/raspberrypi-tools`  
sysroot: see [Raspbian sysroot](#raspbian-sysroot)

```sh
../configure \
	-opensource \
	-confirm-license \
	-release \
	-strip \
	-no-rpath \
	-make libs \
	-skip qtwebengine \
	-skip wayland \
	-device linux-rasp-pi2-g++ \
	-opengl es2 \
	-device-option CROSS_COMPILE=/opt/raspberrypi-tools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf- \
	-sysroot /opt/rpi-sysroot \
	-prefix /opt/qt58-rpi2 \
	-extprefix /opt/qt58-rpi2 \
	-hostprefix /opt/qt58-rpi2_hosttools \
	-no-use-gold-linker \
	-openssl \
	-fontconfig \
	-gstreamer 1.0 \
	-no-xcb \
	-no-dbus \
	-no-glib \
	-no-icu \
	-system-zlib \
	-system-libpng \
	-system-libjpeg \
	-system-sqlite \
	-verbose
```
