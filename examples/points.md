# Points/Currency System

This points bot is simple, but functional. Make sure you've followed the Installation Instructions before doing the following. 

First, you need to create a new persistent Enmap. Here's how it goes:

```javascript
const Enmap = require("enmap");
client.points = new Enmap({name: "points"});
```

That will create a new Enmap under the name of points, and attaches it to the client object so it can be used where ever you have access to the client object.

## Accumulating Points

The obvious goal of a points system is to accumulate fake internet points and gloat about it. So, of course, that's going to be our first focus. In this example implementation, we will make the points guild-specific, and unuseable in DMs. Points will still accumulate even if the user does a command, which simplifies our code a bit.

Our starting point is a very basic message handler with pre-existing commands - such as what we see in the [Command with Arguments](https://anidiots.guide/first-bot/command-with-arguments) page on An Idiot's Guide. The code is as such:

```javascript
client.on("message", message => {
  if (message.author.bot) return;
  // This is where we'll put our code.
  if (message.content.indexOf(config.prefix) !== 0) return;

  const args = message.content.slice(config.prefix.length).trim().split(/ +/g);
  const command = args.shift().toLowerCase();

  // Command-specific code here!
});
```

We do have a small caveat - we really don't want to react on Direct Messages, so our whole code will be in a block that checks for that:

```javascript
client.on("message", message => {
  if (message.author.bot) return;
  if (message.guild) {
    // This is where we'll put our code.
  }
  // Rest of message handler
});
```

Our very first step is going to be to initialize a new entry in the enmap for any new user - one we haven't received a message from before. This is done using the `enmap.ensure(key, defaultvalue)` method, which can check if a specific key exists in the Enmap, write it if it doesn't \(and return the defaultvalue in this case\). Note that our keys take the format of `guildid-userid` so they're unique to the guild and the user. Also, our data in this case is a complete object, which we'll take advantage of fully.

```javascript
client.on("message", message => {
  if (message.author.bot) return;
  if (message.guild) {
    client.points.ensure(`${message.guild.id}-${message.author.id}`, {
      user: message.author.id,
      guild: message.guild.id,
      points: 0,
      level: 1
    });
    // Code continued...
  }
  // Rest of message handler
});
```

There's obviously a few ways we could have done this, including some fancy ternary condition or whatever. I will, however, keep this code as simple to read as possible.

The following bit is super simple - Enmap has a method to directly increment a value in Enmap even if it's in an object. Pretty clever if I do say so myself!

```javascript
client.on("message", message => {
  if (message.author.bot) return;
  if (message.guild) {
    // Let's simplify the `key` part of this.
    const key = `${message.guild.id}-${message.author.id}`;
    client.points.ensure(key, {
      user: message.author.id,
      guild: message.guild.id,
      points: 0,
      level: 1
    });
    client.points.inc(key, "points");
  }
  // Rest of message handler
});
```

{% hint style="info" %}
Have your own way of incrementing points? No problem! Enmap.math\(\) gives you the ability to add, multiply, and act upon any numerical value or property. To add 10 points, for instance, `client.points.math(key, "+", 10, "points")` would be used.
{% endhint %}

## Ding!

Time to level up! If a user has enough points, they will go up a level. Now we have to do some math here, but don't run off in fear, this one's pretty easy. This is how we calculate the levels:

```javascript
const curLevel = Math.floor(0.1 * Math.sqrt(client.points.get(key, "points")));
```

This line will calculate the square root of `currentPoints` then multiplies that result by 0.1 then floors that result for a round number.

Now we should work out if you've amassed enough points to actually level up, by grabbing the current user's level and comparing them. If the new calculated level is higher, it means the user leveled up and we can deal with that, first by sending them a very annoying mee6-inspired message!

```javascript
if (client.points.get(key, "level") < curLevel) {
  message.reply(`You've leveled up to level **${curLevel}**! Ain't that dandy?`);
}
```

Lastly, we want to update the `score.level` value with the new level so throw this under the `message.reply`.

```javascript
client.points.set(key, curLevel, "level");
```

So here's the whole thing from top to bottom, with bonus comments!

```javascript
client.on("message", message => {
  // As usual, ignore all bots.
  if (message.author.bot) return;
  
  // If this is not in a DM, execute the points code.
  if (message.guild) {
    // We'll use the key often enough that simplifying it is worth the trouble.
    const key = `${message.guild.id}-${message.author.id}`;

    // Triggers on new users we haven't seen before.
    client.points.ensure(`${message.guild.id}-${message.author.id}`, {
      user: message.author.id,
      guild: message.guild.id,
      points: 0,
      level: 1
    });
    
    client.points.inc(key, "points");
    
    // Calculate the user's current level
    const curLevel = Math.floor(0.1 * Math.sqrt(client.points.get(key, "points")));
    
    // Act upon level up by sending a message and updating the user's level in enmap.
    if (client.points.get(key, "level") < curLevel) {
      message.reply(`You've leveled up to level **${curLevel}**! Ain't that dandy?`);
      client.points.set(key, curLevel, "level");
    }
  }
  // Rest of message handler
});
```

## Points & Level Commands

Alright, that's the bulk of the code, you could throw this into your bot and it would work like a charm, however your users wouldn't know how many points, or even their levels, so let's fix that, make a new command called `points`, which will also show them their level.

{% hint style="info" %}
Obviously there's no way for us to know how you're making commands, so again we'll assume you're doing a bot in a single js file. You may need to adjust the code, of course!
{% endhint %}

So let's re-iterate our current starting position.

```javascript
client.on("message", message => {
  if (message.author.bot) return;
  if (message.guild) { /* Points Code Here */ }
  if (message.content.indexOf(config.prefix) !== 0) return;

  const args = message.content.slice(config.prefix.length).trim().split(/ +/g);
  const command = args.shift().toLowerCase();

  // Command-specific code here!
});
```

The `points` command would look like this:

```javascript
  if (command === "points") {
    const key = `${message.guild.id}-${message.author.id}`;
    return message.channel.send(`You currently have ${client.points.get(key, "points")} points, and are level ${client.points.get(key, "level")}!`);
  }
```

## We are the champions, my friend!

Let's finish this off with a very simple `leaderboard` command that will show the top 10 users in the current guild. For this we'll need to _filter_ the Enmap to only get the users for the current guild, then we'll convert the results to an array, sort that, and keep the first 10 results only.

{% hint style="info" %}
We convert to an array because an `Enmap`, just like its underlying `Map` structure, is not ordered and thus cannot be sorted. It may _seem_ ordered because it stores by keys, but that's actually a quirk, not a feature.
{% endhint %}

So here's our leaderboard command:

```javascript
if(command === "leaderboard") {
  // Get a filtered list (for this guild only), and convert to an array while we're at it.
  const filtered = client.points.filter( p => p.guild === message.guild.id ).array();

  // Sort it to get the top results... well... at the top. Y'know.
  const sorted = filtered.sort((a, b) => b.points - a.points);

  // Slice it, dice it, get the top 10 of it!
  const top10 = sorted.splice(0, 10);

  // Now shake it and show it! (as a nice embed, too!)
  const embed = new Discord.RichEmbed()
    .setTitle("Leaderboard")
    .setAuthor(client.user.username, client.user.avatarURL)
    .setDescription("Our top 10 points leaders!")
    .setColor(0x00AE86);
  for(const data of top10) {
    embed.addField(client.users.get(data.user).tag, `${data.points} points (level ${data.level})`);
  }
  return message.channel.send({embed});
}
```

## ADDENDUM: Extra Commands!

```javascript
  if(command === "give") {
    // Limited to guild owner - adjust to your own preference!
    if(message.author.id !== message.guild.ownerID) 
      return message.reply("You're not the boss of me, you can't do that!");

    const user = message.mentions.users.first() || client.users.get(args[0]);
    if(!user) return message.reply("You must mention someone or give their ID!");

    const pointsToAdd = parseInt(args[1], 10);
    if(!pointsToAdd) 
      return message.reply("You didn't tell me how many points to give...")

    // Ensure there is a points entry for this user.
    client.points.ensure(`${message.guild.id}-${user.id}`, {
      user: message.author.id,
      guild: message.guild.id,
      points: 0,
      level: 1
    });

    // Get their current points.
    let userPoints = client.points.get(`${message.guild.id}-${user.id}`, "points");
    userPoints += pointsToAdd;
    

    // And we save it!
    client.points.set(`${message.guild.id}-${user.id}`, userPoints, "points")

    message.channel.send(`${user.tag} has received ${pointsToAdd} points and now stands at ${userPoints} points.`);
  }

  if(command === "cleanup") {
    // Let's clean up the database of all "old" users, 
    // and those who haven't been around for... say a month.

    // Get a filtered list (for this guild only).
    const filtered = client.points.filter( p => p.guild === message.guild.id );

    // We then filter it again (ok we could just do this one, but for clarity's sake...)
    // So we get only users that haven't been online for a month, or are no longer in the guild.
    const rightNow = new Date();
    const toRemove = filtered.filter(data => {
      return !message.guild.members.has(data.user) || rightNow - 2592000000 > data.lastSeen;
    });

    toRemove.forEach(data => {
      client.points.delete(`${message.guild.id}-${data.user}`);
    });

    message.channel.send(`I've cleaned up ${toRemove.size} old farts.`);
  }
```

