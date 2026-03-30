# C++

> This repository contains all my self-study notes on C++.

## Table of Contents

1. [Installation and Setup](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#chapter-01-installation-and-setup)
    - [Install C++ compiler](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#install-c-compiler)
    - [Install VS Code](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#install-vs-code)
    - [Setting the workspace](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#setting-the-workspace)
    - [Install WSL2 on Windows](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#install-wsl2-on-windows)
2. [Make and Makefiles](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#chapter-02-make-and-makefiles)
    - [Basic Structure](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#basic-structure)
    - [Variables](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#variables)
    - [Wild cards](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#wild-cards)
3. [Modern CMake](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#chapter-03-modern-cmake)
    - [VS Code with CMake Extension](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#vs-code-with-cmake-extension)
    - [First Project with CMake](https://github.com/backstreetbrogrammer/56_CPlusPlus?tab=readme-ov-file#first-project-with-cmake)

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

To run any program or `cd` to any folder in `Windows` from `Ubuntu`, use the following directory structure:

```
cd /mnt/c/Users/~/ApacheKafka

# run with partition = 0 (args[0]) 
java -cp ./target/ApacheKafka-1.0-SNAPSHOT-jar-with-dependencies.jar -Xms128m -Xmx1024m com.backstreetbrogrammer.producer.KafkaProducerDemo 0
```

---

## Chapter 02. Make and Makefiles

[Makefile Github Repository](https://github.com/franneck94/UdemyMakefile)

- Open a new Folder in VS Code
- Create a simple `main.cpp`

On Terminal or cmd, we can run:

```
$ g++.exe .\main.cc -o .\main
$ .\main.exe
Hello, World!
```

OR, we can just type this in `Makefile`:

```
# TARGETS

build: 
	g++ main.cc -o main 
```

And run on terminal: `make`.

It will create `main.exe`.

- Adding another target:

```
# TARGETS

build: 
	g++ main.cc -o main 

execute:
	./main
```

On terminal, if we just type `make`, always the first target will be run from top: `make build`

To run `execute` target, type: `make execute`.

We can have **multiple** commands in a target.

```
# TARGETS
# target: prerequisites
# 	commands

build: 
	g++ main.cc -c main.o 
	g++ main.o -o main 

execute:
	./main

clean:
	rm -rf *.o main
```

### Basic Structure

Suppose we have more than source files in the same folder.

Our `Makefile` can be:

```
# TARGETS
# target: prerequisites
# 	commands

build: main.o my_lib.o
	g++ main.o my_lib.o -o main

main.o:
	g++ main.cc -c

my_lib.o:
	g++ my_lib.cc -c

execute:
	./main

clean:
	rm -rf *.o main
```

As seen above, `Makefile` is used to make **files**.

We are explicitly specifying the prerequisite dependencies and the commands to build the project.

### Variables

We can declare variables in `Makefile` to avoid repetition of code and make it more maintainable.

Also, we can use if-else statements to set the variables.

```
###############
## VARIABLES ##
###############
# Note: Variables can only be strings
# Note: Single or double quotes for variable names or values have no meaning to Make

# CC: Program for compiling C programs; default cc
# CXX: Program for compiling C++ programs; default g++
# CFLAGS: Extra flags to give to the C compiler
# CXXFLAGS: Extra flags to give to the C++ compiler
# CPPFLAGS: Extra flags to give to the C preprocessor
# LDFLAGS: Extra flags to give to the linker

DEBUG = 1
EXECUTABLE_NAME = main

CXX_STANDARD = c++17
CXX_WARNINGS = -Wall -Wextra -Wpedantic
CXX = g++
CXXFLAGS = $(CXX_WARNINGS) -std=$(CXX_STANDARD)
LDFLAGS =

ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
else
CXXFLAGS += -O3
endif

COMPILER_CALL = $(CXX) $(CXXFLAGS)

build: my_lib.o main.o
	$(COMPILER_CALL) main.o my_lib.o $(LDFLAGS) -o $(EXECUTABLE_NAME)

main.o:
	$(COMPILER_CALL) main.cc -c

my_lib.o:
	$(COMPILER_CALL) my_lib.cc -c

execute:
	./main

clean:
	rm -f *.o main

```

### Wild cards

We can use wild cards to avoid writing the same code again and again for each source file.

```
DEBUG = 1
EXECUTABLE_NAME = main

CXX_STANDARD = c++17
CXX_WARNINGS = -Wall -Wextra -Wpedantic
CXX = g++
CXXFLAGS = $(CXX_WARNINGS) -std=$(CXX_STANDARD)
LDFLAGS =

ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
else
CXXFLAGS += -O3
endif

CXX_COMPILER_CALL = $(CXX) $(CXXFLAGS)

CXX_OBJECTS = my_lib.o main.o

build: $(CXX_OBJECTS)
	$(CXX_COMPILER_CALL) $(CXX_OBJECTS) $(LDFLAGS) -o $(EXECUTABLE_NAME)

execute:
	./main

clean:
	rm -f *.o main

##############
## PATTERNS ##
##############
# $@: the file name of the target
# $<: the name of the first dependency
# $^: the names of all prerequisites
%.o: %.cc
	$(CXX_COMPILER_CALL) -c $< -o $@

```

As seen above, we can use pattern rules to avoid writing the same code for each source file.

We can also use pattern substitution to generate the list of object files from the list of source files.

```
DEBUG = 1

CXX_STANDARD = c++17
CXX_WARNINGS = -Wall -Wextra -Wpedantic
CXX = g++
CXXFLAGS = $(CXX_WARNINGS) -std=$(CXX_STANDARD)
LDFLAGS =

ifeq ($(DEBUG), 1)
CXXFLAGS += -g -O0
EXECUTABLE_NAME = mainDebug
else
CXXFLAGS += -O3
EXECUTABLE_NAME = mainRelease
endif

CXX_COMPILER_CALL = $(CXX) $(CXXFLAGS)

CXX_SOURCES = $(wildcard *.cc)
CXX_OBJECTS = $(patsubst %.cc, %.o, $(CXX_SOURCES))

##############
## TARGETS  ##
##############
build: $(CXX_OBJECTS)
	$(CXX_COMPILER_CALL) $(CXX_OBJECTS) $(LDFLAGS) -o $(EXECUTABLE_NAME)

execute:
	./$(EXECUTABLE_NAME)

clean:
	rm -f *.o $(EXECUTABLE_NAME)

##############
## PATTERNS ##
##############
%.o: %.cc
	$(CXX_COMPILER_CALL) -c $< -o $@

```

---

## Chapter 03. Modern CMake

[CMake Github Repository](https://github.com/franneck94/UdemyCmake)

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

