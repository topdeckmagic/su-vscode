# Using VS Code in Seattle University Graduate Classes

The goal of this document is to help other people in the program understand how to setup VSCode as an IDE that works smoothly with submissions to CS1 and allows for support of multiple languages.

## Installing VSCode

### PC Users

1. Install a supported open SSH client [here](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
2. Install VSCode [here](https://code.visualstudio.com/)
3. Install the Remote Development Extension Pack [here](https://aka.ms/vscode-remote/download/extension)

### MAC Users

1. Install VSCode [here](https://code.visualstudio.com/)
2. Install the Remote Development Extension Pack [here](https://aka.ms/vscode-remote/download/extension)

## Connecting to CS1

To enable the easiest integration you will actually have your terminal in VSCode directly connected to CS1, this means that you are storing your files, building and debugging based on the configuration of CS1.

1. Open the command pallette in VSCode (press F1 or ctrl + shift + p)
2. Type ""Remote-SSH: Connect to Host..." and press enter.
3. Enter the host information, this will be yourusername@cs1.seattleu.edu
4. You will be prompted for a password, provide your school password and press enter

At this point your terminal will be connected to cs1 and you can issues normal cs1 commands from within the VSCode terminal.  Additionally for PC users this means no more Putty and WinSCP, you can now SSH directly from a Power Shell window.

Note: To avoid having to do this again it's a good idea to save your workspace (File -> Save Workspace As...), in VSCode a workspace is a set of configurations for the IDE that you can quickly relaunch.

## Ensuring CS1 has the correct G++ settings for your profile

Once you are connected to CS1 you need to run this command to ensure that you get the correct warnings and errors on build commands.  This ensures that you don't get any surprises when it comes to submission time.  From the terminal to cs1 run:

```echo "alias g++='g++ -Wall -Werror -pedantic -std=c++11'" >>~/.bashrc```

## Developing in C++ with VSCode

To get familiar with VSCode for C++ you can follow the tutorial [here](https://code.visualstudio.com/docs/cpp/config-wsl#_add-a-source-code-file), you can ignore everything before Add A Source Code File (unless you are curious about how to develop on Linux locally on Windows Subsystem for Linux).

In general to setup a new work space for C++ these are the steps that you will want to follow.

### Create a new folder for the class

1. Connect to cs1.seattleu.edu by running ```ssh <yourusername>@cs1.seattleu.edu``` from PowerShell (PC) or from Terminal(Mac)(note: by default this lands you in your student home directory).
2. Create a new folder for the class ```mkdir cpsc5041```
3. Execute ```exit``` to log out of your SSH session

### Setup a new VSCode Workspace in That Folder

1. Open a new VSCode Window ```Ctrl+Shift+N```
2. Open the command pallette ```Ctrl+Shift+P``` and search for "Remote-SSH: Connect to Host..." and press ```Enter```
3. Either select your existing ssh connection definition for cs1 or type yourusername@cs1.seattleu.edu and press enter
4. Enter your password
5. Select the the top charm on the left toolbar in VSCode (this is the file charm) and click "Open Folder"
6. Select the folder you created in step 2, this will re-launch VSCode in that folder.

### Configuring C++ Build and Debug Tasks to Align with CS1

By default VSCode will start to suggest configurations as you code.  To ensure that we have the right configuration for C++ submissions on CS1 you can follow these steps:

1. Install the C++ for Visual Studio Code extension [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
2. In the terminal run ```mkdir .vscode```
3. Then create the following three files in that directory with the associated content:

#### c_cpp_properties.json

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "compilerPath": "/opt/rh/devtoolset-8/root/bin//gcc",
            "cStandard": "c11",
            "cppStandard": "c++11"
        }
    ],
    "version": 4
}
```

#### launch.json

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++ build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "g++ build active file",
            "miDebuggerPath": "/opt/rh/devtoolset-8/root/bin/gdb"
        }
    ]
}
```

#### tasks.json

```json
{
    "tasks": [
        {
            "type": "shell",
            "label": "g++ build active file",
            "command": "/opt/rh/devtoolset-8/root/bin//g++",
            "args": [
                "-ansi",
                "-pedantic",
                "-Wall",
                "-Werror",
                "-std=c++11",
                "-g",
                "${fileDirname}/**.cpp",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "/opt/rh/devtoolset-8/root/bin/"
            },
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ],
    "version": "2.0.0"
}
```

Once these are created you can build the file you are currently working with byt pressing ```Ctrl+Shift+B```. It will effectively run g++ yourfile.cpp with all of the relevant cs1 flags.  Additionally you will be able to enter a debug session by pressing ```F5```.
