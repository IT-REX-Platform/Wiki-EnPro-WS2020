# Cross Platform Framework
Suggestion: Expo with bare workflow

Pros:
- Monorepo, Variation through file endings. e.g. index.ios.js, index.web.js. etc.
- Good documentation
- Support of native platform features
- Free and Open Source
- Performant apps due to underlying React Native
- Project deployable to native dev environments (Android studio, xcode)

Cons:
- Desktop app probably harder to implement

Why?
- expo over react native
  - lower effort for monorepo codebase
  - react native web already integrated
- expo over ionic
  - native look and feel on mobile devices
  - faster, no ressource overhead for web tech on mobile devices

Development strategy:
- in case of dev issues -> carry-over to pure react native possible
- try to minimize dependencies on expo specific implementations
- separate business logic in specific components (UI independent)
- etc. 


# Notes
## Which OS / Browser should be supported
* Mobile Apps (iOS / Android) (1)
* Browser (1)
  * Chromium/Chrome (1)
  * Firefox (1)
  * Safari (1)
  * Edge (2)
  * Opera  (3)
  * Brave (3)
* Desktop (2)
  * Windows
  * Linux
  * MacOS

(1): Must have , (2): Optional , (3): Nice to have

## Prototypes
React native: Slawa, Dani
Expo: Marcel
Ionic: Christian
Electron: Benedikt

### Expected result

* Hello World-App
* Deploy to target


# Frontend FrameWorks

# Cross Platform Frameworks

| Framework               | IDE                               | Language                   | Frameworks            | Runtime                                                 | Targets                                       | Launched | Pros       | Cons |
|-------------------------|-----------------------------------|----------------------------|-----------------------|---------------------------------------------------------|-----------------------------------------------|----------|------------|------| 
| Ionic                   | VS-Code, Atom, WebStorm           | HTML, CSS, JavaScript (TS) | React, VueJs, Angular | Full screen Web browser                                 | Android, iOS, Web/PWA Desktop (electron)      | 2013     |            |      | [Ionic](https://ionicframework.com/) 
| Flutter (Google)        | Android Studio, VS-Code, IntelliJ | Dart                       |                       | custom graphics engine Skia (own library of UI Widgets) | Android, iOS, Desktop (alpha), Web app (beta) | 2017     | Perormance | New  | [Flutter](https://flutter.dev/)
| React Native (Facebook) | Atom, VS Code, WebStorm           | JavaScript                 | React                 | Copmiled to native UI components                        | Android, iOS, Web                             | 2015     |            |      | [React native](https://reactnative.dev/)
| Expo                    |                                   | JavaScript                 | React                 |                                                         | Android, iOS, Web                             | 2015     |            |      | [Expo](https://expo.io/)
| Xamarin (Microsoft)     | Visual Studio/Xamarin Studio      | C#                         | .Net                  |                                                         | Android, iOS, Desktop                         |          |            |      |

## Ionic vs Flutter

https://ionicframework.com/resources/articles/ionic-vs-flutter-comparison-guide 

##  Cross-platform mobile frameworks used by software developers worldwide in 2019 and 2020 

![Cross-platform mobile frameworks used by software developers worldwide in 2019 and 2020](./Images/statistic_id869224_cross-platform-mobile-frameworks-used-by-developers-worldwide-2019-and-2020.png)

https://www.statista.com/statistics/869224/worldwide-software-developer-working-hours/

## Web Frameworks

### VueJs
### AngularJs
### React
