# Using VS Code in Seattle University Graduate Classes

The goal of this document is to help other people in the program understand how to setup Visual Studio Enterprise as an IDE that works smoothly with submissions to CS1 and allows for support of multiple languages.

## Installing Visual Studio Enterprise

### PC Users
1. Install a supported open SSH client [here](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
2. Install Visual Studio Enterprise [here](https://visualstudio.microsoft.com/downloads/).  Note: Some new capabilities require the preview version of Visual Studio Enterprise, this is generally a stable build and comes with the latest and greatest.
3. During the install, select Linux Development with C++.  You may want other areas of Visual Studio Enterprise but you can always modify your install at a later time by launching the Visual Studio Installer and selecting Modify.

##  Building on CS1

To enable the easiest integration you will configure Visual Studio Enterprise to leverage CS1 as a remove build environment. Building your solution will push the files, build the projects and build on CS1. This ensures that you are getting immediate feedback if there are issues with compilation of your file. When you launch Visual Studio Code you will be prompted to create a new project, for the purposes of this walk through we will create a Solution that has multiple projects.

### Creating A Simple Solution
First we will need a simple solution that we can use to configure our development environment.

1. Select "Create New Project" on the Visual Studio Enterprise Start Page
2. Filter language to "C++"
3. Select "Console App" and click "Next"
4. Input the following:

    | Field         | Value                         |
    | ------------- |:-----------------------------:|
    | Project Name  | Server                        |
    | Location      | Local Path To Save Your Files |
    | Solution Name | ServerClientHelloWorld        |

5. Click "Create"
6. At this point you have a Solution with a single Project.

### Adding a Remote System
Next we need to add CS1 as a remote system for Visual Studio Enterprise.

1. Go to Tools -> Options and search for and select "Connection Manager"
2. Click Add
3. Complete the form with the following values

    | Field               | Value                         |
    | ------------------- |:-----------------------------:|
    | Host Name           | cs1.seattleu.edu              |
    | Port                | 22                            |
    | User Name           | Your username at SeattleU     |
    | Authentication Type | Password                      |
    | Password            | Your SeattleU password        |

### Configuring Your Project
 Now we need to configure our project to use CS1.

 1. Right click on your project (Server (Linux)) and choose "Properties"
 2. Update the Remote Build Machine to select your Remote System created above
 3. Specify a root directory you want this project to build in. I follow a convention of ~/class/SolutionName (ie ~/cs5042/ServerClientHelloWorld)

 ### Build and Run Your Solution
 At this point it should be working!

 1. Press F7 To Build the Solution
 2. Open a Terminal Window View -> Terminal (Requires Preview Version of VS)
 3. SSH Into CS1 by typing ssh <username>@cs1.seattleu.edu into the Terminal
 4. Navigate to the project (ie cd cs5042/ServerClientHelloWorld/Server/bin/x64/Debug)
 5. Run "./Server.out"
 6. 
