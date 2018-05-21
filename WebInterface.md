## Introduction
**Note** This repository already contains prebuilt 'index.html.gz.h' and it is not necessary to build it yourself unless 
 files in 'code/html' are modified.

**Note** It is not necessary to have the web interface for ESPurna to run on your device. You can configure all options at compile time or you can use the [terminal](Terminal) interface to do it once you flash the firmware.

**Note** Previous versions of ESPurna (prior to 1.7.0) used the SPIFFS partition to store the static contents for the web interface (HTML, scripts, style sheets, images). Since 1.7.0 all these resources are encoded into a header file (a file with the .h extension) and copied to program memory (PROGMEM) during the build process. This means they are included in the firmware image and only one flash step is required. The overall size of the image is (of course) bigger than just the code but way smaller than the firmware plus the filesystem size. In particular this means that 512Kb devices can now have the full featured web interface.

Here you can read a couple of posts about this procedure:

* [Optimizing files for SPIFFS with Gulp](http://tinkerman.cat/optimizing-files-for-spiffs-with-gulp/)
* [Embed your website in your ESP8266 firmware image](http://tinkerman.cat/embed-your-website-in-your-esp8266-firmware-image/)

## Web interface build process explanation

The build process consists of following tasks:

1. Inlining images: any reference to an image in the HTML or the CSS files is converted into the base64 representation of the image and inlined in the code.
1. Inlining scripts and stylesheets: CSS and JS files are cleaned and inlined in the same order they appear in the HTML file
1. Minifying contents: the HTML file (along with the inline scripts and styles) is minified, comments, spaces and line breaks are removed.
1. Compressing contents: everything is then compressed in a single GZIP file (same format the web servers use to send compressed content).
1. Embedding in program memory: the GZIP file is then encoded in a byte array as a PROGMEM constant, ready to be included and compiled within the firmware image.

## Web interface build process

All the tasks are managed by **[Gulp](http://gulpjs.com/)** (built on **[Node.js](https://nodejs.org/)**). Use the following links to find information about gulp and node:
* [Installing Node.js via package manager](https://nodejs.org/en/download/package-manager)
* [Download Node.js](https://nodejs.org/en/download/)
* [Getting Started - Gulp Documentation](https://gulpjs.org/getting-started)

Once you have node installed, go to the 'code' folder to install all the dependencies with:

```sh
npm install --only=dev
```

It will take a minute or two. Then you are ready to build the web interface files with:

```sh
node node_modules/gulp/bin/gulp.js
```
(if you are using ATOM-PlaformIO - you can install gulp-control package and manage web builds from within the SDK)

The resulting byte array will be embedded in 'code/espurna/static/index.html.gz.h'

## Custom vendor files

### PureCSS

The PureCSS file used in ESPurna are created using the [developer build script](https://github.com/pure-css/pure#build-from-source) but modifying the build script to remove unneeded media types.

**Note** this is not necessary unless you want to update the PureCSS files and reduce their default size.

```
index 7398e1f..a7f0b5b 100644
--- a/Gruntfile.js
+++ b/Gruntfile.js
@@ -212,10 +212,7 @@ grunt.initConfig({

             options: {
                 mediaQueries: {
-                    sm: 'screen and (min-width: 35.5em)',   // 568px
-                    md: 'screen and (min-width: 48em)',     // 768px
                     lg: 'screen and (min-width: 64em)',     // 1024px
-                    xl: 'screen and (min-width: 80em)'      // 1280px
                 }
             }
         }
```

See [PR 870](https://github.com/xoseperez/espurna/pull/870), thanks to [@mcspr](https://github.com/mcspr) and [@gn0st1c](https://github.com/gn0st1c) for this improvement.

## Troubleshooting

Some users have had issue with old versions of Node.js. Check you have at least 4.6.0. They have reported they had to install additional packages but that is still untested and I don't want to add things I'm not sure they are needed. Check issue [#147](https://github.com/xoseperez/espurna/issues/147)

## Flashing it

Once you have the 'code/espurna/static/index.html.gz.h' file, it is included from the 'code/espurna/web.ino' file and compiled with the firmware image. Read the sections related to building the firmware using [PlatformIO](PlatformIO) or [Arduino IDE](ArduinoIDE).
