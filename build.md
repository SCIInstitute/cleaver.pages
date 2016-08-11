---
title: Build Instructions
category: info
tags: build
layout: default
---

## Table of Contents

* [Installing ShapeworksStudio from source](#installing-shapeworks-studio-from-source)
    * [Dependencies](#dependencies)
        * [Qt](#qt)
        * [CMake](#cmake)
        * [ITK](#itk)
        * [VTK](#vtk)
    * [Compiling From Source](#compiling-from-source)
        * [Compiling ITK](#compiling-itk)
        * [Compiling VTK](#compiling-vtk)
        * [Compiling ShapeworksStudio](#compiling-shapeworks-studio)
            * [Unix and OSX](#unix-and-osx)
            * [Windows](#windows)
            * [All Platforms](#all-platforms)
* [ShapeworksStudio Support](#shapeworks-studio-support)

<!-- Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc) -->

# Installing Shapeworks Studio from source

## Dependencies

### Qt

[Qt binaries](qt.io) and packages are available on the Qt website or can be built 
from source code. Gcc/Clang/MSVC with C++11 support is required.

### CMake

[CMake](https://cmake.org/) versions 2.8 - 3.4 are supported.

### ITK

[ITK](http://www.itk.org/) Insight Toolkit (ITK 4.7+ recommended) 

### VTK

[VTK](http://www.vtk.org/) Visualization ToolKit (VTK 7. recommended) 

## Compiling From Source

Once you have obtained a compatible compiler and installed Qt on your system, you need to
download and install CMake (http://www.cmake.org) to actually build the software.
CMake is a platform independent configuring system that is used for generating Makefiles,Visual Studio project files, or Xcode project files.

### Compiling ITK

Configure with:
<br/><br/>
``` CMAKE_CXX_FLAGS+="-std=c++11" ``` <br/>
``` BUILD_SHARED_LIBS=FALSE ``` <br/>
``` BUILD_EXAMPLES=FALSE ``` <br/>
``` BUILD_TESTING=FALSE ``` <br/>
``` ITKV3_COMPATIBILTY=TRUE ``` <br/>
<br/>
Then build ITK.
<br/><br/>
``` make -j12 all ``` <br/>
<br/>
You may need to use the CMake GUI in Windows. It is best to configure with "NMake Makefiles". Once you have configured and generated, you can build in a command prompt.
<br/><br/>
``` cd C:\ITK_DIR ``` <br/>
``` mkdir build ``` <br/>
``` cd build ``` <br/>
``` nmake all ``` <br/>

### Compiling VTK

Configure with:
<br/> <br/>
``` VTK_Group_Qt=ON ``` <br/>
``` VTK_QT_VERSION=5 ``` <br/>
``` Qt5_DIR="/PATH/TO/YOUR/Qt5 ``` <br/>
``` BUILD_SHARED_LIBS=FALSE ``` <br/>
``` BUILD_EXAMPLES=FALSE ``` <br/>
``` BUILD_TESTING=FALSE ``` <br/>
<br/>
Then build VTK.
<br/><br/>
``` make -j12 all ```
<br/><br/>
You may need to use the CMake GUI in Windows. It is best to configure with "NMake Makefiles". Once you have configured and generated, you can build in a command prompt.
<br/><br/>
``` cd C:\VTK_DIR ``` <br/>
``` mkdir build ``` <br/>
``` cd build ``` <br/>
``` nmake all ``` <br/>

### Compiling Shapeworks Studio
Once CMake, Qt, ITK, and VTK have been installed and/or built, run CMake from your build directory and give a path to the ShapeworksStudio directory containing the master CMakeLists.txt file.

#### Unix and OSX
``` mkdir ShapeWorksStudio/build ``` <br/>
``` cd ShapeWorksStudio/build ``` <br/>
``` cmake -DVTK_DIR=Path/To/Your/VTK/build -DITK_DIR=Path/To/Your/ITK/build -DQT_DIR=Path/To/Your/Qt5/build -DCMAKE_BUILD_TYPE=Release ../src ``` <br/>
``` make ``` <br/>
<br/>
Depending on how you obtained Qt, you may need to specify other Qt directories:
<br/><br/>
``` -DQT5WidgetsDIR="Path/To/Qt/5.6/gcc/lib/cmake/Qt5Widgets" ``` <br/>
``` -DQT5OpenGLDIR="Path/To/Qt/5.6/gcc/lib/cmake/Qt5OpenGL" ``` <br/>

#### Windows
Open a Visual Studio 64 bit Native Tools Command Prompt.
Follow these commands:
<br/><br/>
``` mkdir C:\Path\To\ShapeWorksStudio\build ``` <br/>
``` cd C:\Path\To\ShapeWorksStudio\build ``` <br/>
``` cmake -G "NMake Makefiles" -DVTK_DIR="C:/Path/To/Your/VTK/build" -DITK_DIR="C:/Path/To/Your/ITK/build" -DQT_DIR="C:/Path/To/Your/Qt5/build" -DCMAKE_BUILD_TYPE=Release ../src ``` <br/>
``` nmake ``` <br/>
<br/>
**NOTE** Be sure to copy the Qt5 DLL files to the Executable directory for the program to run.
<br/><br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Widgets.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Core.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5OpenGL.dll ``` <br/>
``` C:\Qt5_DIR\msvc2015\5.6\bin\Qt5Gui.dll ``` <br/>

#### All Platforms
Your paths may differ slightly based on your Qt5, ITK, and VTK versions and where they are installed/built.

The console version ``ccmake``, or GUI version can also be used.
You may be prompted to specify your location of the Qt installation.
If you installed Qt in the default location, it should find Qt automatically.
After configuration is done, generate the make files or project files for your favorite
development environment and build.

The ShapeworksStudio application will be built in bin/Application.

# Shapeworks Studio Support

For questions and issues regarding building the software from source,
    please email our support list: [shapeworks@sci.utah.edu](mailto:shapeworks-users@sci.utah.edu)
