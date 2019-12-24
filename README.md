# tw1c3b0t Project

This repository contains BeagleBone Blue versions of the HAL, WPILibJ, and WPILibC projects. These are the core libraries for creating robot programs for the BeagleBone Blue (tw1c3b0t).

The tw1c3b0t is a low cost, small, and very portable robot that allows students to prepare for programming a FIRST Robotics Competition robot.  tw1c3b0t is based on the BeagleBone Blue (https://beagleboard.org/blue).

This repository will be more or less up to date with the real allwpilib, though various hacks will be made so that it can still run on a tw1c3b0t.  For example, tw1c3b0t does not support or require connection to a FIRST Field Management System - just a cheap bluetooth joystick.

FRC 1481 - The Riveters



------------------ remainder copied from allwpilib ------------------



# Building WPILib

Using Gradle makes building WPILib very straightforward. It only has a few dependencies on outside tools, such as the ARM cross compiler for creating roboRIO binaries.

## Requirements

- A C++ compiler
    - On Linux, GCC works fine
    - On Windows, you need Visual Studio 2019 (the free community edition works fine).
      Make sure to select the C++ Programming Language for installation
- [ARM Compiler Toolchain](https://github.com/wpilibsuite/toolchain-builder/releases)
  * Note that for 2020 and beyond, you should use version 7 or greater of GCC
- Doxygen (Only required if you want to build the C++ documentation)

## Setup

Clone the WPILib repository. If the toolchains are not installed, install them, and make sure they are available on the system PATH.

See the [styleguide README](https://github.com/wpilibsuite/styleguide/blob/master/README.md) for wpiformat setup instructions.

## Building

All build steps are executed using the Gradle wrapper, `gradlew`. Each target that Gradle can build is referred to as a task. The most common Gradle task to use is `build`. This will build all the outputs created by WPILib. To run, open a console and cd into the cloned WPILib directory. Then:

```bash
./gradlew build
```

To build a specific subproject, such as WPILibC, you must access the subproject and run the build task only on that project. Accessing a subproject in Gradle is quite easy. Simply use `:subproject_name:task_name` with the Gradle wrapper. For example, building just WPILibC:

```bash
./gradlew :wpilibc:build
```

If you have installed the FRC Toolchain to a directory other than the default, or if the Toolchain location is not on your System PATH, you can pass the `toolChainPath` property to specify where it is located. Example:

```bash
./gradlew build -PtoolChainPath=some/path/to/frc/toolchain/bin
```

If you also want simulation to be built, add -PmakeSim. This requires gazebo_transport. We have tested on 14.04 and 15.05, but any correct install of Gazebo should work, even on Windows if you build Gazebo from source. Correct means CMake needs to be able to find gazebo-config.cmake. See [The Gazebo website](https://gazebosim.org/) for installation instructions.

```bash
./gradlew build -PmakeSim
```

If you prefer to use CMake directly, the you can still do so.
The common CMake tasks are wpilibcSim, frc_gazebo_plugins, and gz_msgs

```bash
mkdir build #run this in the root of allwpilib
cd build
cmake ..
make
```

The gradlew wrapper only exists in the root of the main project, so be sure to run all commands from there. All of the subprojects have build tasks that can be run. Gradle automatically determines and rebuilds dependencies, so if you make a change in the HAL and then run `./gradlew :wpilibc:build`, the HAL will be rebuilt, then WPILibC.

There are a few tasks other than `build` available. To see them, run the meta-task `tasks`. This will print a list of all available tasks, with a description of each task.

wpiformat can be executed anywhere in the repository via `py -3 -m wpiformat` on Windows or `python3 -m wpiformat` on other platforms.

CMake is also supported for building. See [README-CMAKE.md](README-CMAKE.md).
