---
layout: documentation
title: Commands
description: The Commands API lets you create custom commands for users to run
type: server
---

The Commands API lets you create custom commands for users to run

## Methods

### `#add(commandText, command)`

Registers a new command for users on the lounge. `commandText` is what the users will type after `/`, and command is the command object.

The `command` object will have the following structure:

```js
{
  input: function(client, target, command, args) {
    // Command logic goes here
  }
}
```

The `input` function will be run when a user runs the provided command. Parameters: `client` is a [client](/docs/api/client) object, for the user sending the command, `target` is the channel/user/lobby the command was sent from, `command` is the name of the command, and `args` is the rest of the input command.


#### Example

```js
const shrug = {
  input: function(client, target, command, args) {
    const messageWithShrug = args.join(" ") + " ¯\\_(ツ)_/¯";
    client.runAsUser(messageWithShrug, target.chan.id);
  }
};

module.exports = {
  onServerStart(thelounge) {
    thelounge.Commands.add("shrug", shrug);
  }
};
```