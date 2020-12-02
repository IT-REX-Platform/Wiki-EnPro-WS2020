# [Expo](https://expo.io/)
Make any app. Run it everywhere. Build one project that runs natively on all your users' devices.

## Overview
Expo is a framework and a platform for universal React applications. It is a set of tools and services built around React Native and native platforms that help you develop, build, deploy, and quickly iterate on iOS, Android, and web apps from the same JavaScript/TypeScript codebase.

Free and Open Source

Docs: https://docs.expo.io/

Tries to manage as much as possible for building react native apps and lets you focus on just developing it.

It's a "bare" native project with React Native and one or more packages from the Expo SDK installed. Anything that you can do in a native project is possible here.

Based on React and React Native. Uses React Native Web for web app deploy.

## Helpful links
[React Native Guy on Youtube](https://www.youtube.com/c/wcandillon/featured)
<br>
[React Native Guy#2 on Youtube](https://www.youtube.com/c/CatalinMironDev/featured)


### Limitations of the managed workflow

- Not all iOS and Android APIs are available
- The SDK doesn't support all types of background code execution
- If you need to keep your app size extremely lean, the managed workflow may not be the best choice
- Native libraries to integrate with proprietary services are usually not included in the SDK
- The only supported push notification service is the Expo notification service
- The minimum supported OS versions are Android 5+ and iOS 10+
- Free builds can sometimes be queued
- Updates (JS and assets) for OTA updates and builds are size-limited
- Your app cannot target only children under 13 years old.

### Limitations of the bare workflow

- Build service only works in the managed workflow
- Configuration must be done on each native project rather than once with app.json

As you can see, the only disadvantage of bare workflow is that you have to configure more yourself.
We can also integrate native components, written in Android/Kotlin and Swift. (With the managed workflow we are limited to expo-packages)

[Doku](https://docs.expo.io/introduction/why-not-expo/)


## Using Bare Workflow

( Based on the offcial documentation [Doku](https://docs.expo.io/bare/exploring-bare-workflow/) ) 

Make sure you have setup you local environment using this guide [Environment-Setup](https://reactnative.dev/docs/environment-setup)


If you are using the bare workflow ios and android projects located in their own sub-folders.
It is possible to work on these projects with Android Studio or Xcode.




There are several posibilities to run/compile the different targets.

## Prerequisites

- https://nodejs.org/en/download/current/ (important: current and not LTS)

- Install expo `npm install -g expo-cli`
- Create new app `expo init MyCoolApp`
  * Use bare workflow -> minimal (TypeScript)


## Run / Debug / Deploy

### Android

#### Debug mode (With hot-reload)

Run your local dev server:

```
npx react-native start
```

Then compile and deploy to the emulator:
```
npm run android
```

#### Release mode

Go into the android subfolder an execute.
```
./gradlew assembleRelease
```

If you run into an error like `java.lang.NoClassDefFoundError: Could not initialize class org.codehaus.groovy.vmplugin.v7.Java7`

Change the used gradle-version from 6.2 to 6.3 in `android/gradle/wrapper/gradle-wrapper.properties`.

If the build succeeded you can deploy the app via adb `adb install ./app/build/outputs/apk/release/app-release.apk`.
(if you have multiple android devices running, use the `-s <DEVICE-NANE>` parameter to select the correct one)

Liste the connected devices `adb devices`

### iOS

#### Debug

```
npm run ios
```

### web

#### Debug

```
npm run web
```

#### Deploy

`expo build:web`

The target is now placed in the `web-build` subfolder

If you want to test the binaries you can use the npm package `serve`.

- Install serve via `npm install -g serve`
- run serve via `serve -s web-build`


### Android/Web/iOS Debug mode via Expo developer tools

```bash
expo start
```

### Video example

- `expo install expo-av`

Add the following lines after `<Text>...</Text>`

```
<Video
  source={{ uri: 'https://d23dyxeqlo5psv.cloudfront.net/big_buck_bunny.mp4' }}
  rate={1.0}
  volume={1.0}
  isMuted={false}
  resizeMode="cover"
  shouldPlay
  useNativeControls={true}
  style={{ width: 300, height: 300 }}
/>
```



### Troubleshooting

#### build abort: w: Detected multiple Kotlin daemon sessions at build/kotlin/sessions

Try again ;)


## Developer services

There is an option to pay for Expo to get "Prioritized build infrastructure" and "Team features". This [blogpost](https://medium.com/@ji/hi-im-one-of-the-co-founders-of-expo-and-have-worked-on-it-for-several-years-and-have-the-context-a85810f373b9) sums this up a bit.

The gist is, that you can either use Expo with their managed workflow (which enables among others automatic builds or OTA updates) or with the bare workflow (where you have to build and supply your services on your own). Paying for Expo gives you prioritized builds when using the managed workflow. Furthermore it allows to showcase apps to other team members (https://forums.expo.io/t/documentation-about-features-teams-in-paid-plan-is-not-so-clear/31225). I couldn't find more about the paid plan, it is very poorly documented.

We would definitely use the bare workflow and do not want to rely on their managed services. Therefore the paid plan is not of interest here.

## Bare Workflow
https://docs.expo.io/introduction/managed-vs-bare/

### Differences between managed and bare workflow:
| Feature | Managed | Bare |
|---------|---------|------|
| Develop apps with only JavaScript/TypeScript | ✅	| |
| Use Expo build service to create your iOS and Android builds | ✅	| ⏱ (in progress) |
| Use Expo's push notification service | ✅	| ✅ |
| Use Expo's over the air updates features |	✅ |	✅ |
| Develop with the Expo client app |	✅ |	✅ (if you follow guidlines) |
| Access to Expo SDK	| ✅ |	✅ |
| Add custom native code and manage native dependencies	| |	✅ |
| Develop in Xcode and Android Studio	| |	✅ |

When starting with the managed workflow you can "eject" at any time and your project will just be a typical native project with the React Native and Expo SDK packages that your app is using installed and configured.

Building the iOS SDK requires a MacOS operating system (use pc pool of university).

## Difference of Expo to React Native
Managed solution for React Native which also includes React Nativ Web.

https://adhithiravi.medium.com/building-react-native-apps-expo-or-not-d49770d1f5b8

Pros:
* faster way to build react native apps (because many things are managed)
* don't need to use native Android or iOS code which is sometimes required with React Native (essentially a wrapper around the native iOS and Android components)
* You don't need Xcode or Android Studio
* OTA updates (publish over the air): you can update the app without publishing a new version to the app store
* integrates native APIs out of the box (camera, file system, location, push notifications)

Cons:
* additional layer of abstraction, black box -> may be a good thing for us since we are rather inexperienced
* Not all iOS and Android APIs are available yet (bluetooth, in-app purchases)

If we would start with Expo but then want to switch to React Native this is possible but we would have to:
* rewrite push notification code
* refactor code to use other libraries that are not a part of Expo ecosystem
* do navigation changes and general code refactoring
