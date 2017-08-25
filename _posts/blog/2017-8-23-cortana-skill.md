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

The first option (based on Dorado) is still in its alpha version, which seems only applicable for Microsoft employees at the current stage. 
It provides a unified platform for building and managing Cortana skills, here's a neat [introduction video](https://microsoft.sharepoint.com/:v:/r/teams/CortanaSkillsKitUpdatesSupportInternal/_layouts/15/guestaccess.aspx?share=EQ9jKaQoIoBAllnGiODg6SYBNLGkxR7fuejMm-Uzt2vRYA)
and [slides](https://microsoft.sharepoint.com/:b:/r/teams/CortanaSkillsKitUpdatesSupportInternal/_layouts/15/guestaccess.aspx?share=EQ1Hn9u9AjZFuJhn_N3MzcwBD_pjs55A8eusS8DClMUDag)
which are also only available to Microsoft employees.

The second option (based on [Bot Framework](https://dev.botframework.com/)) is publically available, together with its [introduction video](https://channel9.msdn.com/Events/Build/2017/B8031).
However in practice there could be many pitfalls for someone starting from scratch. This walkthrough will guide you step by step to create a simple Cortana skill.

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

**0. Set up your Cortana skills development environment.**

The first thing to do is make sure you have access to all the resources listed in [this article](https://docs.microsoft.com/en-us/cortana/tutorials/setup-dev-env). Note that the Microsoft account (MSA) required for Cortana and LUIS registration can not be the `yourname@microsfot.com` account for Microsoft employees.

**1. Build or reuse an existing bot using the latest BotBuilder SDK.**

[Here](https://docs.microsoft.com/en-us/bot-framework/resources-tools-downloads) is how to get the SDK and other tools you might need.
Following the instructions [here](https://docs.microsoft.com/en-us/bot-framework/bot-builder-overview-getstarted) you will be able to develop an echo bot on the platform you prefer.

**2. Use LUIS.ai in your bot if you need natural language understanding capabilities in your bot.**

[LUIS.ai](https://www.luis.ai) is a language understanding framework that can work with Bot Framework.
Following [this](https://docs.microsoft.com/en-us/azure/cognitive-services/luis/luis-get-started-create-app) toturial you will be able to create a LUIS applicaiton.
It's not necessary to add an intent or entitie to make your LUIS model work, if Luis cannot recognize an intent, it will return an empty string for your bot to handle, see [this question](https://stackoverflow.com/q/41392366/3041068). 

After you've successfully created an application, you can see the [application ID](https://www.luis.ai/applications) and [keys](https://www.luis.ai/keys).
Adding these information to the bot you've created in step 1 like [this](https://github.com/Microsoft/BotBuilder-Samples/blob/master/CSharp/intelligence-LUIS/Dialogs/RootLuisDialog.cs#L14), your bot will be able to exploit LUIS features.
[Here](https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/intelligence-LUIS) is a more sophisticated LUIS exmaple.

**3. Use the new speech functionalities in the BotBuilder SDK to give your bot a voice.**

See [this tutorial](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-cortana-skill). Also in align with the above mentioned LUIS example, we can also use `context.SayAsync(text, speech)` instead of `context.PostAsync(text)` to add speech to your bot.

**4. Deploy your bot to Azure.**

See [this tutorial](https://docs.microsoft.com/en-us/bot-framework/deploy-bot-visual-studio).

**5. Register your bot with the Bot Framework.**

See [here](https://docs.microsoft.com/en-us/bot-framework/portal-register-bot) on how to register your bot with the Bot framework, after registeration, remember to configurate the `web.config` file.

>
If you're using the Bot Builder SDK for Node.js, set the following environment variables:
* MICROSOFT_APP_ID
* MICROSOFT_APP_PASSWORD
If you're using the Bot Builder SDK for .NET, set the following key values in the web.config file:
* MicrosoftAppId
* MicrosoftAppPassword

**6. & 7. Add your bot to the Cortana Channel. Publish your Cortana skill.**

Step 6 and 7 are trivial, see [this turorial](https://docs.microsoft.com/en-us/cortana/tutorials/bot-skills/add-bot-to-cortana-channel). Now you'll be able to try out the Cortana skill you've just built, make sure the Cortana on your system is logged in with the same account you used for development.

Have fun!
