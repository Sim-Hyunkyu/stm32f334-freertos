Toolchain
=========
  * gcc-arm-embedded toolchain >= 4.9-2014-q4
    * https://launchpad.net/gcc-arm-embedded

  * Command line tools (use cygwin for windows)
    * make
	* git
    * python >= 2.7

  * Flash programming
    * STM32 ST-LINK utility (windows)
    * https://github.com/texane/stlink (linux)

  * Eclipse Luna

Eclipse settings
================
  * Download and configure Eclipse Luna:
    * Help -> Install new Software -> Add
      * Name: `http://pydev.org/updates`
      * Location: `http://pydev.org/updates`
    * Install the following plugins:
      * Programming Languages
        * C/C++ Development Tools
      * Mobile and Device Development
        * C/C++ GCC Cross Compiler Support
        * C/C++ GDB Hardware Debugging
     * PyDev
        * PyDev for Eclipse
      * Collaboration
        * Eclipse Git Team Provider

  * Window -> Preferences
    * C/C++
      * Build -> Console -> Limit console output: `5000`
      * Editor -> Scalability -> .. number of lines: `50000`
      * Editor -> Folding -> Enable folding of preprocessor branches
      * Code Style -> Formatter -> Import: `Docs/Codestyle.xml`
      * Code Analysis -> Uncheck all options
    * General -> Editors -> Text Editors -> Spelling -> Disable spell checking

  * File -> New -> Makefile Project with Existing Code
    * Toolchain for Indexer Settings: Cross GCC

  * Project -> Uncheck "Build Automatically" 
  
  * Project -> Properties -> C/C++ General
    * Preprocessor Include Paths, Macros, etc. -> Providers
      * CDT GCC Build Output Parser: `arm-none-eabi-gcc`
      * CDT Cross GCC Built-in Compiler Settings: `arm-none-eabi-gcc -E -P -v -dD "${INPUTS}"`

Flashing
========

Windows
-------
Copy the ST-LINK utility to the Tools/st-link directory.

    make boot_flash
    make flash

Linux
-----
Make sure to install the udev rules, so you can flash without root
privileges.

    make boot_flash
    make flash

Debugging
=========
GDB may complain that auto-loading has been declined. If this is
the case, just create a .gdbinit in your home directory:

    $ nano ~/.gdbinit
    set auto-load safe-path /

Afterwards, 

    $ arm-none-eabi-gdb obj_app/drquad32.elf

should do the trick.
