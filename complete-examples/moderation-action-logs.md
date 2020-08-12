---
description: >-
  This page describes using 2 different enmaps in tandem using autonum and a
  reference array.
---

# Moderation Action Logs

An interesting problem in javascript is that having an array of objects can be quite the ordeal. A lot of things you want to do require functions and loops, bleh. So, where Enmap is meant to be easier to use, this is an area where it's still a bit hard to handle things. 

But there's a solution. If Enmap isn't enough, how about **TWO**  Enmap???? So yeah, we're going to be using one enmap to store user data, and another to store "warnings", that is to say, moderation actions stored as objects. 

When we add a new element to the _actions_ enmap, we'll be adding a _reference_ to that new entry in the _user_ enmap, via the `autonum` feature.

If you've read about databases a bit, you might have heard about "autonum" and "automatic indexes" before, and this is exactly it. Alright let's get down to brass tax!

### The Actions Enmap

The actions enmap will be using autonum to generate new unique numbers that we'll be able to reference later. The setup is very typical, to begin. We'll attach these things to the discord.js client to keep things simple.

```javascript
client.actions = new Enmap({
    name: 'actions'
});
```

When we want to create a new action, it's a simple act of using autonum to get a key automatically. Let's do a simple warning: 

```javascript
const newActionId = client.actions.autonum;
client.actions.set(newActionId, {
    user: target.id,
    guild: message.guild.id,
    type: 'warning',
    moderator: message.author.id,
    reason: "Don't do it again!",
    when: Date.now()
});
```

So what this does is twofold: it gives us an ID, as well as save the data for this new warning in the Enmap. 

### The User Enmap

You might already have one of those enmaps lying around, but if you don't, the deal's pretty much the same \(because enmap is _simple_!\): 

```javascript
client.userProfiles = new Enmap({
    name: 'userProfiles'
});
```

We of course need to have some properties in there, and this will be done using ensure\(\). This is very similar to our Points system, and it can be done on user join \(guildMemberAdd\) and/or in the message event. Both would be fine: 

```javascript
client.userProfiles.ensure(message.author.id, {
    id: message.author.id,
    guild: message.guild.id,
    totalActions: 0,
    warnings: [],
    kicks: []
});
```

### The Commands

So now we have everything ready to create a simple warn command that will use the above setup to create what we need: 

```javascript
if (command === 'warn') {
    // get a target user
    const target = message.mentions.users.first();
    // remove the mention from the message, join for a reason
    const reason = args.slice(1).join(" ");
    const newActionId = client.actions.autonum;
    client.actions.set(newActionId, {
        user: target.id,
        guild: message.guild.id,
        type: 'warning',
        moderator: message.author.id,
        reason: reason,
        when: Date.now()
    });
    // Push the action to the user's warnings
    client.userProfiles.push(target.id, newActionId, 'warnings');
    client.userProfiles.inc(target.id, 'totalActions');
    // then send some message or embed or whatever
    message.channel.send(`${target} was warned for '${reason}`);
}
```

So how does this help us in the end? If you look at the warnings, you only get a bunch of IDs, right? Well, we can most definitely do some array magic in order to get these proper values... Yeah let's do that. Abracadabra!

```javascript
if (command === 'mywarns') {
    const warnIDs = client.userProfiles.get(message.author.id, 'warnings');
    const warnData = warnIDs.map(id => client.actions.get(id));
    // have fun displaying this wooh!
    message.reply(`You have ${warnIDs.length} warns, buddy!`);
}
```

Now go have fun an explore the endless possibilities of this system :D

