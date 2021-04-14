# Room-Checker-Bot 🤖 MSFT Version

## What is it ?
This bot checks the availability of a room and allows you to book it.
<img src="https://raw.githubusercontent.com/SarahCiscoFrance/room-checker-bot-MSFT/master/Visual-msft.png" width="500">

This form allows you to book the room during 30/45/60 minutes from the moment you submit the form.

**How ?**

All Webex Room, Board and Desk series devices come with intelligent people counting sensors directly embedded without any additional cost.
So a Webex device in a room can tell us if this room is currently used or not.

In our case the devices send 2 type of data to the Room-Checker-Bot through a macro :
- **Presence** : the presence of a person in the room
- **PeopleCount** : the number of people detected in the room

This data are send by the following marco : https://github.com/SarahCiscoFrance/room-checker-bot/blob/master/room-checker-macro.js

To add a device to the bot just install the macro on this device

## How to run 🔨

MicrosoftAppId=
MicrosoftAppPassword=
PORT=

1. Clone this repo:

    ```sh
    git clone https://github.com/SarahCiscoFrance/room-checker-bot-MSFT.git
    ```

1. Change into the new repo's directory and install the Node.js dependencies:

    ```sh
    npm install
    ```
1. Create a [BotFramework]https://dev.botframework.com/bots account, and note/save your MicrosoftAppId, MicrosoftAppPassword

1. Edit the `.env` file and configure past your MicrosoftAppId and MicrosoftAppPassword. Also choose a PORT number.

1. Install mongodb and create a collection of objects that you will call "codecs" (see example below).
    ```sh
    {
        "_id" : ObjectId("5e2809bbbb4e47d8339b0aed"),
        "mac" : "6C:6C:D3:2B:F3:70",
        "name" : "Kandinsky Dual 70",
        "status" : false,"nbPeople" : 5,
        "ip" : "10.1.110.182",
        "publicIp" : "::ffff:10.1.110.182"
    }
    ```
    
1. Install the macro on your Webex device [link to the macro](https://github.com/SarahCiscoFrance/room-checker-bot/blob/master/room-checker-macro.js)

    >This will allow the bot to receive presence data and have the device in its list 

1. You're ready to run your bot:

    ```sh
    node index.js
    ```



# Extra informations

## Testing the bot using Bot Framework Emulator

[Bot Framework Emulator](https://github.com/microsoft/botframework-emulator) is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

- Install the Bot Framework Emulator version 4.3.0 or greater from [here](https://github.com/Microsoft/BotFramework-Emulator/releases)

### Connect to the bot using Bot Framework Emulator

- Launch Bot Framework Emulator
- File -> Open Bot
- Enter a Bot URL of `http://localhost:3978/api/messages`

With the Bot Framework Emulator connected to your running bot, the sample will not respond to an HTTP GET that will trigger a proactive message.  The proactive message can be triggered from the command line using `curl` or similar tooling, or can be triggered by opening a browser windows and nagivating to `http://localhost:3978/api/notify`.

### Using curl

- Send a get request to `http://localhost:3978/api/notify` to proactively message users from the bot.

   ```bash
    curl get http://localhost:3978/api/notify
   ```

- Using the Bot Framwork Emulator, notice a message was proactively sent to the user from the bot.

### Using the Browser

- Launch a web browser
- Navigate to `http://localhost:3978/api/notify`
- Using the Bot Framwork Emulator, notice a message was proactively sent to the user from the bot.

## Proactive Messages

In addition to responding to incoming messages, bots are frequently called on to send "proactive" messages based on activity, scheduled tasks, or external events.

In order to send a proactive message using Bot Framework, the bot must first capture a conversation reference from an incoming message using `TurnContext.getConversationReference()`. This reference can be stored for later use.

To send proactive messages, acquire a conversation reference, then use `adapter.continueConversation()` to create a TurnContext object that will allow the bot to deliver the new outgoing message.

### Avoiding Permission-Related Errors

You may encounter permission-related errors when sending a proactive message. This can often be mitigated by using `MicrosoftAppCredentials.trustServiceUrl()`. See [the documentation](https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-proactive-message?view=azure-bot-service-4.0&tabs=javascript#avoiding-401-unauthorized-errors) for more information.

## Deploy this bot to Azure

To learn more about deploying a bot to Azure, see [Deploy your bot to Azure](https://aka.ms/azuredeployment) for a complete list of deployment instructions.
