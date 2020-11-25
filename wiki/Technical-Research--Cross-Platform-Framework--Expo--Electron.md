- [Introduction](#introduction)
- [Setup](#setup)
- [The caveat](#the-caveat)
- [Debugging](#debugging)
- [Building](#building)

## Introduction

Expos Electron support is still experimental and is going to change in the future.
Additionally building a video player with Expo and deploying it to Electron is not so straight forward as the documentation makes it out to be.

## Setup

``` bash
expo init <NAME> --npm
```

This creates an Expo project with *npm* as a package manager instead of *yarn*.

``` bash
cd <NAME>
npm i --save-dev @expo/electron-adapter electron-builder
```

This adds the *@expo/electron-adapter* and the *electron-builder*. The latter is used for the actual build process.

``` bash
npx expo-electron
```

This does the following:

- Append electron generated files to the *.gitignore*
- Install the required dependencies: *electron*, *@expo/webpack-config*, *react-native-web*, etc...
- Create a new electron-webpack config file *electron-webpack.js*

``` javascript
const { withExpoAdapter } = require('@expo/electron-adapter');

module.exports = withExpoAdapter({
  projectRoot: __dirname,
  // Provide any overrides for electron-webpack: https://github.com/electron-userland/electron-webpack/blob/master/docs/en/configuration.md
});
```

## The caveat

To get an electron application that starts the following has to be added to the *package.json*

``` json
"name": "videoapp", // application name
  "version": "1.0.0", // a version
  "build": {  // I must admit that I don't have a clue what that does but it's necessary.
    "extraMetadata": {
      "main": "main.js"
    },
    "files": [
      {
        "from": "dist/main/",
        "to": "./",
        "filter": [
          "**/*"
        ]
      },
      {
        "from": "dist/renderer",
        "to": "./",
        "filter": [
          "**/*"
        ]
      },
      "package.json",
      "**/node_modules/**/*"
    ]
  }
```

While this was already enough to build a player that loads the video from the web, for local files it's a bit more complicated.

In the local case the video player has to be initialized in the following way:

``` typescript
import {unpackAsset} from "./unpackAsset";

...

<Video
  source={unpackAsset(require('../assets/video.mp4'))}
  rate={1.0}
  volume={1.0}
  isMuted={false}
  resizeMode="cover"
  shouldPlay
  useNativeControls={true}
  style={{width: "100%", height: "100%"}}
/>
```

While using just *require()* to load the asset on the web and on mobile plattforms is enough to get it to work, on Electron this function call has to be wrapped in *unpackAsset()*. This function looks the following way:

*unpackAsset.electron.ts*

``` typescript
export const unpackAsset = (asset: any) => {
  return asset.default;
}
```

*unpackAsset.ts*

``` typescript
export const unpackAsset = (asset: any) => {
  return asset;
}
```

The correct function is choosen during the build process by naming the files this way.

## Debugging

Running the debug build with hot reload is done the following way:

``` shell
npx expo-electron start
```

## Building

At the moment the project can't be build with the *@expo/electron-adapter*. Instead of that the *electron-builder* is used by invoking the following command:

``` shell
npx electron-webpack && npx electron-builder --dir -c.compression=store -c.mac.identity=null
```

"*-c.compression=store* speeds the builds up a lot, delete this for actual production builds."
