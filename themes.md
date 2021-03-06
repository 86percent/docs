---
title: Bot themes 
description: (draft documentation)<br/>Customize the look & feel of your in-app conversations
layout: page
---

# Overview 

Themes let you customize the look & feel of your in-app conversations.

Before coding the appearance, a designer will often be involved to design it. To help doing with this step, here's a [Sketch document](/resources/86Percent_Theme_template.sketch) that can be customized easily.

![Sketch Document Preview](/resources/SketchPreview.png)

# EPAppearance

To create a theme, you'll have to handle an `EPAppearance` object.

Here is the structure. We'll explore the different levels of customization in the documentation below.

![Global Architecture](/resources/themes/architecture.png)

On the `EPAppearance`, you can for instance customize:
* the `mainTintColor`
* the `customFontName`
* the `customBackgroundColor`
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPAppearance.html)

You can also customize the look and feel of the `Bubbles`, and the `Input` (the custom keyboard displayed so that the user can answer the chatbot's question).

## Bubbles
On `Bubbles`, you can customize:
* the `typingAnimation`: the loading indicator
* the shapes of the bubbles that can be different if it's an incoming or outgoing bubble, and if it has a tail or not. 
These objects are `incoming`, `incomingFollowed`, `outgoing`, and `outgoingFollowed`, of class `Appearance`.
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPAppearance/Bubbles.html)

### Bubble Appearance

On a Bubble `Appearance` object, you can define for instance:

* the `textColor` (UIColor)
* the `strongTextColor` (UIColor)
* the `backgroundColor` (UIColor)
* the `bubbleImage` (UIImage), the bubble background image (will be tinted by the `backgroundColor`).
* the `bubbleOverImage` (UIImage), coming over the image for video/pictures
* the `cellLayoutOption` (LayoutOption), on which you can customize offsets/insets for instance.
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPAppearance/Bubbles/Appearance.html)

Important: all images for the bubbles must be stretchable, and sliced in Xcode (see screenshot below).

![Global Architecture](/resources/themes/bulleImage_sliced.png){:class="img-responsive"}

## Input

On the `EPAppearance`, you can also customize the `Input` (where the user sends inputs).
* `textContainer` (UIImage), the image to use as the input text field background.
* `positiveSendIcon` (UIImage), this is the "Send button" icon for positive option.
* and same principle for `negativeSendIcon`, `searchIcon`, and `sendIcon`
* for all possibilities, please refer to the [iOS Reference API](https://www.86percent.co/documentation/ios/Classes/EPAppearance/Input.html)

## Helpers

To quickly define a `EPAppearance`, you can call the constructor with the following arguments.

```swift
let mainColor = UIColor(hexString: "#0275D8")
let secondaryColor = UIColor(hexString: "#0379D8")
let appearance: EPAppearance = EPAppearance(resourcePrefix: "mytheme", mainColor: mainColor, secondaryColor: secondaryColor)
```

* `mainColor`: this is the color of the outgoing bubbles (right-hand side bubbles, `outgoing` and `outgoingFollowed`)
* `secondayColor`: this is the color of the incoming bubbles (left-hand side bubbles, `incoming` and `incomingFollowed`)
* based on the `resourcePrefix`, the SDK will try to fetch the graphical resources, following this naming convention (e.g. mytheme_incomingBubble, mytheme_incomingBubbleNoTail...):

![Global Architecture](/resources/themes/theme_prefix.png){:class="img-responsive"}

# Code sample

Here is an example, including the helper when instantiating `EPAppearance`:

```swift
class func myCustomTheme() -> EPAppearance {   
    let mainColor = UIColor(hexString: "#0275D8")
    let secondaryColor = UIColor(hexString: "#0379D8")
    let appearance: EPAppearance = EPAppearance(resourcePrefix: "mytheme", mainColor: mainColor, secondaryColor: secondaryColor)
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