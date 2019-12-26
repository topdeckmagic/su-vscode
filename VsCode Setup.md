# Overview
The goal of this document is to help other people in the program understand how to setup VSCode as an IDE that works smoothly with submissions to CS1 and allows for support of multiple languages.

# Installing VSCode
## PC Users
1. Install a upported open SSH client: https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client
2. Install VSCode: https://code.visualstudio.com/
3. Install the Remote Development Extension Pack: https://aka.ms/vscode-remote/download/extension

## MAC Users (Untested but I think this works)
1. Install VSCode: https://code.visualstudio.com/
2. Install the Remote Development Extension Pack: https://aka.ms/vscode-remote/download/extension

# Connecting to CS1
To enable the easiest integration you will actually have your terminal in VSCode directly connectedt to CS1, this means that you are storing your files, building and debugging based on the configuration fo CS1.

1. Open the command pallete in VSCode (press F1)
2. Type ""Remote-SSH: Connect to Host..." and press enter.
3. Enter the host information, this will be yourusername@cs1.seattleu.edu
4. You will be prompted for a password, provide your school password and press enter

At this point your terminal will be connected to cs1 and you can issues normal cs1 commands from within the VSCode terminal.

Note: To avoide having to do this again it's a good idea to save your workspace (File -> Save Workspace As...), in VSCode a workspace is a set of configurations for the IDE that you can quickly relaunch.

To get familiar with VSCode for C++ you can follow the tutorial here: https://code.visualstudio.com/docs/cpp/config-wsl#_add-a-source-code-file, you can ignore everything before Add A Source Code File (unless you are curious about how to develop on Linux locally on Windows).

# Ensuring CS1 has the correct G++ settings for your profile
Once you are connected to CS1 you need to run this command to ensure that you get the correct warnings and errors on build commands.  This ensures that you don't get any surprises when it comes to submission time.  From the terminal to cs1 run:

```echo "alias g++='g++ -Wall -Werror -pedantic -std=c++11'" >>~/.bashrc```