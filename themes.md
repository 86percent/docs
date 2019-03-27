---
title: Bot themes (draft documentation)
description: Customize the look & feel of your in-app conversations
layout: page
---

# EPAppearance

To create a theme, you'll have to handle an `EPAppearance` object.

Here is the structure. We'll explore the different levels of customization in the documentation below.

![Global Architecture](/resources/themes/architecture.png)

On the `EPAppearance`, you can for instance customize:
* the `mainTintColor`
* the `customFontName`
* the `customBackgroundColor`
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPBubbleChatAppearanceOption.html)

You can also customize the look and feel of the `Bubbles`, and the `Input` (the custom keyboard displayed so that the user can answer the chatbot's question).

[iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPAppearance.html)

## Bubbles
On `Bubbles`, you can customize:
* the `typingAnimation`: the loading indicator
* the shapes of the bubbles, of class `Appearance`, that can be different if it's an incoming or outgoing bubble, and if it has a tail or not. 
These objects are `incoming`, `incomingFollowed`, `outgoing`, and `outgoingFollowed`, of class `Appearance`.
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPBubbleChatAppearanceOption.html)

### Bubble Appearance

On an Bubble `Appearance` object, you can define for instance:

* the `textColor` (UIColor)
* the `strongTextColor` (UIColor)
* the `backgroundColor` (UIColor)
* the `bubbleImage` (UIImage), the bubble background image (will be tinted by the `backgroundColor`).
* the `bubbleOverImage` (UIImage), coming over the image for video/pictures
* the `cellLayoutOption` (LayoutOption), on which you can customize offsets/insets for instance.
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPBubbleChatAppearanceOption.html)

Important: all images for the bubbles must be stretchable, and sliced in Xcode (see screenshot below).

![Global Architecture](/resources/themes/bulleImage_sliced.png){:class="img-responsive"}

## Input

On the `EPAppearance`, you can also customize the `Input` (where the user sends inputs).
* `textContainer` (UIImage), the image to use as the input text field background.
* `positiveSendIcon` (UIImage), this is the "Send button" icon for positive option.
* and same principle for `negativeSendIcon`, `searchIcon`, and `sendIcon`
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPBubbleChatAppearanceOption.html)

## Helpers

To quickly define a `EPAppearance`, you can call the constructor with the following arguments.

```swift
let mainColor = UIColor(hexString: "#0275D8")
let appearance: EPAppearance = EPAppearance(resourcePrefix: "mytheme", mainColor: mainColor, secondaryColor: mainColor)
```

The `resourcePrefix` will try to fetch the graphical resources, following this naming convention (e.g. mytheme_incomingBubble, mytheme_incomingBubbleNoTail...):

![Global Architecture](/resources/themes/theme_prefix.png){:class="img-responsive"}

# Code sample

Here is a full theming example, including the helper when instantiating `EPAppearance`:

```swift
class func myCustomTheme() -> EPAppearance {   
    let mainColor = UIColor(hexString: "#0275D8")
    let appearance: EPAppearance = EPAppearance(resourcePrefix: "mytheme", mainColor: mainColor, secondaryColor: mainColor)
    appearance.bubbleAppearance.incoming.textColor = .black
    appearance.bubbleAppearance.incomingFollowed.textColor = .black
    appearance.customFontName = "ComicBook"
    appearance.customStrongFontName = "ComicBook-BoldItalic"
    appearance.customSectionDateColor = #colorLiteral(red: 0.9931825995, green: 0.856918633, blue: 0.007652404252, alpha: 1).alpha(0.8)
    appearance.customBackgroundColor = UIColor.clear
    appearance.endBotButtonColor = #colorLiteral(red: 0.9931825995, green: 0.856918633, blue: 0.007652404252, alpha: 1)
    appearance.endBotButtonTextColor = .black
    appearance.bubbleAppearance.typingAnimation = typingAnimation(color: mainColor)
    return appearance
    }
```