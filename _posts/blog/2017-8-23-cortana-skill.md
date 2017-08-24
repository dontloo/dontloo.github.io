---
layout: post
title: "Cortana Skill Walkthrough"
modified: 2017-8-23
categories: blog
excerpt:
tags: []
date: 2017-8-23
---

At the time of writing, [Cortana](https://developer.microsoft.com/en-us/cortana) supports two ways of creating a skill as shown [here](https://developer.microsoft.com/en-us/cortana/dashboard#!/home).

The first option (based on Dorado) is sitll in its alpha version, which seems only applicable for Microsoft employees at the current stage. 
It provides a unified platform for building and managing Cortana skills, here's a neat [introduction video](https://microsoft.sharepoint.com/:v:/r/teams/CortanaSkillsKitUpdatesSupportInternal/_layouts/15/guestaccess.aspx?share=EQ9jKaQoIoBAllnGiODg6SYBNLGkxR7fuejMm-Uzt2vRYA)
and [slides](https://microsoft.sharepoint.com/:b:/r/teams/CortanaSkillsKitUpdatesSupportInternal/_layouts/15/guestaccess.aspx?share=EQ1Hn9u9AjZFuJhn_N3MzcwBD_pjs55A8eusS8DClMUDag)
which are also only available to Microsoft emplyees.

The second option (based on [Bot Framework](https://dev.botframework.com/)) is publically avaiable, together with its [introduction vedio](https://channel9.msdn.com/Events/Build/2017/B8031).
However in practice there could be many pitfalls for someone starting from scrach. This walkhtrough will guide you step by step to create a simple Cortana skill.

As discribed in the [official document](https://docs.microsoft.com/en-us/cortana/tutorials/bot-skills/creating-a-bot-based-skill), the major steps are as follows.
>
1. Build or reuse an existing bot using the latest BotBuilder SDK.
2. Use LUIS.ai in your bot if you need natural language understanding capabilities in your bot.
3. Use the new speech functionalities in the BotBuilder SDK to give your bot a voice.
4. Deploy your bot to Azure.
5. Register your bot with the Bot Framework.
6. Add your bot to the Cortana Channel.
7. Publish your Cortana skill.

We'll walk through each step in details.

**1. Build or reuse an existing bot using the latest BotBuilder SDK.**

[Here](https://docs.microsoft.com/en-us/bot-framework/resources-tools-downloads) is how to get the SDK and other tools you might need.
Following the instructions [here](https://docs.microsoft.com/en-us/bot-framework/bot-builder-overview-getstarted) you will be able to develop an echo bot on the platform you prefer.

**2. Use LUIS.ai in your bot if you need natural language understanding capabilities in your bot.**

[LUIS.ai](https://www.luis.ai) is a language understanding framework that can work with Bot Framework.
Following [this](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-get-started-create-app) toturial you will be able to create a LUIS applicaiton.
In the simplest case, you don't need to add any intents or entities since there's always a default option "None". 
But do remember to add some utterances to the "None" intent, otherwise your app won't get trained.

After you've successfully created an application, you can see the [application ID](https://www.luis.ai/applications) and [keys](https://www.luis.ai/keys).
Adding these information to the bot you've created in step 1 like [this](https://github.com/Microsoft/BotBuilder-Samples/blob/master/CSharp/intelligence-LUIS/Dialogs/RootLuisDialog.cs#L14), your bot will be able to exploit LUIS features.
[Here](https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/intelligence-LUIS) is a more sophisticated LUIS exmaple.

**3. Use the new speech functionalities in the BotBuilder SDK to give your bot a voice.**

See [this tutorial](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-cortana-skill).

**4. Deploy your bot to Azure.**
See [this tutorial](https://docs.microsoft.com/en-us/bot-framework/deploy-bot-visual-studio), remember to configurate the `web.config` file after deployment.

**5. Register your bot with the Bot Framework.**
