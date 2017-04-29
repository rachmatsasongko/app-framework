

## Development environment

### Text editor

You can use your favorite text editor, but we highly recommend *Atom*, because it is well-configurable, open source, available for Windows, macOS and Linux and supports Vue components syntax.

- Install [Atom](https://atom.io/) according your operating system
- ...



### Status bar style

You can configure the application status bar style in the *config.json* file:

```
statusbarVisibility: true,                               // true or false
statusbarTextColor: 'white',                             // 'black' or 'white'
statusbarBackgroundColor: '#3f51b5',                     // Hex color code
changeStatusbarBackgroundColorOnThemeColorChange: true   // true or false
```

You can modify the application status bar style in Vue hook `created` or later:

```
created: function () {
  this.$root.statusbarVisibility = true
  this.$root.statusbarTextColor = 'white'
  this.$root.statusbarBackgroundColor = '#3f51b5'
}
```

Limitations:

- Changing the status bar visibility is limited to native applications
- Changing the status bar text color is limited to iOS native applications
- Changing the status bar background color is limited to native or homescreen applications

### Global data object

App Framework provides a global data object, which will be restored immediately on each application reload and is accessible from all your Vue components with the hook `created` or later.

- To save data, use `this.$root.saveData(path, value)`
- To remove data, use `this.$root.removeData(path)`
- To retrieve data, use `this.$root.data.path`

The *path* must be a string, use a a point to nest data. Example:

```
created: function () {
  this.$root.saveData('greeting', 'Hello!')
  this.$root.saveData('names', {first: 'Jan', second: 'Tom', third: 'Sophie'})
  this.$root.removeData('names.second')
}
```

Now, the data object will look like following:

```
{
  greeting: 'Hallo',
  names: {
    first: 'Jan',
    third: 'Sophie'
  }
}
```

Example for the usage in templates:

```
<f7-block>
  <p>UTC date: {{$root.data.dateString}}</p>
  <f7-buttons>
    <f7-button @click="$root.saveData('dateString', (new Date()).toUTCString())">Update date</f7-button>
    <f7-button @click="$root.removeData('dateString')">Remove date</f7-button>
  </f7-buttons>
</f7-block>
```

Do not modify `$root.data` directly, because there wont be any update triggered.

## Firebase backend

App Framework is well-prepared to use [Firebase](https://firebase.google.com/) as a backend provider.

Configuration file:

```
firebase: {
  apiKey: "AIzaSyAvzTiqd9fKR-h4asdsadsadasd7Uxl4iXwqSMU1VjGdII",   // Leave blank to disable Firebase
  authDomain: "app-framework-9045a.firebaseapp.com",               // Leave blank to disable auth service
  databaseURL: "https://app-framework-9045a.firebaseio.com",       // Leave blank to disable database service
  storageBucket: "app-framework-9045a.appspot.com",                // Leave blank to disable storage service
  allowEmailLogin: true,                                           // true or false
  allowEmailRegistration: true                                     // true or false
}
```

Disabling a service will reduce the build size.

You can use Firebase in any Vue hook `created` or later:

- `window.firebase` - Firebase application instance
- `this.$root.user` -  Shortlink to `window.firebase.auth().currentUser`
- `this.$root.db(...)` - Shortlink to `window.firebase.database().ref(...)`
- `this.$root.store(...)` - Shortlink to `window.firebase.storage().ref(...)`

To test your Firebase rules in development, you have the chance to configure a second Firebase project:

```
devFirebase: {
  deployDevRulesOnTesting: false,
  apiKey: "AIzaSyBL0Xxsc-jFZ2BnmQV08T4O9B56HJVpwXk",
  authDomain: "dev-app-framework.firebaseapp.com",
  databaseURL: "https://dev-app-framework.firebaseio.com",
  storageBucket: "dev-app-framework.appspot.com",
  allowEmailLogin: true,
  allowEmailRegistration: true
}
```

If you set `deployDevRulesOnTesting: true`, on each test command (`npm run dev`, `npm run ios` and `npm run android`), the *database-rules.json* and *storage-rules.txt* files will be deployed to your second Firebase project.

## Overview - Project folder structure

The following project folder will be created by default.

```
├── app                         # App source folder
│   ├── images                  # App images
│   ├── pages                   # App page components
│   ├── app.vue                 # App main component
│   ├── config.js               # App configuration
│   ├── database-rules.json     # Firebase database rules
│   ├── icon.png                # App icon file (minimum size is 1024 pixel)
│   ├── routes.json             # App routes configuration
│   └── storage-rules.txt       # Firebase storage rules
├── build                       # Latest build files (do not modify)
├── design                      # Design templates (PDF, Power Point)
├── node_modules                # Installed node modules (do not modify)
├── snapshots                   # Project snapshots (for rollback)
├── .babelrc                    # Babel configuration file for ES2015 support
├── .gitignore                  # List of ignored files for Git commits
└── package.json                # Project information
```

## Overview - Configuration options

Configure your application easily in the `config.json` file.

Details are described in the corresponding chapters.

<!-- config-options -->
<!-- /config-options -->

---

> OLD DOCUMENTATION BELOW

## CLI commands

![Process](media/cli-commands.png)

This is an overview and reference, please see the Workflow for details.

- Setup
  - `npm install` to install App Framework and setup the project folder
    - `npm run reset-app` to replace the app folder with minimum files
  - `npm update` to update App Framework to the latest sub version

- Testing
  - `npm run dev` to start the development server in the web browser
    - `CTRL + C` to stop the development server
  - `npm run ios` to open Xcode with an iOS development build
  - `npm run android` to open Android Studio with a development build

- Building
  - `npm run patch` to build after bug-fixes and improvements
  - `npm run minor` to build after adding new functionality
  - `npm run major` to build after backward-capability breaking changes

- Deployment
  - `npm run firebase` to deploy rules and static files to Firebase
    - `npm run database` to deploy database rules to Firebase
    - `npm run storage` to deploy storage rules to Firebase
    - `npm run hosting` to deploy static files to Firebase
  - `npm run ftp` to deploy static files to your FTP server
  - `npm run xcode` to deploy static files as iOS Xcode project
  - `npm run studio` to deploy static files as Android Studio project

- Backup
  - `npm run backup` to create a snapshot of the Firebase database and user list
  - `npm run snapshot` to create a snapshot of your project folder

## Window objects

You can use several window objects directly from your components:

- `window._` - [Lodash](https://lodash.com/) library
- `window.Dom7` - [Dom7](http://framework7.io/docs/dom.html) library
- `window.f7` - [Framework7](http://framework7.io/docs/init-app.html) instance of your application
- `window.firebase` - [Firebase](https://firebase.google.com/docs/web/setup) instance (if configured)

## Vue root object

You can use the following information directly from the $root object of all your Vue components:

- `$root.appMode` - Run mode (native, homescreen, mobile, desktop)
- `$root.config` - Configuration (from config.json file)
- `$root.user` - Current user (null or object with uid, email, ...)
- `$root.language` - Current language (could be changed)
- `$root.theme` - Current theme (ios or material, could be changed)
- `$root.themeColor` - Current theme color ([list](http://framework7.io/docs/color-themes.html), could be changed)
- `$root.themeLayout` - Current theme layout ([list](http://framework7.io/docs/color-themes.html), could be changed)
- `$root.statusbarFont` - Current statusbar font style (default, lightContent, blackTranslucent or blackOpaque, could be changed)
- `$root.statusbarBackground` - Current statusbar background color (as HEX code, could be changed)
- `$root.statusbarDisplay` - Current statusbar visibility (true or false, could be changed)
- `$root.version` - Project version
- `$root.frameworkVersion` - App Framework version

## Global data object

To use data across your application, App Framework provides an easy to use global data object. The data object will be immediately restored after each application restart.

### Save data to the global data object

Use `saveData(item, value)` to save data directly from the template section.

```
<template>
  ...
  <f7-link @click="saveData('testItem.subItem', 'test data')">Click to save data</f7-link>
  ...
</template>
```

Use `this.saveData(item, value)` to save data in the component script section.

```
<script>
  module.exports = {
    ...
    methods: {
      ...
      anyMethod: function () {
        this.saveData('testItem.subItem', 'test data')
      }
      ...
    }
    ...
  }
</script>
```

### Remove data from the global data object

Use `removeData(item)` to remove data directly from the template section.

```
<template>
  ...
  <f7-link @click="removeData('testItem.subItem')">Click to remove data</f7-link>
  ...
</template>
```

Use `this.removeData(item)` to remove data in the component script section.

```
<script>
  module.exports = {
    ...
    methods: {
      ...
      anyMethod: function () {
        this.removeData('testItem.subItem')
      }
      ...
    }
    ...
  }
</script>
```

### Get data from the global data object

Use `data.item` to get data in the template section.

```
<template>
  ...
  <f7-block>Item value: {{data.testItem.subItem}}</f7-block>
  ...
</template>
```

Use `this.data.item` to get data in the component script section.

```
<script>
  module.exports = {
    ...
    methods: {
      ...
      anyMethod: function () {
        let itemData = this.data.testItem.subItem
      }
      ...
    }
    ...
  }
</script>
```

## State restoration

After an application switch or closure, the application state may be reset. This means, if your user changed the page or tab, scrolled, opened modals, put in some data before - everything will be gone.

App Framework has an automatic state restoration on each application restart, to let your users continue with the same application state they have had before they left the application.

This restoration includes the following elements:

- URL history per view
- Selected tabs (requires unique ID attribute per page)
- Scroll positions
- Side panels
- Action sheets (requires unique ID attribute)
- Login screens (requires unique ID attribute)
- Pickers (requires unique ID attribute)
- Popups (requires unique ID attribute)
- Form inputs data (requires unique form ID attribute)
- Focus on form input (requires unique NAME attributes per form)

The state is not restored for standard modals, popovers and code-generated modals.

## Statusbar modification

You can modify the statusbar in native and homescreen Apps from any component after its creation hook.

```
{
  created: function () {
    this.$root.statusbarTextColor = 'white'           // allowed are 'black' and 'white'
    this.$root.statusbarBackgroundColor = '#3f51b5'   // allowed are hex color codes
    this.$root.statusbarVisibility = true             // allowed are 'true' and 'false'
  }
}
```

Changing the text color is limited to native iOS Apps.

## Hooks

### Window hooks

- `window._` - [Underscore.js](http://underscorejs.org/) library
- `window.firebase` - Firebase instance
- `window.$$` - Framework7 Dom7 instance
- `window.f7` - Framework7 instance

## Workflow

### Setup your development environment

You can use your favorite code editor. But we recommend [Atom](https://atom.io/), an open source code editor.

1. Install [Atom](https://atom.io/)
2. Open Atom preferences > Packages page
3. Search for *language-vue-component* and install the package for correct syntax highlighting

### Install App Framework

1. Install [Node.js with npm](https://docs.npmjs.com/getting-started/what-is-npm)
2. Create a **package.json** file in an empty project folder with the following content:

   ```
   {
     "name": "my-app",
     "version": "1.0.0",
     "devDependencies": {
       "app-framework": "*"
     }
   }
   ```

3. Run `npm install` to install App Framework and setup the project folder
4. Run `npm run dev` to start the Demo App at localhost:8080

Right after the installation, you can run `npm run reset-app` to reduce the *app* folder to a minium set of files. Use this if you know Framework7 / Framework7-Vue well and could start with an empty app folder. However, a snapshot will be created before the reset automatically to to *snapshots* folder.

Run `npm update` to update App Framework to latest sub version. A snapshot of your project folder will be created before in folder *snapshots*.

### Design your application
- Use our printable [smartphone template](design/smartphone-template.pdf) to sketch your application
- Use our icon template as [PDF to sketch](design/icon-template.pdf) and [PPTX to draw](design/icon-template.pptx) your application icon

### Develop your application

- Update the configuration in *app/config.json* file - first of all for Firebase!
- Run `npm run dev` to start the development server at localhost:8080
- Save images to *app/images* folder
- Edit the app component in *app/app.vue* file
- Edit page components in *app/pages* folder
  - After adding, removing or renaming pages you have to run `npm run dev` again!
  - Study the code of the Demo App pages to learn how to realize things in App Framework
- Edit your [database rules](https://firebase.google.com/docs/database/security/quickstart) in *app/database-rules.json* file
- Edit your [storage rules](https://firebase.google.com/docs/storage/security/) in *app/storage-rules.txt* file
- Add Cordova / PhoneGap plugins easily in the *config.json* file with property *useCordovaPlugins*

### Test your application

- Run `npm run dev` to start the development server in the web browser
  - `CTRL + C` to stop the development server
- Run `npm run ios` to open an iOS simulator with a development build
- Run `npm run android` to open an Android emulator with a development build

  Confirm Gradle sync and removal of older application installations if asked.

  If you get an error *Failed to find 'JAVA_HOME' environment variable. Try setting setting it manually.* you have to install the Java SE SDK first.

App Framework fix your code automatically on each test or build command. To disable this behavior, you can set the config parameter *fixCodeOnBuild* to false. If some findings could not be fixed automatically, they will be logged to *code-findings.log*.

If *dev-firebase* is configured in *config.json* file, on each test command, the Firebase database and storage rules are deployed automatically.

### Build your application

Each build command will update the *build* folder on success.

- Run `npm run patch` after bugfixes and improvements
- Run `npm run minor` after adding new functionality
- Run `npm run major` after breaking backward-capability

### Deploy your application

*App Framework* does many adjustments in the background to enable you to deploy your App easily as Web App or as native App. So you could start fast and become professional later on without any change. But what are the differences?

| &nbsp; |Web App|Native App|
|---|---|---|
|Installation|Are running in the device browser and could be pinned to the homescreen.|Are installed from an App Store or manually to the device (Android only).|
|Performance|Reload on reopen, but could be cached for offline usage. Offline warning.|Kept in runtime of the device, smoother usage. No offline warning.|
|Capability|Only browser features.|Access to the device hardware and OS features.|
|Deployment|In seconds.|Additional native build plus approval process, which takes some time and could be refused at the Apple App Store.|
|Costs|Firebase hosting service is free for small apps.|Apple requires developer program (around 99€ per year), Google Play store requires registration fee (around 25 USD once). For selling apps, Apple and Google charge around 30% of the sales.|
|Promotion|All regular ways.|All regular ways plus special promotions and user ratings in the store.|

Deployment to a FTP server (Web App)

- Run `npm run ftp` to deploy your latest build to your FTP server, on first call, the config file *ftp-config.json* is created automatically and you have to update it with your FTP server data
- For rollback, run `npm run ftp -- --version x.y.z`

Deployment to [Firebase Hosting](https://firebase.google.com/docs/hosting/) (Web App)

- Run `npm run firebase` to deploy your latest build, database rules and storage rules to Firebase
- Run `npm run database` to deploy your latest build database rules to Firebase
- Run `npm run storage` to deploy your latest build storage rules to Firebase
- Run `npm run hosting` to deploy your latest build static files to Firebase
- For rollback, run all the commands above and extend with ` -- --version x.y.z` or use the Firebase Console

Deployment to the Apple App Store (native App)

- You need a Mac with [macOS](http://www.apple.com/de/macos/) and installed [Xcode](https://developer.apple.com/xcode/) (free)
- You need to sign to the [Apple developer program](https://developer.apple.com/programs/) (around 99€ per year)
- Create a production certificate in iTunes Connect, download and install it on your Mac
- Create a distribution provisioning profile in iTunes Connect, download and install it on your Mac
- You need to prepare the publishing in [iTunes Connect](https://itunesconnect.apple.com/)
- Run `npm run xcode` to create a project file for Xcode, based on [Cordova](https://cordova.apache.org/)
- Make screenshots on the biggest iPhone (you will need them in iTunes Connect later on)
- Deactivate automatic managed signing, select your certificate and provisioning profiles created before
- Select the Generic iOS Device
- Create an archive (Product > Archive) of the Xcode project and upload it to iTunes Connect
- Send your App in iTunes Connect for the review to Apple
- For rollback, run `npm run xcode -- --version x.y.z` or use iTunes Connect

Deployment to the Google Play Store (native App)

- You need to install the [Android Studio](https://developer.android.com/studio/)
- You need to register at the [Google Play Developer Console](https://play.google.com/apps/publish/signup/) (around 25 USD once)
- Run `npm run studio` to create a project file for Android Studio, based on [Cordova](https://cordova.apache.org/)
- Select your project and confirm Gradle sync
- Make screenshots, you will need them later in the Google Play Developer Console
- Generate signed APK
- Log in to the Google Play Developer console to deploy your application
- For rollback, run `npm run studio -- --version x.y.z` or use the Google Play Developer Console

### Backup your application

- Run `npm run backup` to save the Firebase database content and user list as JSON to the *snapshots* folder
- Run `npm run snapshot` to create a snapshot of all important project files to the *snapshots* folder
- Backup your project folder frequently by
  - Copying the *snapshots* folder to any external drive or cloud
  - *and/or* pushing and synchronizing your changes to GitHub