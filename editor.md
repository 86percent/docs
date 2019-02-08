---
title: Bot Editor
description: Learn how to use the Bot Editor
layout: page
---

# 86% Editor documentation

In the `Bot Editor`, you will find references to this guide, contextualized in the various sections.

### Input bot variables + A/B Testing [#](#input-botvariables)

#### Input bot variables
These variables will have to be passed in the Mobile App to the `Mobile SDK` before starting the `bot`.
If your Mobile App does not give one of the variables (it's possible), then this variable will be undefined. In a `Rule`, you can then test its existence.

#### A/B Testing
When you activate the A/B Testing mode for the entire `Bot`, a new `Input bot variable` will be available in the `bot`.
This `OPTION A/B` variable is a `boolean` and is either `true` (it's A) or `false` (it's B).

On this `OPTION A/B`, you can define `Rules` in the `bot` to follow different paths and then measure conversions.

### Node Message [#](#node-message)

The `bot  message` you define in the `EDITOR VIEW` is the default message, in the default language of your `bot`.
In the `MESSAGES` tab, you can manage all your messages:
* translate them in various languages (go to `SETTINGS` / `General info` to add languages to your `bot`)
* and add `variations` to your message, either to test the conversion of other ways to talk to your users, or simply to make it more natural in terms of interactions (e.g. for a `bot` you'll display several times to your user, you don't have to always have the exact same messages).
