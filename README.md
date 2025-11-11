# C++

> This repository contains all my self study notes on C++.

## Table of Contents

1. [Installation and Setup]()

---

## Chapter 01. Installation and Setup

### Install C++ compiler

#### Using mingw64

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
- Extensions: type "franneck94" in the search and install:
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

#### Configure a Build Task

- Go to `Terminal -> Configure Default Build Task`
- Select `g++.exe` build active file

A new `tasks.json` file is created inside `.vscode` folder.

In `"args"`, add:

- `"-Wall"`
- `"-std=c++17"`
- replace `"${file}"` with `"${fileDirname}\\*.cpp"`

#### Build and Run the program

Select the `.cpp` file and click on `Terminal -> Run Build Task` or `Ctrl + Shift + B`.

This will create the `.exe` file.

Right click the `.exe` file -> `Open in Integrated Terminal`.

In the terminal, type: `.\main.exe` to run the program.

#### Create another project

Click on the previous project and press `Esc` -> now we can create new folder as a new project inside the same 
parent folder.

Now, when we create new `.cpp` files, click on `Terminal -> Run Build Task` or `Ctrl + Shift + B`, same as above for 
build and run section.

#### Debugger










