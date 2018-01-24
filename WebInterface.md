# Web Interface

## Introduction

**Note** it's not necessary to have web interface for ESPurna to run on your device. You can configure all options at compile time or you can use the [terminal](Terminal) interface to do it once you flash the firmware.

**Note** Previous versions of ESPurna (prior to 1.7.0) used the SPIFFS partition to store the static contents for the web interface (HTML, scripts, style sheets, images). Since 1.7.0 all these resources are encoded into a header file (a file with the .h extension) and copied to program memory (PROGMEM) during the build process. This means they are included in the firmware image and only one flash step is required. The overall size of the image is (of course) bigger than just the code but way smaller than the firmware plus the filesystem size. In particular this means that 512Kb devices can now have the full featured web interface.

## Web interface build process explanation

The build process of the web interface performs different steps:

1. Inlining images: any reference to an image in the HTML or the CSS files is converted into the base64 representation of the image and inlined in the code.
1. Inlining scripts and stylesheets: CSS and JS files are cleaned and inlined in the same order they appear in the HTML file
1. Minifing contents: the HTML file (along with the inline scripts and styles) is minified, comments, spaces and line breaks are removed.
1. Compressing contents: everything is the compressed in a single GZIP file (same format the web servers use to send compressed contents).
1. Embedding in program memory: the GZIP file is then encoded in a byte array as a PROGMEM constant, ready to be included and compiled within the firmware image.

## Web interface build process

All the previous steps are performed by a **[Gulp](http://gulpjs.com/)** script. Gulp is a build system built in [node.js](https://nodejs.org/en/). So you will need node (and [npm](https://www.npmjs.com/), its package manager) first. [Read the documentation](https://docs.npmjs.com/getting-started/installing-node) on how to install them.

Once you have node and npm installed, go to the 'code' folder and install all the dependencies with:

```
npm install --only=dev
```

It will take a minute or two. Then you are ready to build the web interface files with:

```
node node_modules/gulp/bin/gulp.js
```

It will create a populate the 'code/espurna/static' folder with a 'code/espurna/static/index.html.gz.h' file with the byte array to be included in the code.

## Troubleshooting

Some users have had issue with old versions of NodeJS. Check you have at least 4.6.0. They have reported they had to install additional packages but that is still untested and I don't want to add things I'm not sure they are needed. Check issue #147.

## Flashing it

Once you have the 'code/espurna/static/index.html.gz.h' file, it is included from the 'code/espurna/web.ino' file and compiled with the firmware image. Read the sections related to building the firmware using [PlatformIO](PlatformIO.md) or [Arduino IDE](ArduinoIDE.md).