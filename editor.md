---
title: Bot Editor
description: Learn how to use the Bot Editor
layout: page
---

In the `Bot Editor`, you will find references to this guide, contextualized in the various sections.

# <a name="botvars-ab"></a>Bot inputs

## Input bot variables
These `variables` will have to be passed in the Mobile App to the `Mobile SDK` before starting the `bot`.
If your Mobile App does not give one of the `variables` (it's possible), then this `variable` will be undefined. In a `rule`, you can then test its existence.

## A/B Testing
When you activate the A/B Testing mode for the entire `bot`, a new `Input bot variable` will be available in the `bot`.
This `OPTION A/B` variable is a `boolean` and is either `true` (it's A) or `false` (it's B).

On this `OPTION A/B`, you can define `rules` in the `bot` to follow different paths and then measure conversions.

# <a name="node-message"></a>Node Message

## Default message
The `bot  message` you define in the `EDITOR VIEW` is the default message, in the default language of your `bot`.

## URL-only message
If your message is only a URL, then the `Bot Editor` will try to determine the MIME type (e.g. image/gif, image/png...).
This will be used by the `Mobile SDK` to display it nicely in the App.
Be careful: in other languages, make sure to put a URL as well. This MIME type is determined for the default language.

## "End" switch
If this is an end of your bot, you just have to turn on the switch.

Then you can configure this "end", either by displaying a standard left bubble, or a large central button.

Moreover, here you can chain bots if necessary: if you want to have the `Mobile SDK` chaining another `bot`.

# <a name="next-messages-rules"></a>Next messages and rules

## Next message
By default, if it's not an end message, you have to determine the next message. The `Mobile SDK` will simply move to this message.

## What a rule is
Based on the `variables` available in the `bot`, you can determine `rules` and `conditions` to have your end-user following different paths of your scenario.

## Priority
In the list of `rules` you'll determine for a given message, the first `rule` matching the conditions wins. It means you have to put first the `rule` having the highest priority, and so on. 

# <a name="messages"></a>Messages
In the `MESSAGES` tab, you can manage all your messages:
* translate them in various languages (go to `SETTINGS` / `General info` to add languages to your `bot`)
* and add `variations` to your message, either to test the conversion of other ways to talk to your users, or simply to make it more natural in terms of interactions (e.g. for a `bot` you'll display several times to your user, you don't have to always have the exact same messages).

# <a name="user-input"></a>User input

## <a name="user-input-syntax"></a>Syntax to display variable
To display the user input in a message, you simply type the variable name like this `<variableName>`

> E.g.: Nice to meet you &lt;firstname&gt;!

# <a name="settings"></a>Bot settings

## <a name="settings-uuid"></a>Bot UUID
The bot UUID is the bot main identifier, necessary to "play" the bot from the `86% SDK`.

To find it, open one of your bots, and go to `SETTINGS` / `General info`
