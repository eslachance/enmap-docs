# Per-Server Settings

This example uses a very, _very_ simple bot made in discord.js to demonstrate how easily [Enmap](https://www.npmjs.com/package/enmap) can be used to create a per-server configuration system.

Remember to follow the [Installation Instructions](../install/) before running any of this!

## Initializing

Our first task is of course to initialize the enmap correctly. In this case, we're attaching the settings to our client object so we can use it in different commands. 

```javascript
// start discord.js init
// config with token and prefix.
const config = require("./config.json"); 
// Code below supports and is tested under "stable" 11.3.x
const Discord = require("discord.js");
const client = new Discord.Client();
// end discord.js init

// Initialize the server configurations
const Enmap = require('enmap');

// I attach settings to client to allow for modular bot setups
// In this example we'll leverage fetchAll:false and autoFetch:true for
// best efficiency in memory usage. We also have to use cloneLevel:'deep'
// to avoid our values to be "reference" to the default settings.
// The explanation for why is complex - just go with it.
client.settings = new Enmap({
  name: "settings",
  fetchAll: false,
  autoFetch: true,
  cloneLevel: 'deep'
});
// Just setting up a default configuration object here, to have somethign to insert.
const defaultSettings = {
  prefix: "!",
  modLogChannel: "mod-log",
  modRole: "Moderator",
  adminRole: "Administrator",
  welcomeChannel: "welcome",
  welcomeMessage: "Say hello to {{user}}, everyone!"
}
```

## Events Setup

```javascript
client.on("guildDelete", guild => {
  // When the bot leaves or is kicked, delete settings to prevent stale entries.
  client.settings.delete(guild.id);
});
  
client.on("guildMemberAdd", member => {
  // This executes when a member joins, so let's welcome them!
  
  // First, ensure the settings exist
  client.settings.ensure(member.guild.id, defaultSettings);
  
  // First, get the welcome message using get: 
  let welcomeMessage = client.settings.get(member.guild.id, "welcomeMessage");
  
  // Our welcome message has a bit of a placeholder, let's fix that:
  welcomeMessage = welcomeMessage.replace("{{user}}", member.user.tag)
  
  // we'll send to the welcome channel.
  member.guild.channels
    .find("name", client.settings.get(member.guild.id, "welcomeChannel"))
    .send(welcomeMessage)
    .catch(console.error);
});
```

## Message Event

The main event for our bot, where messages are received. Any error here will probably crash the bot on every message received, so be careful!

```javascript
client.on("message", async (message) => {
  // This stops if it's not a guild (obviously), and we ignore all bots.
  // Pretty standard for any bot.
  if(!message.guild || message.author.bot) return;
  
  // We can use ensure() to actually grab the default value for settings,
  // if the key doesn't already exist. 
  const guildConf = client.settings.ensure(message.guild.id, defaultSettings);
  
  // Now we can use the values! 
  // We stop processing if the message does not start with our prefix for this guild.
  if(message.content.indexOf(guildConf.prefix) !== 0) return;

  //Then we use the config prefix to get our arguments and command:
  const args = message.content.split(/\s+/g);
  const command = args.shift().slice(guildConf.prefix.length).toLowerCase();
  
  // Commands Go Here
});
```

## Command to set configurations

```javascript
  // Alright. Let's make a command! This one changes the value of any key
  // in the configuration.
  if(command === "setconf") {
    // Command is admin only, let's grab the admin value: 
    const adminRole = message.guild.roles.find("name", guildConf.adminRole);
    if(!adminRole) return message.reply("Administrator Role Not Found");
    
    // Then we'll exit if the user is not admin
    if(!message.member.roles.has(adminRole.id)) {
      return message.reply("You're not an admin, sorry!");
    }
    
    // Let's get our key and value from the arguments. 
    // This is array destructuring, by the way. 
    const [prop, ...value] = args;
    // Example: 
    // prop: "prefix"
    // value: ["+"]
    // (yes it's an array, we join it further down!)
    
    // We can check that the key exists to avoid having multiple useless, 
    // unused keys in the config:
    if(!client.settings.has(message.guild.id, prop)) {
      return message.reply("This key is not in the configuration.");
    }
    
    // Now we can finally change the value. Here we only have strings for values 
    // so we won't bother trying to make sure it's the right type and such. 
    client.settings.set(message.guild.id, value.join(" "), prop);
    
    // We can confirm everything's done to the client.
    message.channel.send(`Guild configuration item ${prop} has been changed to:\n\`${value.join(" ")}\``);
  }
```

## Command to show the configuration

```javascript
  if(command === "showconf") {
    let configProps = Object.keys(guildConf).map(prop => {
      return `${prop}  :  ${guildConf[prop]}\n`;
    });
    message.channel.send(`The following are the server's current configuration:
    \`\`\`${configProps}\`\`\``);
  }
```



