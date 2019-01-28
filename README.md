# Horde3D

Horde3D is a 3D rendering engine written in C++ with an effort being as lightweight and conceptually clean as possible.

Horde3D requires a fully OpenGL 2.0 compatible graphics card. In terms of DirectX that means a card supporting at least Shader Model 2.0 or higher.

## Features

- Modern, cross-platform, shader-based architecture (requires OpenGL 2.0+)
    - Lightweight, non-intrusive design with very few dependencies, avoiding complexity where possible
    - C-style API for easy usage from virtually any programming language
- Resource management
    - Garbage collected resources, loaded from virtually any type of data stream
    - Hot-reloading of resources for more increased productivity during development
    - Access to vertex data for collision detection and interoperability with physics engines
- Übershader-based, customizable rendering pipeline
    - Hot-reloading of pipelines for rapid testing of different rendering techniques
    - Support for post processing effects like bloom, DOF or motion blur
    - Support for almost all forward, deferred and High Dynamic Range rendering techniques
    - Support for real-time reflections and other techniques that require several cameras
    - Support for geometry, tessellation and compute shaders
    - Real-time shadows using Parallel Split Shadow Maps (PSSM)
    - Particle systems that can cast shadows and have effects like motion blur
- Unified scene system
    - World, models and skeletons are scene nodes instead of special objects
    - Frustum culling based on spatial graph
    - Hardware occlusion culling
    - Level of detail for model geometry and materials
- Unified, low-level animation system
    - Key frame animation for joints and meshes
    - Skeletal animation with up to 4 weights per vertex for articulated models
    - Layered animation blending and mixing using masks and additive channels
    - Morph targets for facial animation and lip synchronization
    - Access to joint data for dynamic animations and ragdoll physics
- Content Pipeline
    - Mixture of binary and XML formats for best tradeoff between performance and productivity
        - Pipeline, material and scene descriptions are XML
        - Model and animation are binary for maximum performance
        - Textures are common image formats (DDS, PNG, JPEG, etc.)
    - COLLADA Converter for importing assets from many common DCC tools
      - Calculation of tangent space basis for normal mapping
      - Optimization of geometry for GPU post-transform vertex cache
    - Editor for composing scenes, developing shaders and rendering techniques

## Building

You need to have a C++ compiler and [CMake 2.8+](http://www.cmake.org/) installed.

### Use of CMake

**CMake** is a meta-build system, e.g. it creates Makefiles or Visual Studio files using Generators. The main ways to use CMake are `cmake-gui` (Qt Interface), `ccmake` (Curses Interface) and `cmake` (Commandline Interface). Instructions for commonly used generators:

- [Qt Creator](http://qt-project.org/downloads#qt-creator): open `CMakeLists.txt` as new project, follow the instructions, hit build and you're done.
- [Visual Studio](http://www.microsoft.com/visualstudio/eng/products/visual-studio-express-products): start `cmake-gui`, choose OGDF as source path, `build-vs` as build path, press generate, open `build-vs\Horde3D.sln` and start compiling. You could also generate the solution from the command line running ``mkdir build-vs && cd build-vs && cmake -G "Visual Studio XYZ" ..``, where XYZ is the correct identifier for the desired version of Visual Studio (i.e. `8 2005` for VS 2005, `9 2008` for VS 2008, `10` for VS 2010, `11` for VS 2011, etc. Please run ``cmake --help`` for more info).
- [Xcode](https://developer.apple.com/xcode/): open up a terminal, navigate to the repository and run ``mkdir build-xcode && cd build-xcode && cmake -G "Xcode" ..``, then open the generated project file inside Xcode.
- [Makefiles](http://www.gnu.org/software/make/): open up a terminal, navigate to the repository and run ``mkdir build-make && cd build-make && cmake -G "Unix Makefiles" .. && make`` (hint: use `export JOBS=MAX` to speed things up).
- [Ninja](http://martine.github.io/ninja/): open up a terminal, navigate to the repository and run ``mkdir build-ninja && cd build-ninja && cmake -G "Ninja" .. && ninja``.

### Build samples

In order to build the samples you need [GLFW](http://www.glfw.org/download.html) *(>3.x)*.

By default, if not present on the system, a default version will be automatically downloaded, built and linked for you.

You could force this behavior using `HORDE3D_FORCE_DOWNLOAD_GLFW` flag with CMake (from your build directory):

     cmake -DHORDE3D_FORCE_DOWNLOAD_GLFW=ON ..

On **Debian/Ubuntu** platforms, you also need to install the following packages:

     sudo apt-get install xorg-dev

You could also skip sample building using `HORDE3D_BUILD_EXAMPLES` flag with CMake (from your build directory):

     cmake -DHORDE3D_BUILD_EXAMPLES=OFF ..

### Build Horde3D scene editor

There is also a scene editor available for Horde3D. To enabling build of the editor, first make sure you have the Qt 4.8 or any newer Qt 5.x SDK installed. To enable creating makefiles
for the editor via cmake set the HORDE3D_BUILD_EDITOR flag to ON (default is OFF).

    cmake -DHORDE3D_BUILD_EDITOR=ON

As the editor needs Lua as a dependency you can either make sure the Lua development files can be found by cmake, or Lua will be automatically downloaded by CMake.

## What's next

Here are some quick links to help you get started:

- [Homepage](http://horde3d.org/)
- [Introduction Tutorial](http://www.horde3d.org/docs/html/_tutorial.html)
- [Reference Documentation](http://www.horde3d.org/docs/manual.html)
- [Community Forums](http://www.horde3d.org/forums)
- [Community Wiki](http://horde3d.org/wiki/)

## License

Horde3D is licensed under the [Eclipse Public License v1.0 (EPL)](http://www.eclipse.org/legal/epl-v10.html).

The EPL is a quite liberal license and has fewer restrictions than the popular LGPL. Basically it allows you to use Horde3D in free and commercial projects as long as you contribute improvements like bug fixes, optimizations and code refactorings back to the community. The EPL allows static linking and is not viral; hence it does not affect any other modules of your application.
