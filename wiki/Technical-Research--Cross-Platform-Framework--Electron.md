# [Electron](https://www.electronjs.org/)

an Electron application is essentially a Node.js application
[Quick-start](https://www.electronjs.org/docs/tutorial/quick-start)

## Electron with React

Built a React application following this [tutorial](https://reactjs.org/tutorial/tutorial.html#setup-option-2-local-development-environment).

Then built Electron into the application, following this [article](https://www.freecodecamp.org/news/building-an-electron-application-with-create-react-app-97945861647c/)

This worked and the application could be started in the web browser as well as in a desktop window on Windows through Electron. This has some implications though: The desktop application requires building the React web application first. So you have to issue 'npm start' and 'npm run electron' in this order in two separate terminals. We have to see how this will effect creating a deployment and not just using it for development purposes. After all this is just a quick and dirty solution and there seem to be other solutions or workarounds that might fix the named issues.

## Project integration
Electron provides different packages for deployment and packaging, projects needs tbd.


