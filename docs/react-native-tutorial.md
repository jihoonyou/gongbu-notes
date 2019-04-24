# react-native-tutorial

## 1. Introduction

way to write cross-platform applications on JavaScript
- React Native is like React, but it uses native components instead of web components as building blocks.
- Android and iOS
- not suitable for develpoing high end performance like games

## 2. Setting up React Native
getting strated (https://facebook.github.io/react-native/docs/getting-started)
- npm install -g react-native-cli or npm install -g expo-cli
- expo를 사용하면, 제약이 많은듯..?
- react-native init (AwesomeProject) or expo init (AwesomeProject)
- install Java SDK & Android Studio
- Configure the ANDROID_HOME environment variable
- If you use Android Studio to open ./AwesomeProject/android, you can see the list of available Android Virtual Devices (AVDs) by opening the "AVD Manager" from within Android Studio.
- run AVD and react-native run-android

## 3. File Structure
android
- consist files which used to build the application for android platform
ios
- consist files which used to build the application for ios platform
node_modules
.babelrc
- preset to react native
buckconfig
flowconfig
.git(default)
App.js
- App 그려지는 곳
app.json
- name
index.js
- which bootstrap your application (this is the first file that react native enters)
package.json
- dependencies

## 4. Hello World
in android folder
- local.properties (determine corresponding OS)
- react-native run-android (virtual)
- react-native run-ios --simulator="iPhone 8 Plus" (Mac OS)

Using a virtual device
- If you use Android Studio to open ./AwesomeProject/android, you can see the list of available Android Virtual Devices (AVDs) by opening the "AVD Manager" from within Android Studio. Look for an icon that looks like this:

how does the program work?
- entry -> index.js
- index.js includes App.js
- Platform => which is used to differentiate b/w different kind of platforms
- StyleSheet => CSS (mostly flexbox)
- Text => render your text (used to display text)
- View => container copmonent (template)
- A View is useful as a container for other components, to help control style and layout.
- JSX
- render() => gets the view template of the particular component and displays it on the screen
- const styles => applying styles 

## 5. Props & State
There are two types of data that control a component: props and state. props are set by the parent and they are fixed throughout the lifetime of a component. For data that is going to change, we have to use state.

Props
- in JSX {{}} curly brace needed 
- Most components can be customized when they are created, with different parameters. These creation parameters are called props.

State
- initialize state in the constructor, and then call setState when you want to change it.
- set state when you have new data from the server, or from user input.
- . You can also use a state container like Redux or Mobx to control your data flow. In that case you would use Redux or Mobx to modify your state rather than calling setState directly.
- 


