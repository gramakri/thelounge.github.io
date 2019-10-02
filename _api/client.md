---
layout: documentation
title: Client
description: The Client object defines a user's connection to an IRC server and to the web browser.
---

The Client object defines a user's connection to an IRC server and to the web browser.

## Methods

### `#runAsUser(command, chatId)`

Runs a command in The Lounge as if the user has sent it to us. Useful for amending messages sent, or for aliases for other commands. `command` is a string containing a standard IRC message, `chatId` is the channel/user/lobby to send the command to.
It is important to note that this does not go directly to the IRC server, it will go through the lounge first. So this can create infinite loops if you aren't careful. 


#### Example

```js
client.runAsUser("/join #thelounge", 0);
// Sends `/join #thelounge` to the lobby on the lounge. This will then be eventually passed to the IRC server
```

### `#createChannel(channelAttributes)`

This will create a channel in the lounge for the user, using the provided channel attributes.

#### Example

```js
client.createChannel({
    type: "query",
    name: "My Plugin"
});
```

### `#sendToBrowser(event, data)`

Raw command to send a message to the browser.

`event` is the name of the event, it must be something that browser can recognise, otherwise it will be ignored.
`data` is the body of the event to be sent. Again, this needs to be something the browser knows how to deal with.

### `#getChannel(chanId)`

Get a message from it's id.