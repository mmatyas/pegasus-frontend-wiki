On many Linux distros, such as Debian (Ubuntu, Mint, ...) the Qt libraries are outdated, and the versions available in the repositories may be several years old (as a trade-off between stability and access to the latest software). Unless you're using a "bleeding edge" distribution (eg. Arch), it is recommended to use the official release available from the website of Qt. You can get the required tools from [here](https://info.qt.io/download-qt-for-application-development) (select open source). You will need to install Desktop GCC and Gamepad from Qt 5.8, and Qt Creator from under Tools.

Here's how to build on most desktop Linux distros:

## Using the graphical tools

1. Open Qt Creator
2. Open the project file (`pegasus.pro`) in Qt Creator
3. Qt Creator will ask you which Qt setup ("kit") you want to use (in case you've installed multiple versions), and where you want to place the generated files (see Details). If everything's OK, click Configure Project.
4. In the bottom left corner, on the sidebar of Qt Creator, you can find 4 buttons:

    - with the button that looks like a desktop monitor, you can change the build type (optimized Release build or development-friendly but slower Debug build)
    - the green arrow will build and run the program
    - the green arrow with a bug will also open several debug toolbars
    - the hammer will build the project but won't run it

5. Change the build type to Release (see above), and press the green arrow to build and run the project.

## Using the command line

1. Create a build directory somewhere, and `cd` into it
2. Call `qmake`, the configuration tool of Qt: `/path/to/qmake path/to/project/directory`. If you have multiple Qt versions installed, make sure you call the right `qmake`. If you've installed using the official release from the Qt site, you can find it in `[qt-installdir]/Qt5/[version]/gcc_64/bin`. You can also set some configuration parameters, see the general build guide for more information.
3. Call `make`
4. [optional] Call `make install`
