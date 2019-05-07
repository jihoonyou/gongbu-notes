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
- You can also use a state container like Redux or Mobx to control your data flow. In that case you would use Redux or Mobx to modify your state rather than calling setState directly.

## 6. Style & Height and Width
- react native styles your app using JavaScript
- All of components accept a prop named style
- similar to CSS but using camelCase
- it is often cleaner to use StyleSheet.create to define several styles in one place
- height하고 width로 fixed하게 style할 수 있고, flex를 사용하여 copmonent의 available space를 dyanamic하게 style할 수 있다
- flex의 경우 보통 1로 설정하고, if the parent does not have dimensions, the children can't expand.

## 7. Layout with Flexbox
- use a combination of flexDirection, alignItems, and justifyContent
- similar to CSS on the web with a few exception. The defaults are different, with flexDirection defaulting to column instead of row, and the flex parameter only supporting a single number.
- flexDirection: component's style determines the primary axis of its layout
- justifyContent: Adding justifyContent to a component's style determines the distribution of children along the primary axis.
 - Available options are flex-start, center, flex-end, space-around, space-between and space-evenly
- alignItems: Adding alignItems to a component's style determines the alignment of children along the secondary axis
 - Available options are flex-start, center, flex-end, and stretch
 - flexDirection의 perpendicular느낌?

[flex practice][https://flexboxfroggy.com]
[grid practice][https://cssgridgarden.com]

## 8. Handling Text Input & Handling Touches
- TextInput is a basic component that allows the user to enter text. It has an onChangeText prop that takes a function to be called every time the text changed, and an onSubmitEditing prop that takes a function to be called when the text is submitted.
- Pressing the button will call the "onPress" function
- If the basic button doesn't look right for your app, you can build your own button using any of the "Touchable" components provided by React Native.
 - These components do not provide any default styling, however, so you will need to do a bit of work to get them looking nicely in your app.
   - you can use TouchableHighlight anywhere you would use a button or link on web. The view's background will be darkened when the user presses down on the button.
   - You may consider using TouchableNativeFeedback on Android to display ink surface reaction ripples that respond to the user's touch.
   - TouchableOpacity can be used to provide feedback by reducing the opacity of the button, allowing the background to be seen through while the user is pressing down.
   - If you need to handle a tap gesture but you don't want any feedback to be displayed, use TouchableWithoutFeedback.
   - In some cases, you may want to detect when a user presses and holds a view for a set amount of time. These long presses can be handled by passing a function to the onLongPress props of any of the "Touchable" components.

uncontrolled 
```
    //id="_username"
    ref={input => this._username = input}
```
- host platform manages it 
controlled
```
    onChnangeText={text => this.setState({username: text})}
```
- react controls it
## 9. Using a ScrollView
- a generic scrolling container that can host multiple components and views.
- ScrollViews can be configured to allow paging through views using swiping gestures by using the pagingEnabled props. 

## 10. Using List Views
use either FlatList or SectionList
- The FlatList 
 - component displays a scrolling list of changing, but similarly structured, data.(well for long lists of data, where the number of items might change over time)
 - only renders elements that are currently showing on the screen (not all elements at once)
 - The FlatList component requires two props: data and renderItem.
  - data is the source of information for the list. renderItem takes one item from the source and returns a formatted component to render.
- The SectionList
 - If you want to render a set of data broken into logical sections, maybe with section headers, similar to UITableViews on iOS, then a SectionList is the way to go.

## 11. Networking
Using Fetch
- React Native provides the Fetch API for your networking needs.
you may use XMLHttpRequest API or Websocket.



나중에 다시 참고
[resource][https://www.slideshare.net/deview/121react-native]