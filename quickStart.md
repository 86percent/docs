---
title: Quickstart
description: Have your bot running in 5min
layout: page
---

# Create an account

To get started with 86%, you first need to create an account on the platform.
1. Go to [86% Bot Editor](https://editor.86percent.co){:target="_blank"}
2. Enter your email, password and name as shown on the screen capture below: 
![Sign up on 86percent.co](/resources/signup.png)
3. You're in!
![Connected to 86percent.co](/resources/justLoggedIn.png) 

# Create your first bot

1. To create your first bot, simply click on "My first bot" button.
2. Give it a good name and choose your default language:
![Connected to 86percent.co](/resources/giveItAName.png) 
3. You're all set!

If you want to learn more on the Bot Editor, [open the Bot Editor documentation](editor.md)

# Basic integration concepts 

 - **Bot**: we refer as `bot` a scenario that is defined within the `Bot Editor`.
 - **Conversation**: we refer as `conversation` the content of the exchange between the user and `86% SDK`.   
 - **Bot file**: when you publish a `bot` in the `Bot Editor`, it generates a `bot file`. This file contains the entire definition of your bot scenario.

Note that it's possible to play several bots in a single conversation, either by chaining bots together or by manually starting a bot in an existing conversation.

![Conversation and bots](/resources/conversation.svg)

# Basic integration in your iOS App 

To run a bot within your App, there are 2 simple steps to `register` it and create a `conversation`.

## Step 1: Register your bot
1. First, initialize the SDK calling `EPManager`, the main class of `86% SDK`. 
2. Then, register any bot that you want to use in your App.  

Typically, you would define a function that you call from the `application didFinishLaunchingWithOptions` in your `AppDelegate`.   

```swift
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        initializeEightySixPercent()
        return true
    }

    func initializeEightySixPercent() {
        EPManager.shared.initialize()
        EPManager.shared.registerBot(uuid: BotUUID.demoBot, fetchingStrategy: .onlineWithDefault(majorVersion: 4, fileName: "SimpleDemo.json"))
    }
```

**Parameters:** 
- `uuid` is the bot identifier. It can be found from the `Bot Editor`, in the [bot's settings](editor.md#settings-uuid).
- `fetchingStrategy` can be of 3 kinds:
    - `onlineWithDefault` (recommended): you provide the SDK with a default `bot file` to use in case of no internet. If you are connected though, the SDK will automatically update your bot to the latest version defined in the `Bot Editor` and compatible with your App (see the section on `majorVersion`).    
    - `online`: the bot definition is loaded directly from the web and you don't need to provide any default `bot file`. It will raise an error if the user is not connected to internet.
    - `offline`: the `bot file` is provided within the App build and will never change dynamically.
    
**What is the majorVersion?**

The `major version` helps enforcing the compatibility between your App and your `bot file`. 

In case the `fetchingStrategy` is not offline, the `86% SDK` automatically fetches new `bot files` once they are published in the `Bot Editor`. But only `bot files` with the same `majorVersion`.
    
## Step 2: Play your bot

To play your `bot`, you need to create a `conversation`, starting it with your `bot` and then you can present the `86% SDK` main controller with your `conversation` played within.

```swift
    // Create a new conversation: 
    let conversation = EPChatConversation(botUuid: BotUUID.demoBot)
    
    // Get the controller that displays this conversation:
    EPManager.shared.controller(for: conversation) { controller, error in
        if let controller = controller {
            controller.navigationItem.leftBarButtonItem = UIBarButtonItem(barButtonSystemItem: .stop, target: self, action: #selector(self.dismissController))
            self.presentController(UINavigationController(rootViewController: controller))
        } else {
            self.showAlert(message: error?.localizedDescription ?? "N/A")
        }
    }
``` 

 