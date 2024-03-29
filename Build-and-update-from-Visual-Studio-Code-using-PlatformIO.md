This page summarizes all you need to compile and deploy Espurna on Windows 10 with Visual Studio Code (VSCode). VSCode is a free, open source, light IDE from Microsoft.

# Install main components

## Git for Windows

Download it from https://git-scm.com/download/win (choose appropriate version).

Ensure that it modifies the path variable.

## Visual Studio Code

Download it from https://code.visualstudio.com/docs/?dv=win

Ensure that it updates the PATH variable (default option).

## Node.js and npm

Download it from https://nodejs.org/en/download/ (more convenient with the ***Windows Installer*** (.msi) version)

NPM gets installed with node.js

Restart your computer. 

Launch Visual Studio Code. It should detect git (displaying a message in a git pane at the bottom of the window).

## Gulp

From VSC, open a terminal (<kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>\`</kbd> *OR* <kbd>CTRL</kbd>+<kbd>SHIFT</kbd>+<kbd>P</kbd> and search for `Terminal: Create New Integrated Terminal`) and run

```
npm install --global gulp-cli
```

# Install main extensions

From the extensions pane of Visual Studio Code install the following extensions.

Mandatory :
- Platformio IDE

Optionally :
- Python
- GitLens (to show modifications history)

# Get the code

Clone https://github.com/xoseperez/espurna.git

For example into `C:\Users\{user}\Documents\PlatformIO\Projects\xoseperez-espurna`

With VSCode, open `xoseperez-espurna\code` folder. PlatformIO IDE will start and detect platformio project.

# Build and update

Now you can build espurna, including web files, directly from Visual Studio Code.

To build / upload firmware for a specific board, use "Tasks / Run Task..." (<kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>T</kbd> by default) and search for "Build (...)" / "Upload (...)" tasks.

`PlatformIO: Build` and button on the bottom bar builds 'default' environment specified in 'code/platformio.ini' (`wemos-d1mini-relayshield` at the time of writing this)

## Environment variables for OTA uploads

OTA parameters are now picked up from environment variables.

You need to set them up for every `Upload (...-ota)` task you want to use. Here's how to do it:

- Press <kbd>F1</kbd> (on Mac it's usually <kbd>Fn</kbd>+<kbd>F1</kbd>)
- Select `Tasks: Configure Task` *(type a part of the name and click it when it appears)*
- Select `Upload (...-ota)` task you need to use *(type a part of the name and click it when it appears)*
- An editor for a JSON config opens. You'll see a section added with your task name, ex.:

```json
"type": "PlatformIO",
"task": "Upload (itead-sonoff-th-ota)",
"problemMatcher": [
    "$platformio"
]
```

- Add the `options` section before the `problemMatcher`, so you have this:

```json
"type": "PlatformIO",
"task": "Upload (itead-sonoff-th-ota)",
"options": {
    "env": {
        "ESPURNA_IP": "192.168.4.1",
        "ESPURNA_AUTH": "fibonacci"
    }
},
"problemMatcher": [
    "$platformio"
]
```

- If you have custom IP or password, put them here. Otherwise, use `192.168.4.1` and `fibonacci`
- If you have Zeroconf configured, you can use Zeroconf names here, ex: `sonoff-kitchen.local`
- Save and close the file. Now you can OTA upload this target successfully

To reuse the same environment (like `itead-sonoff-th-ota`) you will need to manually specify platformio command as a "shell" task. The pro is you can natively support several devices with different IPs and passwords right from the VSCode (ref: [Platform.IO documentation](http://docs.platformio.org/en/latest/ide/vscode.html#custom-tasks)).

For example, here we are declaring "Arbol1" and "Light1" tasks that use the same `itead-sonoff-basic-ota` environment:
```json
{
    "label": "PlatformIO: Arbol1",
    "type": "shell",
    "command": "platformio run -e itead-sonoff-basic-ota -t upload",
    "options": {
        "env": {
            "ESPURNA_IP": "192.168.1.100",
            "ESPURNA_AUTH": "---"
        }
    },
    "problemMatcher": [
        "$platformio"
    ]
},
{
    "label": "PlatformIO: Light1",
    "type": "shell",
    "command": "platformio run -e itead-sonoff-basic-ota -t upload",
    "options": {
        "env": {
            "ESPURNA_IP": "192.168.1.200",
            "ESPURNA_AUTH": "---"
        }
    },
    "problemMatcher": [
        "$platformio"
    ]
}
```
Source: **@oscarsan1**, [xoseperez/espurna#1515](https://github.com/xoseperez/espurna/issues/1515)
