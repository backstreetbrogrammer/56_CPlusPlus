# C++

> This repository contains all my self-study notes on C++.

## Table of Contents

1. [Installation and Setup]()
    - [Install C++ compiler]()
    - [Install VS Code]()
    - [Setting the workspace]()
2. [Modern CMake]()

---

## Chapter 01. Installation and Setup

### Install C++ compiler

**Using mingw64**

- Open [winlibs](https://winlibs.com/)
- Jump to `Download`
- Win64: Zip Archive
- Extract the zip file to `C:\MinGW64\mingw64`
- Add the path: `C:\MinGW64\mingw64\bin`
- Verify: open `cmd` and type `g++ --version`

```
C:\Users\rishi>g++ --version
g++ (MinGW-W64 x86_64-ucrt-posix-seh, built by Brecht Sanders) 13.1.0
Copyright (C) 2023 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

### Install VS Code

- Open [VS Code](https://code.visualstudio.com/)
- Click on `Download for Windows`
- Install the exe
- Launch VS Code
- Extensions: type "C/C++" in the search and install:
    - C/C++: Microsoft
    - C/C++ Extension Pack: Microsoft
    - C/C++ Themes: Microsoft
- Extensions: type `"franneck94"` in the search and install:
    - Coding Tools Extension Pack
    - C/C++ Extension Pack
    - C/C++ Runner
- Restart VS Code

### Setting the workspace

- Create a folder in Windows
- Open Folder from VS Code
- Create new projects folder inside the parent folder
- These folders will work as separate projects containing `main.cpp`

Once the source code is written, click on the `.cpp` file and open `View -> Command Palette` or `Ctrl + Shift + P`.

- Select `C/C++: Edit Configurations (UI)`
- Compiler Path: chose `g++` and not `gcc`
- C++ Standard: chose `c++17` and save

A new `.vscode` folder will be created containing a file: `c_cpp_properties.json`.

**Configure a Build Task**

- Go to `Terminal -> Configure Default Build Task`
- Select `g++.exe` build active file

A new `tasks.json` file is created inside `.vscode` folder.

In `"args"`, add:

- `"-Wall"`
- `"-std=c++17"`
- replace `"${file}"` with `"${fileDirname}\\*.cpp"`

**Build and Run the program**

Select the `.cpp` file and click on `Terminal -> Run Build Task` or `Ctrl + Shift + B`.

This will create the `.exe` file.

Right-click the `.exe` file -> `Open in Integrated Terminal`.

In the terminal, type: `.\main.exe` to run the program.

**Create another project**

Click on the previous project and press `Esc` -> now we can create new folder as a new project inside the same
parent folder.

Now, when we create new `.cpp` files, click on `Terminal -> Run Build Task` or `Ctrl + Shift + B`, same as above for
the build and run section.

**Debugger**

- Click on one `main.cpp` file
- Click on `Run -> Add Configuration`
- Select `C++ (GDB/LLDB)`
- Select `g++.exe build and debug active file`

This will create `launch.json` file inside `.vscode` folder.

In `"configurations"`, edit:

- "program": `"${fileDirname}\\${fileBasenameNoExtension}.exe"`
- "cwd": `"${fileDirname}"`

Now, we can set breakpoints and click on `Run -> Start Debugging` or `F5` to debug the program.

### Install WSL2 on Windows

- Open Powershell in administrative mode
- Type this command: `wsl --install`
- Restart the system
- After restart, `Ubuntu` app will be installed
- Launch `Ubuntu` app
- Set up Linux username and password
- Disable IPv6 on WSL2

```
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
```

Install `C++` by running the following commands one by one:

```
sudo apt-get update
sudo apt-get upgrade

# Mandatory
sudo apt-get install gcc g++ gdb
sudo apt-get install make cmake
sudo apt-get install git
sudo apt-get install doxygen
sudo apt-get install python3 python3-pip

# Optional
sudo apt-get install lcov gcovr
sudo apt-get install ccache
sudo apt-get install cppcheck
sudo apt-get install llvm clang-format clang-tidy
sudo apt-get install curl zip unzip tar
sudo apt-get install graphviz
```

---

## Chapter 02. Modern CMake

[Github Repository](https://github.com/franneck94/UdemyCmake)

[VSCode Shortcuts](https://github.com/franneck94/VSCodeGuide/blob/master/usefulShortcuts.md)

Important VSCode settings such that the CMake Extension behaves the same as in the videos:

```
"cmake.showOptionsMovedNotification": false,
"cmake.options.statusBarVisibility": "visible",
```

### VS Code with CMake Extension

- Open VS Code
- Extensions: type `"franneck94"` in the search and install:
    - Coding Tools Extension Pack
    - C/C++ Extension Pack
    - C/C++ Runner
- Restart VS Code

Open the course folder in VS Code: `C:\Users\rishi\Downloads\BuildWithTech\CPlusPlus\UdemyCmake`

- Open `View -> Command Palette` or `Ctrl + Shift + P`
- Type `Generate C++ Config Files` => this will create `.vscode` folder with `settings.json` file

Copy these lines from local settings to global settings:

```
    "cmake.configureOnOpen": false,
    "cmake.autoSelectActiveFolder": false,
    "cmake.configureOnEdit": false,
    "[cmake]": {
        "editor.formatOnSave": false,
        "editor.defaultFormatter": "cheshirekow.cmake-format"
    },
```

- Global Settings are found at the left bottom corner
- Choose `User` tab
- Click on the `Open Settings` icon in the top right corner
- Paste the copied lines inside the JSON file and save

**WSL in VS Code**

- Install `WSL` extension from Microsoft
- Open `View -> Command Palette` or `Ctrl + Shift + P`
- Type `Reopen folder in WSL`
- Reinstall extensions inside WSL
- Extensions: type `"franneck94"` in the search and install:
    - Coding Tools Extension Pack
    - C/C++ Extension Pack
    - C/C++ Runner

Now every time we want to work on a project, we need to open the folder in WSL.

### First Project with CMake

- In VS Code, Open Folder as `C:\Users\rishi\Downloads\BuildWithTech\CPlusPlus\UdemyCmake\2_CMake\01_HelloWorld`
- Create `main.cc` file with the following code:

```cpp
#include <iostream>

int main()
{
    std::cout << "Hello World\n";

    return 0;
}
```

- Create `CMakeLists.txt` file with the following code:

```cmake
# 0.) Create Source and CMakeFile
# 1.) mkdir build
# 2.) cd build
# 3.) cmake ..   -  Generting the Build Files / Configure the Project
# 4.) cmake --build .
# 5.) ./Executable

cmake_minimum_required(VERSION 3.22)

project(CppProjectTemplate VERSION 1.0.0 LANGUAGES C CXX)

#          User defined name
#                  v
add_executable(Executable main.cc)
```

- follow the steps given as above

Alternatively, we can use the `CMake` extension to build the project:

- Chose the Kit in the bottom bar (`GCC 11.4.0` for WSL)

As soon as we chose the `Kit`, the `CMake` extension will automatically create a `build` folder and run the
configuration step.

Other steps:

- Click on the `CMake: [Debug]` in the bottom bar to choose the build type => for dev, we will use `Debug`
- Click on the `CMake: [Build]` in the bottom bar to build the project
- Click on the `CMake: [Run]` in the bottom bar to run the project

**Generators**

Run the command: `cmake --help`

This will list down all the available generators.

Generator for GCC and Clang: `Unix Makefiles`

```
cd build
cmake -S .. -B . -G "Unix Makefiles" # Option 1
cmake .. -G "Unix Makefiles" # Option 2
```

**Basic Project Structure**

```
C:\Users\rishi\Downloads\BuildWithTech\56_CPlusPlus\02_BasicProject
```

We can create a `C++` project on Windows.

When done with the code, we can build and run it on WSL.

We can use separate target for cmake commands:

```cmake --build . --target <target_name>```

For example, we can create a target for Library:

```cmake
cmake --build . --target Library
```

Or, for Executable:

```cmake
cmake --build . --target Executable
```

**Intermediate Project Structure**

