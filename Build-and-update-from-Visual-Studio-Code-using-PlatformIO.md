This page summarizes all you need to compil and deploy Espurna on Windows 10 with Visual Studio Code.

# Install main components

## Install git

Download it from https://git-scm.com/download/win (choose appropriate version).

Ensure that it modifies the path variable.

## Install Visual studio code

Download it from https://code.visualstudio.com/docs/?dv=win

Ensure that it updates the PATH variable (default option).

## Install node.js

Download it from 

- node.js (including npm)

Restart your computer. Lauch Visual studio code. It should detect git (displaying a message in a git pane at the bottom of the vsc window).

## Install gulp

From VSC, open a terminal (`CTRL+ù`) and run

    `npm install --global gulp-cli`

# Install main extensions

From the extensions pane of Visual studio code install the following extensions.

Mandatory :
- Platformio IDE
And, optionaly, the usefull :
- Python
- GitLens (to show authors of modifications)

# Get the espurna code

Clone https://github.com/xoseperez/espurna.git

For example into `C:\Users\{user}\Documents\PlatformIO\Projects\xoseperez=espurna`

With Visual studio, open `code` folder. PlatformIO stars and detects taks.

# Build and update

Now you can build espurna, including web files, directly from Visual Studio Code.