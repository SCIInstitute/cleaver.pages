---
title: Build Instructions
category: info
tags: build
layout: default
project: Cleaver2
supportEmail: cleaver@sci.utah.edu
---

## Table of Contents

* [Installing {{ page.project }} from source](#installing-cleaver2-from-source)
  * [Dependencies](#dependencies)
    * [Qt](#qt)
    * [CMake](#cmake)
    * [ITK](#itk)
  * [Compiling From Source](#compiling-from-source)
    * [Compiling ITK](#compiling-itk)
    * [Compiling {{ page.project }}](#compiling-cleaver2)
      * [Unix and OSX](#unix-and-osx)
      * [Windows](#windows)
  * [All Platforms](#all-platforms)
* [Testing](#testing)
  * [Windows](#windows)
* [{{ page.project }} Support](#cleaver2-support)

# Installing {{ page.project }} from source

## Dependencies

### Qt

[Qt binaries](https://www.qt.io/) and packages are available on the Qt website or can be built 
from source code. Gcc/Clang/MSVC with C++11 support is required.

### CMake

[CMake](https://cmake.org/) versions 3.4 - 3.18 are supported.

### ITK

[ITK](http://www.itk.org/) Insight Toolkit (ITK 4.13+ recommended) 


## Compiling From Source

Once you have obtained a compatible compiler and installed Qt on your system, you need to
download and install [CMake](http://www.cmake.org/) to actually build the software.
CMake is a platform independent configuring system that is used for generating Makefiles, Visual Studio project files, or Xcode project files.

### Compiling ITK

Using CMake either on the command line or in the CMake gui, set the source directory as ITK's source code. Create a build folder and set as the build directory. Then configure with the following settings:
<br/><br/>
``` CMAKE_CXX_FLAGS+="-std=c++11" ``` <br/>
``` BUILD_SHARED_LIBS=FALSE ``` <br/>
``` BUILD_EXAMPLES=FALSE ``` <br/>
``` BUILD_TESTING=FALSE ``` <br/>
``` ITKV4_COMPATIBILTY=FALSE ``` <br/>
<br/>
After configuration passes, then generate the makefiles. Build ITK from the build folder using the following command:
<br/><br/>

``` make -j12 all ``` <br/>
<br/>

You may need to use the CMake GUI in Windows. It is best to configure with "NMake Makefiles". Once you have configured and generated, you can build in a command prompt.
<br/><br/>
``` cd C:\ITK_DIR ``` <br/>
``` mkdir build ``` <br/>
``` cd build ``` <br/>
``` nmake all ``` <br/>
<br/>

### Compiling {{ page.project }}
Once CMake, Qt, ITK have been installed and/or built, run CMake from your build directory or run the CMake gui. 

#### Unix and OSX

Set the source directory as ``` Cleaver2/src/ ```. Create a build folder (```Cleaver2/build/```) and set as the build directory. Include the paths to your built ITK build directory, and to ```Qt5Widgets``` and ```Qt5OpenGL```. These will be located in your installed Qt library:
<br/><br/>

```Path/To/Qt/Qt5.12.9/5.12.9/clang_64/lib/cmake/Qt5Widgets``` <br/>
```Path/To/Qt/Qt5.12.9/5.12.9/clang_64/lib/cmake/Qt5OpenGL``` <br/>

Cleaver2 will not build a bundle by default. If you would like to build the bundle or the Cleaver2 command line interface, then configure with the respective settings:
<br/><br/>

``` BUILD_GUI=TRUE ``` <br/>
``` BUILD_CLI=TRUE ``` <br/>

Then configure and generate the makefiles. Build Cleaver2 from the build directory:
<br/><br/>

``` make -j12 all ``` <br/>
<br/>

The {{ page.project }} application will be built in build/bin.

#### Windows
Open a Visual Studio 64 bit Native Tools Command Prompt.
Follow these commands:
<br/><br/>
``` mkdir C:\Path\To\{{ page.project }}\build ``` <br/>
``` cd C:\Path\To\{{ page.project }}\build ``` <br/>
``` cmake -G "NMake Makefiles" -DITK_DIR="C:/Path/To/Your/ITK/build" -DQT_DIR="C:/Path/To/Your/Qt5/build" -DCMAKE_BUILD_TYPE=Release ../src ``` <br/>
``` nmake ``` <br/>
<br/>
**NOTE** Be sure to copy the Qt5 DLL files to the Executable directory for the program to run.
<br/><br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Widgets.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Core.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5OpenGL.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Gui.dll ``` <br/>

#### All Platforms
Your paths may differ slightly based on your Qt5 and ITK versions and where they are installed/built.

The console version ``ccmake``, or GUI version can also be used.
You may be prompted to specify your location of the Qt installation.
If you installed Qt in the default location, it should find Qt automatically.
After configuration is done, generate the make files or project files for your favorite
development environment and build.

The {{ page.project }} application will be built in build/bin.

# Testing

The repo comes with a set of regression tests to see if recent
changes break expected results. To build the tests, you will
need to set <code>BUILD_TESTING</code> to "ON" in either
<code>ccmake</code> or when calling CMake:

```c++
cmake -DBUILD_TESTING=ON ../src
```

## Windows
The gtest library included in the repo needs to be
built with forced shared libraries on Windows, so use the following:

```c++
cmake -DBUILD_TESTING=ON -Dgtest_forced_shared_crt=ON ../src
```<br/>

Be sure to include all other necessary CMake definitions as annotated above.

# {{ page.project }} Support

For questions and issues regarding building the software from source,
    please email our support list: [{{ page.supportEmail }}](mailto:{{ page.supportEmail }})
