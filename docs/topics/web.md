# Web builds
In addition to your usual Node applications, discord.js has special distributions available that are capable of running in web browsers.
This is useful for client-side web apps that need to interact with the Discord API.
[Webpack 3](https://webpack.js.org/) is used to build these.

## Usage
You can obtain your desired version of discord.js' web build from the [webpack branch](https://github.com/discordjs/discord.js/tree/webpack) of the GitHub repository.
There is a file for each branch and version of the library, and the ones ending in `.min.js` are minified to substantially reduce the size of the source code.

Include the file on the page just as you would any other JS library, like so:
```html
<script type="text/javascript" src="discord.VERSION.min.js"></script>
```

Rather than importing discord.js with `require('lorio.discord.js')`, the entire `Discord` object is available as a global (on the `window`) object.
The usage of the API isn't any different from using it in Node.js.

## Restrictions
- Any voice-related functionality is unavailable, as there is currently no audio encoding/decoding capabilities without external native libraries,
  which web browsers do not support.
- The ShardingManager cannot be used, since it relies on being able to spawn child processes for shards.
- None of the optional packages are usable, since they're native libraries.

## Example
```html
<script type="text/javascript" src="discord.11.6.4.min.js"></script>
<script type="text/javascript">
  const client = new Discord.Client();

  client.on('message', msg => {
    const guildTag = msg.channel.type === 'text' ? `[${msg.guild.name}]` : '[DM]';
    const channelTag = msg.channel.type === 'text' ? `[#${msg.channel.name}]` : '';
    console.log(`${guildTag}${channelTag} ${msg.author.tag}: ${msg.content}`);
  });

  client.login('some crazy token');
</script>
```
