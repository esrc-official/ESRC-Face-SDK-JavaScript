# ESRC Face SDK for JavaScript

[![Platform](https://img.shields.io/badge/platform-JAVASCRIPT-orange.svg)](https://github.com/esrc-official/ESRC-Face-SDK-JavaScript)
[![Languages](https://img.shields.io/badge/language-JAVASCRIPT-orange.svg)](https://github.com/esrc-official/ESRC-Face-SDK-JavaScript)
[![Commercial License](https://img.shields.io/badge/License-Commercial-brightgreen.svg)](https://github.com/esrc-official/ESRC-Face-SDK-JavaScript/blob/master/LICENSE.md)

## Table of contents

  1. [About ESRC Face SDK](#about-esrc-face-sdk)
  1. [Install ESRC Face SDK](#install-esrc-face-sdk)
  1. [Making your first recognition](#making-your-first-recognition)

<br />

## About ESRC Face SDK

Through our **ESRC Face SDK** for JavaScript, you can efficiently integrate real-time recognition of facial expression into your web app. This and other pages in the Getting Started provide the ESRC Face SDK’s structure and installation steps, then goes through the preliminary steps of implementing the ESRC Face SDK in your own project.

<!-- ### Supported browsers

| Browser|Supported versions|
| :---: | :--- |
| Internet Explorer | 10 or higher |
| Edge | 13 or higher |
| Chrome | 16 or higher |
| Firefox | 11 or higher |
| Safari | 7 or higher |
| Opera | 12.1 or higher |
| iOS Safari | 7 or higher |
| Android Browser | 4.4 (Kitkat) or higher |  -->

### Key functions

|Function|Description|
|---|---|
|Measurement Environment Analysis| Analyze measurement environment including brightness. |
|Face Detection| Detect a single face using a front camera on mobile. |
|Facial Landmark Detection| Detect x and y coordinates of 68 facial landmarks in 2D space from the detected face. |
|Facial Action Unit Analysis| Extract centroid, area, theta and R distance of each 39 facial action unit from the detected 68 facial landmarks based on Facial Action Coding System determined by Paul Ekman. |
|Basic Facial Expression Recognition| Recognize 7 facial expressions consist of neutral, happiness, sadness, surprise, anger, disgust and fear based on 6 basic emotions. |
|Valence Facial Expression Recognition| Recognize 3 facial expressions consist of neutral, positive and negative based on valence of two-dimensional emotion. |


### Try the sample app

Our sample app has the core features of the ESRC Face SDK. Download the app from our [GitHub repository](https://github.com/esrc-official/ESRC-Face-JavaScript) to get an idea of what you can build with the actual SDK and start building in your project.

> Note: The fastest way to see our ESRC Face SDK in action is to build your app on top of our sample app. Make sure to change the application ID of the sample app to your own.


## Install ESRC Face SDK

This page provides a step-by-step guide that demonstrates how to build and configure an in-app face analysis using the ESRC Face SDK.

### Step 1: Download and install the ESRC Face SDK

If you're familiar with using external libraries or SDKs, installing the ESRC Face SDK is simple. You can install the ESRC Face SDK with package manager `npm` by entering the command below on the command line.

- **Npm**

> Node: To use npm to install the ESRC Face SDK, Node.js must be first installed on your system.

```bash
$ npm install @esrc/face (request to npm server)
```

Install via `Npm` and import like below in your `JavaScript` file.

```javascript
// Define a global variable 'Module' with a method 'onLoadedESRC'
Module = {
    onLoadedESRC() {
        // do somthing...
    }
}
// Load '@esrc/face' assinging the value to the global variable 'ESRC'
require("@esrc/face");
```

### Step 2: Download and install the assets

Download the `assets` file from our [GitHub repository](https://github.com/esrc-official/ESRC-Face-SDK-JavaScript/tree/master/assets). Copy the downloaded assets file into your project directory.

## Making your first recognition

The ESRC Face SDK simplifies vision features into an effortless and straightforward process. To recognize your facial expression, do the following steps:

This page provides a step-by-step guide that demonstrates how to build and configure an in-app face analysis using ESRC Face SDK. License key can be received by requesting by the email: **esrc@esrc.co.kr**.

### Step 1: Initialize the ESRC Face SDK

Initialization binds the ESRC Face SDK to JavaScript, thereby allowing it to use a camera in your mobile. To the `initWithApplicationId()` method, pass the **App ID** of your ESRC application to initialize the ESRC Face SDK and the **ESRCLicenseHandler** to received callback for validation of the App ID.

```javascript
// Initialize ESRC
ESRC.initWithApplicationId("APP_ID", (isValid) => {
    if (isValid) {
        // Application ID is valid, so do somthing...
    } 
});
```

> Note: The `ESRC.initWithApplicationId()` method must be called once across your web app. It is recommended to initialize the ESRC Face SDK in the `onLoadedESRC()` method of the Application instance.

### Step 2: Start the ESRC Face SDK

Start the ESRC Face SDK to recognize your facial expression. To the `start()` method, pass the `ESRCProperty` to select analysis modules and the `ESRCHandler` to handle the results. You should implement the callback method of `ESRCHandler` interface. So, you can receive the results of face, facial landmark, facial action unit and facial expression. Please refer to **[sample app](https://github.com/esrc-official/ESRC-Face-JavaScript)**.

```javascript
// Initialize property
var property = new ESRCType.ESRCProperty(
    true,  // Whether analyze measurement environment or not.
    true,  // Whether detect face or not.
    true,  // Whether detect facial landmark or not. If enableFace is false, it is also automatically set to false.
    true,  // Whether analyze facial action unit or not. If enableFace or enableFacialLandmark is false, it is also automatically set to false.
    true,  // Whether recognize basic facial expression or not. If enableFace is false, it is also automatically set to false.
    true  // Whether recognize valence facial expression or not. If enableFace is false, it is also automatically set to false.
);

// Initialize handler
var handler = new ESRCHandler();
handler.onAnalyzeMeasureEnv = function(measureEnv) {
    // do something...
}
handler.onDetectedFace = function(face) {
    // do something...
}
handler.onDetectedFacialLandmark = function(facialLandmark) {
    // do something...
}
handler.onAnalyzedFacialActionUnit = function(facialActionUnit) {
    // do something...
}
handler.onRecognizedBasicFacialExpression = function(basicFacialExpression) {
    // do something...
}
handler.onRecognizedValenceFacialExpression = function(valenceFacialExpression) {
    // do something...
}
// Start ESRC
ESRC.start(property, handler);
```

### Step 3: Feed the ESRC Face SDK

Feed `ESRCType.ESRCMat` on the ESRC Face SDK. To the `feed()` method, pass the `ESRCType.ESRCMat` image received using a camera in real-time. Please do it at 10 fps or higher.

```javascript
ESRC.feed(ESRCMat);
```

### Step 4: Stop the ESRC Face SDK

When your app is not use the camera or destroyed, stop the ESRC Face SDK.

```javascript
ESRC.stop()
```


## Changelogs

### v0.1.4 (JUNE 28, 2022)

If you want to check the record of other versions, go to [Change Log](https://github.com/esrc-official/ESRC-Face-SDK-JavaScript/blob/master/CHANGELOG.md).

- Initial draft.