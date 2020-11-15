# [Expo](https://expo.io/)
Make any app. Run it everywhere. Build one project that runs natively on all your users' devices.

## Overview
Expo is a framework and a platform for universal React applications. It is a set of tools and services built around React Native and native platforms that help you develop, build, deploy, and quickly iterate on iOS, Android, and web apps from the same JavaScript/TypeScript codebase.

Free and Open Source

Docs: https://docs.expo.io/

Tries to manage as much as possible for building react native apps and lets you focus on just developing it.

It's a "bare" native project with React Native and one or more packages from the Expo SDK installed. Anything that you can do in a native project is possible here.

Based on React and React Native. Uses React Native Web for web app deploy.

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
