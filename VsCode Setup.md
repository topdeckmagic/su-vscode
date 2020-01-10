# Using VS Code in Seattle University Graduate Classes

The goal of this document is to help other people in the program understand how to setup VSCode as an IDE that works smoothly with submissions to CS1 and allows for support of multiple languages.

## Installing VSCode

### PC Users

1. Install a supported open SSH client [here](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
2. Install VSCode [here](https://code.visualstudio.com/)
3. Install the Remote Development Extension Pack [here](https://aka.ms/vscode-remote/download/extension)

### MAC Users (Untested but I think this works)

1. Install VSCode [here](https://code.visualstudio.com/)
2. Install the Remote Development Extension Pack [here](https://aka.ms/vscode-remote/download/extension)

## Connecting to CS1

To enable the easiest integration you will actually have your terminal in VSCode directly connectedt to CS1, this means that you are storing your files, building and debugging based on the configuration of CS1.

1. Open the command pallete in VSCode (press F1 or ctrl + shift + p)
2. Type ""Remote-SSH: Connect to Host..." and press enter.
3. Enter the host information, this will be yourusername@cs1.seattleu.edu
4. You will be prompted for a password, provide your school password and press enter

At this point your terminal will be connected to cs1 and you can issues normal cs1 commands from within the VSCode terminal.  Additionally for PC users this means no more Putty and WinSCP, you can now SSH directly from a Power Shell window.

Note: To avoide having to do this again it's a good idea to save your workspace (File -> Save Workspace As...), in VSCode a workspace is a set of configurations for the IDE that you can quickly relaunch.

## Ensuring CS1 has the correct G++ settings for your profile

Once you are connected to CS1 you need to run this command to ensure that you get the correct warnings and errors on build commands.  This ensures that you don't get any surprises when it comes to submission time.  From the terminal to cs1 run:

```echo "alias g++='g++ -Wall -Werror -pedantic -std=c++11'" >>~/.bashrc```

## Developing in C++ with VSCode

To get familiar with VSCode for C++ you can follow the tutorial [here](https://code.visualstudio.com/docs/cpp/config-wsl#_add-a-source-code-file), you can ignore everything before Add A Source Code File (unless you are curious about how to develop on Linux locally on Windows Subsystem for Linux).

In general to setup a new work space for C++ these are the steps that you will want to follow.

1. Connect to cs1.seattleu.edu by running ```ssh <yourusername>@cs1.seattleu.edu``` (note: by default this lands you in your student home directory).
2. Create a new folder for the class ```mkdir cpsc5041```
3. Execute ```exit``` to log out of your SSH session
4. Open a new VSCode Window ```Ctrl+Shift+N```
5. Open the command pallette ```Ctrl+Shift+P``` and search for "Remote-SSH: Connect to Host..." and press ```Enter```
6. Either select your existing ssh connection definition for cs1 or type yourusername@cs1.seattleu.edu and press enter
7. Enter your password

TODO: Finish adding these steps...

## TODO: Developing in Python with VSCode
