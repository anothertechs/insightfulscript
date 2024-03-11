---
title: React Native WebView Starter Guid
date: 2021-10-28
published: true
author: Hatim
keywords: react,native,webview,tutorial,install,originwhitelist,html,plugin,component
description: React Native WebView presents web information in a native view, and it comes with a variety of tricks and features to help you get the most out of it.
Tags: ["programming","react native"]
image: /images/react-native-webview.png
---

WebViews in React Native allow access to any online site from within the mobile app.

In a React Native project, the WebView component is used to load webpages.
It used to be included in React Native out of the box, but it has since been removed from the core and added to the [React Native Community libraries](https://github.com/react-native-community); for additional information, see The [Slimmening proposal](https://github.com/react-native-community/discussions-and-proposals/issues/6).

### Requirements

The requirements to follow this tutorial are:

- Nodejs >=8.x.x with npm or yarn installed as a package manager.
- react-native-cli.

## React Native WebView: Getting Started

To get started with web view setup, we must first install the plugin itself.
We're going to use NPM(Node Package Manager) to install the plugin, although we could also use yarn.
As a result, we must perform the following command in the command prompt of our project folder in order to install the plugin:

```bash
npm install --save react-native-webview #for npm

yarn add react-native-webview # for yarn
```

After that, connect the dependencies.Auto-linking will handle the linking procedure starting with react-native 0.60, but don't forget to execute pod install beforehand.

Native Objective-C, Swift, Java, or Kotlin code in React Native modules must be "linked" so that the compiler knows to include it in the app.

Run the following command to link it:

```bash
 react-native link react-native-webview
```

### For IOS

Run the following command if you're using CocoaPods in the ios/ directory:

```bash
pod install
```

### For Android

Make sure AndroidX is enabled in your project if you're using react-native-webview version 6.X.X by editing `android/gradle.properties` and adding the two lines below:

```
android.useAndroidX=true
android.enableJetifier=true
```

I hope you were able to install it successfully.
Please refer to the [official installation](https://github.com/react-native-community/react-native-webview/blob/master/docs/Getting-Started.md) guide if you get stuck.

Now I'll show you various relevant WebView examples, ranging from simple to complicated, as well as some how-tos.

## Quickstart with WebView in its most basic form

```js
import React, { Component } from "react";
import { WebView } from "react-native-webview";
class MyWebView extends Component {
  render() {
    return (
      <WebView
        style={{ marginTop: 35 }}
        source={{ html: "<h1>Another Techs,Welcomes you</h1>" }}
      />
    );
  }
}
```

We've used the `react-native-webview` plugin to import the `WebView` component.
Now, as demonstrated in the code sample above, we can utilise this component to load the HTML content.

The `MyWebView` class component has been defined.
The `render()` function in this class component renders the WebView component.The HTML content for the WebView component is set to its source prop.

## Loading Remote URL

```js
import React, { Component } from "react";
import { WebView } from "react-native-webview";

class MyWebView extends Component {
  render() {
    return (
      <WebView
        source={{ uri: "https://anothertechs.com/" }}
        style={{ marginTop: 35 }}
      />
    );
  }
}
```

The content is obtained using the `source` attribute, which might be a URL or HTML.You must pass an object with the field uri to load a webpage by its URL, as demonstrated below:

```js
<WebView source={{ uri: "https://anothertechs.com" }} />
```

## `originWhitelist` property in WebView

The origin where users can navigate in your WebView is controlled by the `originWhitelist` attribute.
The default whitelisted origins are `http://` and `https://`, and it accepts an array of strings.

For example, if you want to make sure that users can only go to URIs that start with `https://` or `git://`, you'd do it this way:

```js
<WebView
	originWhitelist={['https://*', 'git://*']
  source={{ uri: 'https://anothertechs.com/' }}
  }
/>
```

## React Native Webview with a loading spinner

It may take some time for the complete HTML content on the page to load when using the WebView component to browse the URL.
As a result, until the website loads, we'll show a loading indication to illustrate the delay. As demonstrated in the code sample below, we need to import the `ActivityIndicator` component from the react-native package for this:

```js
import { Text, View, StyleSheet, ActivityIndicator } from "react-native";
```

```js
import * as React from "react";
import { Text, View, StyleSheet, ActivityIndicator } from "react-native";
import { WebView } from "react-native-webview";

function Loading() {
  return <ActivityIndicator color="#009b88" size="large" />;
}
export default function App() {
  return (
    <WebView
      originWhitelist={["*"]}
      source={{ uri: "https://anothertechs.com/programming" }}
      renderLoading={this.Loading}
      startInLoadingState={true}
    />
  );
}
```

We've used the `AcitivityIndicator` with colour and size props in this example.Then we called the `Loading` function from the WebView component's `renderLoading` prop.This enables us to keep the loading indication visible until the webpage is completely loaded.
The `startInLoadingState` attribute is also used in this case.
On the first load, this boolean value compels the WebView to show the loading view.In order for the `renderLoading` prop to work, this prop must be set to true.

## Wrapping Up

We learned about React Native's web view property in this tutorial.
Because React Native's built-in web-view feature is being phased out, we learned how to use the `react-native-webview` third-party web view plugin.First, we learnt how to use the WebView component to render simple HTML content.Then we got a step-by-step tutorial on how to use the WebView component and its props to render the whole HTML content from the URL, including the loading indication.If you want to learn more about this web view plugin, head over to the [main repository's](https://github.com/react-native-webview/react-native-webview) discussion thread.
