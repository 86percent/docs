---
title: Quickstart
description: Have your bot running in 5min
layout: page
---

## First things first


1. To get started with 86%, you first need to [create an account](https://editor.86percent.co/welcome) on the platform.
2. Then, create your first bot, by clicking on "My first bot" button. 
3. You're all set!

If you want to learn more on the Bot Editor, [open the Bot Editor documentation](editor.md)

## Basic integration concepts 

 - **Bot**: we refer as `bot` a scenario that is defined within the `Bot Editor`.
 - **Conversation**: we refer as `conversation` the content of the exchange between the user and `86% SDK`.   
 - **Bot file**: when you publish a `bot` in the `Bot Editor`, it generates a `bot file`. This file contains the entire definition of your bot scenario.

## Basic integration in your iOS App 

To run a bot within your App, you first need to add 86% SDK as a pod to your project. Then, there are 2 simple steps to `register` it and create a `conversation`.

### Add 86% SDK to your project
Simply add the following to your `Podfile`.

```
    pod 'EightySixPercent'
```
For more information about pod integration, please refer to the [Cocoapod web site](https://cocoapods.org/).

### Step 1: Register your bot
1. First, initialize the SDK calling `EPManager`, the main class of `86% SDK`. 
2. Then, register any bot that you want to use in your App.  

Typically, you would define a function that you call from the `application didFinishLaunchingWithOptions` in your `AppDelegate`.   

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    EPManager.shared.initialize()
    EPManager.shared.registerBot(uuid: "YOU_BOT_UUID_GOES_HERE", fetchingStrategy: .online(majorVersion: nil))
    return true
}
```
   
### Step 2: Play your bot

To play your `bot`, you need to create a `conversation`, starting it with your `bot` and then you can present the `86% SDK` main controller with your `conversation` played within.

```swift
// Create a new conversation: 
let conversation = EPChatConversation(botUuid: "YOU_BOT_UUID_GOES_HERE")

// Get the controller that displays this conversation:
EPManager.shared.controller(for: conversation) { controller, error in
    if let controller = controller {
        //depending on the fetching strategy you have chosen you may need to handle error and a HUD
        self.presentController(UINavigationController(rootViewController: controller))
    } else {
        self.showAlert(message: error?.localizedDescription ?? "N/A")
    }
}
``` 

## Basic integration in your Android App

To run a bot within your App, you first need to add 86% SDK as a pod to your project. Then, there are 2 simple steps to `register` it and create a `conversation`.

### Requirements for your project

Your project must use the AndroidX libraries. This guide assumes that you included `androidx.appcompat` library in your gradle dependencies:
```
dependencies {
    ...

    // AndroidX
    implementation "androidx.constraintlayout:constraintlayout:1.1.3"
    implementation "androidx.appcompat:appcompat:1.0.2"

    ...
}
``` 

In the gradle.properties file, add the following :
```
    android.useAndroidX=true
    android.enableJetifier=true
```
As described in the [Migration to AndroidX guide](https://developer.android.com/jetpack/androidx/migrate)

### Add 86% SDK to your project

In the project build.gradle add the 86% SDK repository in the `repositories` section:
```
allprojects {
    repositories {
        ...
        maven {
            url "http://artifactory.86percent.co/artifactory/bot-release-local"
        }
        maven { 
            url "https://jitpack.io" 
        }
        ...
    }
}
```

Then in your app `build.gradle` file, add the following: 

```
implementation 'co.86percent:bot:1.1.0’
```

### Step 1: Register your bot

Initialize the 86% SDK, typically in your Application `onCreate` , call a `initEightySixPercent()` method that does the following: 

```kotlin
private fun initEightySixPercent() {
    EPManager.init(this)
    EPManager.registerBot("YOU_BOT_UUID_GOES_HERE", EPBotFetchingStrategy.OnlineWithDefault(1,"SimpleDemo.json"))
}
```

Where `SimpleDemo.json` is the path of your bot JSON export file, relative to your project `assets` folder.

Note : you need to create the `assets` folder under the `main` folder of your Android project. 

### Step 2: play your bot

In the activity your want to run the chatbot, add the following: 

```kotlin
    val conversation = EPChatConversation(Constants.BotUuid.simpleDemo)
    EPManager.fragment(this, conversation) { chatConversationFragment, exception ->
        if (chatConversationFragment != null) {
            val transaction = supportFragmentManager.beginTransaction()
            transaction.replace(R.id.container, chatConversationFragment)
            transaction.commit()
        } else {
            exception?.printStackTrace()
        }
    }
```

## More informations

### RegisterBot's parameters 
- `uuid` is the bot identifier. It can be found from the `Bot Editor`, in the [bot's settings](editor.md#settings-uuid).
- `fetchingStrategy` can be of 3 kinds:
    - `onlineWithDefault` (recommended): you provide the SDK with a default `bot file` to use in case of no internet. If you are connected though, the SDK will automatically update your bot to the latest version defined in the `Bot Editor` and compatible with your App (see the section on `majorVersion`).    
    - `online`: the bot definition is loaded directly from the web and you don't need to provide any default `bot file`. It will raise an error if the user is not connected to internet.
    - `offline`: the `bot file` is provided within the App build and will never change dynamically.
    
### What is the majorVersion? 

The `major version` helps enforcing the compatibility between your App and your `bot file`. 

In case the `fetchingStrategy` is not offline, the `86% SDK` automatically fetches new `bot files` once they are published in the `Bot Editor`. But only `bot files` with the same `majorVersion`.
 
### What's next?

Next, you can take a look at the SDK API reference for [Android](https://www.86percent.co/documentation/android/) and [iOS](https://www.86percent.co/documentation/ios/).
