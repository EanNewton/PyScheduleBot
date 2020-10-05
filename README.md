<p align="center">
  <a href="" rel="noopener">
 <img src="https://i.imgur.com/M3wjra4.png" alt="Tangerine Bot logo"></a>
</p>

<h3 align="center">Tangerine Bot</h3>

<div align="center">

  ![Status](https://img.shields.io/badge/status-active-success.svg)
  ![Platform](https://img.shields.io/badge/platform-discord-blue.svg)
  ![Language](https://img.shields.io/badge/language-python-yellow.svg)
  ![License](https://img.shields.io/badge/license-GNU%20GPL%20v3-green)

</div>

---

# 📝 Table of Contents
+ [About](#about)
+ [List of Commands](#commandlist)
+ [Info for Geeks](#geeky)

# About <a name = "about"></a>

I initially created this bot to address a problem I saw occurring frequently: Twitch was helping to connect people from all over the globe, which is a wonderful thing, but it brought the problem of communicating across all those disparate places. A streamer would say something like, "Hey friends! I'll be streaming every Tuesday at 6:00PM!" but when exactly that 6:00PM on Tuesday actually is would be different for people located in London vs New York vs Melbourne. I wanted a simple and intuitive way for anyone to find out when it would occur for them with a single command. 

The project has been growing and adding features as requested since then. If there's a change you'd like to see feel free to issue a Pull Request or contact me.

Invite the bot to your server: https://discord.com/api/oauth2/authorize?client_id=663696399862595584&permissions=8&scope=bot

Or, clone the the project to a local directory and launch it with:
`pipenv run python3 main.py`
You will need a bot token from the Discord Developer portal as well as one from Wolfram, placed into ./.env

# List of Commands <a name = "commandlist"></a>
+ [!help](#!help)
+ [!config](#!config)
+ [!sched](#!sched)
+ [!quote](#!quote)
+ [!lore](#!lore)
+ [!dict](#!dict)
+ [!stats](#!stats)
+ [!8ball](#!8ball)
+ [!wolfram](#!wolfram)
+ [!google](#!google)
+ [!word](#!word)
+ [!poem](#!poem)
+ [!yandex](#!yandex)
+ [!custom](#!custom)


## !help <a name = "!help"></a>
Displays a list of available commands and a brief description of what they do.

**Examples**

![help example](https://github.com/EanNewton/FamBot/blob/master/Samples/help.png)

## !config <a name = "!config"></a>
Generates a config file in JSON format. Only usable by the server owner and roles designated as server administrators. Simply edit the file as you desire and then drag and drop it back into any channel in your discord to apply the changes. 

Optional parameters are: 
+ !config reset --- return to a default configuration

**Example Config File**
```
{
    "Server ID": 012340123401234,
    "Server Name": "My First Server",
    "Server Locale": "Asia/Tokyo",
    "Schedule": "Monday = 10; Tuesday = 10; Wednesday = 16; Friday = 10; Saturday = 16; ",
    "URL Footer": "Come hang with us at: <https://www.twitch.tv/>",
    "Quote Format": "{0}\n ---{1} on {2}",
    "Quote Added Format": "\"{0}\"\n by {1} on {2}",
    "Lore Format": "{0}\n ---Scribed by the Lore Master {1}, on the blessed day of {2}",
    "Blacklisted Words": "none, one, two foo bar; three",
    "Moderator Roles": "mod;admin;discord mod;\n"
}


To edit your server configuration simply change the appropiate values, and drag and drop it back into Discord to upload. 

You can always use `!config reset` to return to default values.

Server Locale: This is your default timezone location. 
    See "!schedule help" for more locations.
    
Schedule: This is your stream schedule, times are in 24 hour format. 
    The format to add a stream is:
        [DAY] = [TIME 1], [TIME 2];
        Monday = 10:30, 14; Wednesday = 18; Friday = 12:15, 14:30
    This would add scheduled times for Monday at 10:30AM and 2:00PM, Wednesday at 6PM, etc.

URL Footer: A brief message to be displayed beneath the schedule.
        
Quote Format: How quotes should be displayed when a user enters "!quote". 
    To create a line break use \n.
    {0} will be the quote text.
    {1} will be the quote's author.
    {2} will be the date.
    Each {} field may only be used once.
    
Lore Format: How lore should be displayed when a user enters "!lore". 
    Lore works the same as quotes but only admins and mods may add to it. 
    This is useful for stream point redeems. 
    See "!lore help" for more information.
    
Quote Added Format: What is displayed when a user reacts with :speech_left: to add a new quote. 
    It also follows the {} order of text, author, date.
```

## !sched <a name = "!sched"></a>
Display a schedule of upcoming events for the server in the user's own time zone. Any events occurring today will be bolded.

Aliased names for the command are:
+ !s
+ !sched
+ !schedule

Optional parameters are:
+ !sched help --- display more detailed options available to the user
+ !sched help [CONTINENT] --- display a list of cities in that continent that users can set their location to. Continents include: Africa, America, Antarctica, Asia, Atlantic, Australia, Europe, Indian, Pacific, and abbr. Note: "abbr" is a short list of common locations that have been aliased, e.g. pst, est, jst, gmt
+ !sched set [CONTINENT]/[CITY] --- sets the user's timezone to the correct one for that location
+ !sched [CONTINENT]/[CITY] --- see the schedule for that location without changing the user's location
+ !sched override [CONTINENT]/[CITY] @User1 @User2 @User3... --- an administrator only command to change any user's location

**Examples**

![sched exmaple](https://github.com/EanNewton/FamBot/blob/master/Samples/sched.png)

## !quote <a name = "!quote"></a>
Users can react to any message in the discord with the :speech_left: reaction to add it to a list of quotes. 
Quotes may be any message that is not from a bot, including text, images, videos, embeds, or files.
A random quote can then be displayed by using the !quote command.
Administrators can use :x: on a message that has a received a :speech_left: to remove it from the quotes list. Multiple users reacting with :speech_left: will not add the quote multiple times.
  
Aliased names for the command are:
+ !q
+ !quote

Optional parameters are:
+ !quote [USER] --- Display a quote that was said by that specific user. Note that this is their actual username (case sensitive) and not their display nickname so as to prevent confusion as users change nicknames often. If you are unsure click on the user in either the right panel users list or on their profile picture next to any message they've sent to see their actual username. This does not include the discriminator, which is a # sign folowed by four numbers.
+ !quote help --- Display a brief explanation of the command usage available to the user.

**Examples**

![quote example](https://github.com/EanNewton/FamBot/blob/master/Samples/quote.png)

## !lore <a name = "!lore"></a>
  Works almost exactly the same as !quote but new entries can only be added by administrators, a sort of VIP version of !quote or a randomized version of a pinned message.
  
  Aliased names for the command are:
  + !l
  + !lore
  
  Optional parameters are:
  + !lore help --- Display a brief explanation of the command usage available to the user.
  + !lore [USER] --- Display a piece of lore from a specific user.
  + !lore add [USER] [TEXT] --- Add a new lore entry of [TEXT] with the author set as [USER] at the current date and time. Note that the [USER] must be a single word, any text after the first whitespace will be part of [TEXT]. Administrators may add a :x: reaction to the "!lore add" message to remove the entry.
  
## !dict <a name = "!dict"></a>
Returns the English Wiktionary entry for a word or phrase. This does not necessarily need to be an English word, it simply needs to have an entry in the https://en.wiktionary.org site.

Aliased names for the command are:
+ !dict
+ !dictionary
+ !wiki
+ !wiktionary

Optional parameters are:
+ !dict [TEXT] --- Display an explanation of any single word or phrase.
+ !dict help --- Show all available web interfaced commands.

**Example**
> !dict computer
![dict example](https://github.com/EanNewton/FamBot/blob/master/Samples/dict.png)

## !stats <a name = "!stats"></a>
Display some fun info about the messages being sent. The default command will generate a word cloud of the most common words for the server.

Optional parameters are:
+ !stats help --- Show the help interface.
+ !stats user [USERNAME] --- Create a word cloud for the specified user. Like !quote this is the case sensitive version of the username without the discriminator.
+ !stats channel [CHANNEL] --- Create a word cloud for the specified channel. This is provided as the #channel-name tag.
+ !stats count [LOW] [HIGH] --- Create a bar graph showing the number of messages of length between LOW and HIGH.
+ !stats phrases [LOW] [HIGH] [LIMIT] --- Create a graph showing the most common phrases / n-grams of length between LOW and HIGH. LIMIT is the amount of n-grams to display.
+ !stats common [LIMIT] --- Create a textual list of the most common single words for the server, up to LIMIT.

**Examples**
>!stats
---
![stats default](https://i.imgur.com/RtQR9kJ.png)
---

>!stats user
---
![stats user](https://i.imgur.com/YNXJUy0.png)
---

>!stats channel
---
![stats channel](https://i.imgur.com/Fi7RRRy.png)
---

>!stats count 2 20
---
![stats count](https://i.imgur.com/lgu9Z3U.png)
---

>!stats phrases 2 5 10
---
![stats phrases](https://i.imgur.com/PcEZXSZ.png)
---

>!stats common 10
---
![stats common](https://i.imgur.com/AkxHHUD.png)
---

## !8ball <a name = "!8ball"></a>
The classic 1950's magic eight ball by Carter and Bookman, now on your Discord. 
Use !8ball followed by a question to have your fortune read.

Aliased names for the command are:
+ !8
+ !8ball
+ !eight
+ !eightball

Possible responses are:
+ It is certain.
+ It is decidely so.
+ Without a doubt.
+ Yes -- definitely.
+ You may rely on it.
+ As I see it, yes.
+ Most likely.
+ Outlook good.
+ Yes.
+ Signs point to yes.
+ Reply hazy, try again.
+ Ask again later.
+ Better not tell you now.
+ Cannot predict now.
+ Concentrate and ask again.
+ Don't count on it.
+ My reply is no.
+ My sources say no.
+ Outlook not so good.
+ Very doubtful.

## !wolfram <a name = "!8ball"></a>
Query the Wolfram computational intelligence engine.

Optional parameters are:
+ !wolf txt [QUERY] --- Query the Wolfram Alpha engine for QUERY and return a text based response.
+ !wolf img [QUERY] --- Query the Wolfram Alpha engine for QUERY and return an image based response.

Aliased names for the command are:
+ !w
+ !wolf
+ !wolfram

**Examples**
>!wolf img Evaluate ∫4x6−2x3+7x−4dx
---
![wolf example 1](https://github.com/EanNewton/FamBot/blob/master/Samples/wolfimg.png)

![wolf example 1 result](https://github.com/EanNewton/FamBot/blob/master/Samples/762496307855491113.gif)

---
>!wolf txt what is the weather in Tokyo
---
![wolf  example 2](https://github.com/EanNewton/FamBot/blob/master/Samples/wolftxt.png)
---

## !google <a name = "!google"></a>
Did someone ask a question that could have been Googled? Send a link to Let Me Google That For You for them.

Aliased names for the command are:
+ !g
+ !google
+ !lmgtfy

**Examples**
> !google what is a banana
---
`https://lmgtfy.com/?q=what+is+a+banana&iie=1`

## !gif <a name = "!gif"></a>
Display a random gif or add a new one.

Aliased names for the command are:
+ !gif
+ !react
+ !meme

Optional Parameters include:
+ !gif add --- Drag and drop a gif to add it to the possible responses when !gif is used.
+ !gif add nsfw --- Same as `!gif add` but marks it as NSFW.
+ !gif nsfw --- Include gifs marked as NSFW in possible responses.

## !word <a name = "!word"></a>
Get the Word of the Day from https://wordsmith.org/words/today.html

Aliased names for the command are:
+ !word
+ !wotd

**Examples**

![word example](https://github.com/EanNewton/FamBot/blob/master/Samples/word.png)

## !poem <a name = "!poem"></a>
Get the Poem of the Day from https://poems.com/todays-poem/

Aliased names for the command are:
+ !poem
+ !potd

**Examples**

![poem example](https://github.com/EanNewton/FamBot/blob/master/Samples/poem.png)

## !yandex <a name = "!yandex"></a>
Return a link to a reverse image search.

Aliased names for the command are:
+ !yandex
+ !tineye
+ !image
+ !reverse

Optional parameters are:
+ !yandex [URL] --- Given a URL to an image return a link to a reverse image search for the provided image. You can right click an image within Discord and choose Copy Link.

## !custom <a name = "!custom"></a>
Add custom commands to your discord.
Admins can react to any message with :gear: to add a new command. The first word of the message will be the command name, the remainder will be what is displayed. The command name is taken literally so if you want a ! or . or any prefix make sure to include that.
Admins can react to any message :X: to remove a command where the first word matches a command name to remove it.
Custom commands can override built-in commands, so if you want to disable any command -- such as !sched or !quote -- simply set up a custom command with the same name.

Custom commands can be nested and can also contain specific additional parameters.
For example, if you add the command `!custom1 Foo` and then add `!custom2 <custom1> Bar <GUILD>`, calling !custom2 will then display `Foo Bar my server`. Make sure that nested command calls are enclosed in `<>`. Custom commands do not suppress user, channel, or role mentions and will ping people if you include a mention in them.

Use `!custom` to display the help text as well as any custom commands you have setup for your server.

Additional Parameters include:
+ `<URL>` --- The URL from your from your !config file
+ `<NOW>` or `<TIME>` ---  The current time for the server location from your !config file
+ `<LOCALE>` or `<LOCATION>` --- The server locale from your !config file
+ `<AUTHOR>` --- The username of whoever used the command
+ `<GUILD>` --- Your Discord guild name
+ `<SCHED>` --- Calls !sched
+ `<QUOTE>` --- Calls !quote
+ `<LORE>` --- Calls !lore
	
**Examples**

![custom example](https://github.com/EanNewton/FamBot/blob/master/Samples/custom.png)

---

![custom help](https://github.com/EanNewton/FamBot/blob/master/Samples/custom-help.png)

# Info for Geeks <a name = "geeky"></a>

This project is written entirely in Python 3 as a passion project, as well as my first project in Python. You are encouraged to use, modify, fork, contribute, hack, or do whatever your heart desires with it within the confines of the GNU General Public License Version 3. Pull requests are warmly welcomed.

The core design philosophies for the project are that it should be: easy to use, easy to maintain and modify, and reliable. Python may not always have the comparable speed of C or its compatriots but I'll be damned if it isn't beautiful.

+ [Packages](#packages)
+ [A Note on Users](#users)
+ [How Stuff Works](#workings)

## Packages <a name = "packages"></a>
The backend makes heavy use of SQLite 3 via the SQLAlchemy project to keep with the Reliable philosophy.

The full list of external Python packages directly imported is:
+ [Pendulum](https://pendulum.eustace.io/)
+ [Discord](https://pythondiscord.com/)
+ [DotEnv](https://github.com/theskumar/python-dotenv)
+ [SQLAlchemy](https://www.sqlalchemy.org/)
+ [AIOHTTP](https://docs.aiohttp.org/en/stable/)
+ [AIOFiles](https://github.com/Tinche/aiofiles)
+ [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/)
+ [WiktionaryParser](https://github.com/Suyash458/WiktionaryParser)
+ [Pandas](https://pandas.pydata.org/)
+ [NLTK](https://www.nltk.org/)
+ [word_cloud](https://github.com/amueller/word_cloud)
+ [PyPlot](https://matplotlib.org/)
+ [SciKit-learn](https://scikit-learn.org/stable/)
+ [Seaborn](https://seaborn.pydata.org/)

Native imports are:
+ from os import getenv, listdir, path, walk
+ from pathlib import Path
+ from urllib.parse import quote_plus
+ import random
+ import re
+ import sqlite3
+ import json
+ import functools

## A Note on Users <a name = "users"></a>

I feel it is important to remember that software is made to be used. Often there is a disconnect between what the developer sees when they make it and what the users see when they actually use it. As makers it is our duty to bridge that gap the best we can.

One of the first things I noticed when having people test out the bot was that they had trouble remembering exactly *what* the commands are, or how to spell them. In addition to the usual help commands I have implemented two ways of combating these problems. 

The first and simplest is to alias the commands. For example, if a user wants to get the definition for a word they should be able to enter `!dictionary`, `!dict`, `!definition`, or `!def` with the same end result. Python makes this simple with the use of hash tables and is done as:
`elif args[0] in {'!8ball', '!8', '!eightball', '!eight'}:`

The second part took a little more doing, that is, how to handle what to do when a user forgets how exactly to spell "dictionary". This was a problem I was seeing frequently (but not only) from users whose first language wasn't my own, and whose language's spelling conventions didn't mesh with the often times odd rules of English. Those users would be trying something like `!dikt`, `!deph`, or `!dektionary`. The solution was to implement a basic form of auto-correct, like you might find on your phone. The actual code for this is located in the ./speller/ directory and is a stripped down and modified version of Filip Sondej's project [autocorrect](https://github.com/fsondej/autocorrect). Filip's code is a work of art and I encourage you to peruse it. It works by making clever use of Python's concept of arrays, iterables, permutations, and generators, alongside regular expressions. It takes textual input, splits it into individual words, generates many variations of those words with array slices, and then compares them to a custom built dictionary of word frequency pairs to find the most likely candidate for what the word should be before then reforming and returning the corrected text.

Another notable place that Ease of Use manifested itself is in allowing server administrators to change key values whenever they desire, and to do so quickly. I decided that the best approach would be to have a configuration table within the database and to allow users to interface with it via a JSON file. The use of a drag-and-drop file system allows server adminstrators to keep multiple configurations stored on their own local systems and change between them at any moment. To further the ease of use we modify this file to a more human readable form inbetween its creation from the config table to the user, and its return from the user to the config table. 

When sending the config file to the user we first query the database to see whether or not a config entry already exists. If it does not we create one with default values and try again. Once we are sure a config exists we get the values in a JSON format, use a Python dict (named jsonFormatter here) to replace text into a user friendly form, append a brief explanation of the entries from ./docs/help/config.txt and send it out. This whole process is located in tutil.py and looks like:

```python
jsonFormatter = [[
		['0=', 'Monday = '],
		['1=', 'Tuesday = '],
		['2=', 'Wednesday = '],
		['3=', 'Thursday = '],
		['4=', 'Friday = '],
		['5=', 'Saturday = '],
		['6=', 'Sunday = '],
		[',', ', '],
		[';', '; '],
	],[
		['id', 'Server ID'],
		['guild_name', 'Server Name'],
		['locale', 'Server Locale'],
		['schedule', 'Schedule'],
		['url', 'URL Footer'],
		['quote_format', 'Quote Format'],
		['qAdd_format', 'Quote Added Format'],
		['lore_format', 'Lore Format'],
		['filtered', 'Blacklisted Words'],
		['mod_roles', 'Moderator Roles'],
	]]

def config_create(guild):
	with engine.connect() as conn:
		select_st = select([Config]).where(Config.c.id == guild.id)
		result = conn.execute(select_st).fetchone()
		if result:
			columns = []
			for each in Config.c:
				columns.append(each.name)
			dict_ = dict(zip(columns, result))
			
			#For pretty printing, make the user's life easier
			for each in jsonFormatter[0]:
				dict_['schedule'] = dict_['schedule'].replace(each[0], each[1])
			for each in jsonFormatter[1]:
				dict_[each[1]] = dict_.pop(each[0])
						
			with open('{}/docs/config/{}.json'.format(DEFAULT_DIR, guild.id), 'w') as f:
				json.dump(dict_, f, indent=4)
				f.write('\n\n{}'.format(fetchFile('help', 'config')))	
			return '{}/docs/config/{}.json'.format(DEFAULT_DIR, guild.id)		
		
		else:
			ins = Config.insert().values(
				id = guild.id,
				guild_name = guild.name,
				locale = 'Asia/Tokyo',
				schedule = '0=10,17:15;1=10,12;2=16,10:15;3=2:44;4=10;5=16:30;',
				quote_format = '{0}\n ---{1} on {2}',
				lore_format = '{0}\n ---Scribed by the Lore Master {1}, on the blessed day of {2}',
				url = 'Come hang with us at: <https://www.twitch.tv/>',
				qAdd_format = 'Added:\n "{0}"\n by {1} on {2}',
				filtered = 'none',
				mod_roles = 'mod;admin;discord mod;',
			)		
			conn.execute(ins)
			return config_create(guild)
```

When retrieving the config from the user we simply reverse the process. We first split off the appended help text, load the remaining JSON into a dict, swap the text back into a database friendly format, and connect it to the appropiate table entry.

```python
def config_load(guild):
	with open('{}/docs/config/{}.json'.format(DEFAULT_DIR, guild), 'r') as f:
		dict_ = json.loads(f.read().split('```', maxsplit=1)[0])
	for each in jsonFormatter[1]:		
		dict_[each[0]] = dict_.pop(each[1])
	for each in jsonFormatter[0]:
		dict_['schedule'] = dict_['schedule'].replace(each[1], each[0])
	
	with engine.connect() as conn:
		ins = Config.update().where(Config.c.id == guild).values(
					locale = dict_['locale'],
					schedule = dict_['schedule'],
					quote_format = dict_['quote_format'],
					lore_format = dict_['lore_format'],
					url = dict_['url'],
					qAdd_format = dict_['qAdd_format'],
					filtered = dict_['filtered'],
					mod_roles = dict_['mod_roles'],
					)
		conn.execute(ins)
	modRoles[guild] = fetch_value(guild, 9, ';')
```

## How Stuff Works <a name = "workings"></a>

The general top-level work flow of the bot is very straight forward. It first loads its API tokens for Discord and Wolfram from the local .env file, creates generic connections to the local SQLite database, sets up a local log file to keep track of any errors, and then connects to Discord's servers.

It then watches for a handful of events: 
+ [being invited to a new guild](#join)
+ [a reaction being added to a message](#reaction)
+ [an error](#errors)
+ [or a message being sent](#messages)

### On Joining a Guild <a name = "join"></a>

When the bot joins a guild for the first time we want to hit that first design philosophy and Make Things Easy. So, we send a title image and a welcome message.

There are several events that occur frequently with slight variations, e.g. reading from a file or checking if a user is an administrator. For these common tasks I have created the `tutil.py` file. 

Here we will encounter the call to fetchFile() in tutil.py for the first time of many. This function looks into our ./docs/ directory for a given file in a given directory and simply returns it to be used in our banner. Any time the bot will be displaying content to the end users I refer to it as a banner. I implemented it this way as part of the second core philosophy, Easy to Modify, so that these common messages can be changed on the fly without needing to interrupt service to users by stopping and reloading the entire bot to change internal code. 

```python
@bot.event
async def on_guild_join(guild):
	banner = 'Hello {}! \n{}'.format(guild.owner.mention, fetchFile('help', 'welcome'))
	await guild.system_channel.send(banner, file=discord.File('./docs/header.png'))
```
--->
```python
def fetchFile(directory, filename):
	with open('{}/docs/{}/{}.txt'.format(DEFAULT_DIR, directory, filename), 'r') as f:
		return f.read()
```

This message is sent to the guild's system_channel (by default the first text channel created, though in practice it is often changed by users to a hidden admin channel) and prompts the server owner through basic config setup for the bot.

### On Reactions Added <a name = "reaction"></a>

There are two related instances of when we want the bot to notice a user has added a reaction to a message and take action: to add a new quote, and to remove an existing quote. The Python Discord API provides two similar events for this, on_reaction_add and on_raw_reaction_add. The important difference for us is that the latter allows for users to add messages that were posted at any point in time, even before the bot was added to the server, to the quotes database. This does however mean that we need to fetch the message rather than operating directly with it.

A few additional considerations (that were added after a series of 'interesting' events) are to ensure that the message that is being added was not posted by a bot, that the message is not already in the database, and that the message does not contain any phrases blacklisted by the server (unless the author was themself an administrator). This became the following the code snippet:

```python
@bot.event
async def on_raw_reaction_add(payload): 
	channel = bot.get_channel(payload.channel_id)
	message = await channel.fetch_message(payload.message_id)
	
	#Add a quote
	if str(payload.emoji) == '🗨️' and not message.author.bot:
		if not tquote.checkExists(message.guild.id, message.id):
			if not tfilter.check(message) or is_admin(payload.member):
				await message.channel.send(tquote.insertQuote(None, message))
	
	#Remove a quote
	if str(payload.emoji) == '❌'and is_admin(payload.member): 
		await message.channel.send(tquote.deleteQuote(message.guild.id, message.id))
```

Another lesson that was quickly learned from this was the need to suppress @user and @role mentions, but to do so without stripping the context of the original message. This is done via a standard string match and replace operation before sending it off to the database. From tquote.py:

```python
def insertQuote(Table, message):
...
	text = message.content
	for each in message.mentions:
		text = text.replace('<@!{}>'.format(each.id), each.name)
	for each in message.role_mentions:
		text = text.replace('<@&{}>'.format(each.id), each.name)
...
```

### On Error <a name = "errors"></a>

This aspect is handled entirely by Python's built in `import logging` and PyDiscord's `on_error`. It was important while trying to locate the nitpicky problems users were running into.

```python
@bot.event 
async def on_error(event, *args, **kwargs):
	with open('./log/err.log', 'a') as f:
		if event == 'on_message':
			timestamp = pendulum.now(tz='America/Phoenix').to_datetime_string()
			print(timestamp)
			print('[!] Error in: {}; {}'.format(args[0].channel.name, args[0].guild.name))
			print('[!] Error content: {}'.format(args[0].content))
			print('[!] Error author: {}'.format(args[0].author))
			f.write(f'{timestamp}\nUnhandled message:\n{args[0]}\n\n')
		else:
			raise
			
			
logger = logging.getLogger('discord')
logger.setLevel(logging.WARNING)
handler = logging.FileHandler(filename='./log/discord.log', encoding='utf-8', mode='a')
handler.setFormatter(logging.Formatter('%(asctime)s:%(levelname)s:%(name)s: %(message)s'))
logger.addHandler(handler)	
```

However, during development simple logging was not enough to fully diagnose most issues. For this I turned to Python's decorator functions and dropped a wrapper into tutil.py. Placing `@debug` above any function definition prints out to the terminal what function is being called and its arguments before actually entering into the function, and what that function is returning before breaking back into its parent. A sort of refined stack trace if you will. This looks like:

```python
def debug(func):
    """Print the function signature and return value"""
    @functools.wraps(func)
    def wrapper_debug(*args, **kwargs):
        args_repr = [repr(a) for a in args]
        kwargs_repr = [f"{k}={v!r}" for k, v in kwargs.items()]
        signature = ", ".join(args_repr + kwargs_repr)
        print(f"Calling {func.__name__}({signature})\n")
        value = func(*args, **kwargs)
        print(f"{func.__name__!r} returned {value!r}\n")
        return value
    return wrapper_debug
```

### On Message <a name = "messages"></a>

Whenever a message is posted in a server it triggers the on_message(message) event in main.py. This first checks the author was not a bot, then logs the message in the database, checks if the message was a config file for the server and if so updates as needed, if it looks to be a command it will attempt any needed auto-corrections, do the appropiate operations for a valid command entry, and finally return any needed output.

Upon recognizing a command it forwards the message to a helper function within the related module. The helper function parses any optional parameters and sends them to dict whose keys are the operator and values are lambda designations to functions. This works like a switch in other languages and is how we interace with the modules. The one located in tsched.py is simple and makes for a good example of how these work in all the other modules. 

#### tsched.py

```python
def helper(message):
	args = message.content.split()
	ops = {'get', 'set', 'help', 'override', 'config'}
	operator = 'get' #Set a default operator
	if len(args) > 1 and args[1] in ops:
		operator = args[1]
	return {
		'get': lambda: getSchedule(message),
		'set': lambda: setSchedule(message),
		'help': lambda: getHelp(args, message.author),
		'override': lambda: override(message),
	}.get(operator, lambda: None)()	
```

Such that calls to modules from main.py are a sort of OOP / Functional hybrid and as Easy to Use as:

```python
...			
elif args[0] in {'!schedule', '!sched', '!s'}:
	banner = tsched.helper(message)
...
```

When the bot is first initialized from the command line with `pipenv run python3 main.py` it imports all the local modules, and those that need to access the database call their setup() functions at this point. They all look more or less the same, setting up any default values, as well as creating an engine and MetaData objects for SQLAlchemy linked to appropiate tables. As an example the one for tsched.py is:

```python
def setup():
	global engine, meta, Users, Config
	engine = create_engine('sqlite:///./log/quotes.db', echo = False)
	meta = MetaData()
	Users = Table(
		'schedule', meta,
		Column('id', Integer, primary_key = True),
		Column('name', String),
		Column('locale', String),
		Column('guild', String),
		Column('guild_name', String),
		)
	Config = Table(
		'config', meta,
		Column('id', Integer, primary_key = True),
		Column('guild_name', String),
		Column('locale', String),
		Column('schedule', String),
		Column('quote_format', String),
		Column('lore_format', String),
		Column('url', String),
		Column('qAdd_format', String),
		)
	meta.create_all(engine)
	with open('./docs/locales/abbr.txt', 'r') as f:
		for line in f:
			(key, val) = line.split(',')
			val = val.strip('\n')
			tzAbbrs[key] = val
	print('[+] End Schedule Setup')
```


Most modules also include a standard getHelp(args, author) that checks the context of what kind of help the user is requesting and if the response should include administrative commands or not, and loads them from the relevant ./docs/help file. For Ease of Maintenance and Modifying the full help message is located in a single file and split at the appropiate location within the file, instead of accessing and combining multiple txt files.

```python
def getHelp(args, author):
	if len(args) < 3: #Get general help
		banner = fetchFile('help', 'schedule')
		if not is_admin(author):
			banner = banner.split('For Admins:')[0]
	else: #Get list of cities or continents
		banner = fetchFile('locales', args[2].lower())
	return banner
```

Let's dive into the heart of the schedule code. This is possibly the ugliest section of code in the entire project so please bear with me. The entire function is:

```python
def getSchedule(message):
	config = load_config(message.guild.id)
	if config:
		server_locale = config[2]
		locale = server_locale
		schedRawStr = config[3]
		url = config[6]
			
		args = message.content.split()
		if len(args) > 1: #User requested specific location
			locale = tzAbbrs.get(args[1].lower(), args[1])
		else: #Checking for saved locale in DB
			user = getUser(message.guild.id, message.author.id)
			if user:
				locale = user[2]	

		dt = pendulum.now(tz=locale)
		dtLocalName = dt.timezone.name
		now_in_server = pendulum.now(tz=server_locale)

		#Convert our raw config string from db into a workable array
		days = schedRawStr.split(';')
		dict_ = {}
		schedTime = []
		schedule = []
		hours = [day.split('=') for day in days]
		
		schedule.append(pendulum.now(tz=server_locale))
		
		for each in hours:
			if each[0] != '' and each[1] != '':
				if each[0] != ' ' and each[1] != ' ':
					dict_[int(each[0])] = each[1].split(',')
		for each in dict_.items():
			for hour in each[1]:
				if ':' in hour:
					hour = hour.split(':')
				if hour != '' and hour != ' ':
					schedTime.append(hour)
			schedule.append(pendulum.now(tz=server_locale).add(days=each[0]))

		#Needed for handling partial weeks, ie so we don't post a message with only 1 or 2 days
		scheduleDup = schedule.copy()
		#Show current server time vs current user time
		banner = '{} in {}\n'.format(dt.to_day_datetime_string(), dt.timezone_name)
		banner += '{} in {}\n'.format(now_in_server.to_day_datetime_string(), server_locale)
		banner += divider

		while(schedule[0].day_of_week != pendulum.MONDAY):
			for day in range(len(schedule)):
				schedule[day] = schedule[day].add(days=1)
		
		schedule.pop(0)
				
		#Previous / Current Week
		if now_in_server.day_of_week != pendulum.MONDAY:	
			#Get us to Monday
			while(scheduleDup[0].day_of_week != pendulum.MONDAY):
				for day in range(len(scheduleDup)):
					scheduleDup[day] = scheduleDup[day].add(days=-1)
			
			scheduleDup.pop(0)
			for day in range(len(scheduleDup)):
				if isinstance(schedTime[day], list):
					#Contains minutes
					scheduleDup[day] = scheduleDup[day].at(
						int(schedTime[day][0]), int(schedTime[day][1]))
				else:
					scheduleDup[day] = scheduleDup[day].at(int(schedTime[day]))
				
				#Convert timezone and add to message
				scheduleDup[day] = scheduleDup[day].in_tz(dtLocalName)
				if scheduleDup[day].format('DDDD') >= dt.format('DDDD'):
					if scheduleDup[day].format('DDDD') == dt.format('DDDD'):
						banner += '**{}**\n'.format(scheduleDup[day].to_day_datetime_string())
					else:
						banner += '{}\n'.format(scheduleDup[day].to_day_datetime_string())
		
		#Next Week	
		for day in range(len(schedule)):
			if isinstance(schedTime[day], list):
				#Contains minutes
				schedule[day] = schedule[day].at(
					int(schedTime[day][0]), int(schedTime[day][1]))
			else:
				schedule[day] = schedule[day].at(int(schedTime[day]))
			#Convert timezone and add to message
			schedule[day] = schedule[day].in_tz(dtLocalName)
			if schedule[day].format('DDDD') == dt.format('DDDD'):
				banner += '**{}**\n'.format(schedule[day].to_day_datetime_string())
			else:
				banner += '{}\n'.format(schedule[day].to_day_datetime_string())
				
		banner += '{}{}\n{}'.format(divider, url, divider)
		banner += 'Help pay for server costs: <{}>\n'.format('https://www.patreon.com/tangerinebot')
		banner += 'Invite the bot to your server: <{}>\n'.format('https://discord.com/api/oauth2/authorize?client_id=663696399862595584&permissions=8&scope=bot')
		banner += 'Use `!schedule help` for more information.'

	else:
		banner = 'A schedule has not been setup for this server yet.\n'
		banner += 'An admin may create one with `!config`.' 
	return banner
```

The function starts by grabbing the server's entry in the config table along with the user's entry in the schedule table (if they exist) with:

```python
def load_config(guild):
	with engine.connect() as conn:
		select_st = select([Config]).where(Config.c.id == guild)
		res = conn.execute(select_st)
		result = res.fetchone()
	if result:
		return result
	return None
	

def getUser(guild_, id_):
	with engine.connect() as conn:
	#We do not filter by guild here so that the user's location
	#is preserved across any other servers using the bot
		select_st = select([Users]).where(
			Users.c.id == id_,)
		res = conn.execute(select_st)
		result = res.fetchone()
		if result:
			return result
```

Which will look something like this for the config table:

![config entry](https://i.imgur.com/YVm2fIf.png)

And for the user table:

![user entry](https://i.imgur.com/ix7LXB3.png)

Breaking down the 'schedule' entry in the config table into a list of Pendulum datetime objects. We also create a temporary entry at the beginning of the list.
```python
	days = schedRawStr.split(';')
	dict_ = {}
	schedTime = []
	schedule = []
	hours = [day.split('=') for day in days]
	#Temporary entry
	schedule.append(pendulum.now(tz=server_locale))
	
	for each in hours:
		if each[0] != '' and each[1] != '':
			if each[0] != ' ' and each[1] != ' ':
				dict_[int(each[0])] = each[1].split(',')
	for each in dict_.items():
		for hour in each[1]:
			if ':' in hour:
				hour = hour.split(':')
			if hour != '' and hour != ' ':
				schedTime.append(hour)
		schedule.append(pendulum.now(tz=server_locale).add(days=each[0]))
```

This temporary entry at the 0th index of the list is used because what we are actually doing is creating entries spaced n-days away from today, as supplied by the "0=", "1=", etc portion of the raw schedule string (e.g. 0=10,17:15;1=10,12;2=16,10:15;3=2:44;4=10;5=16:30;). But we want "0=" to actually always be Monday, i.e. "2=" should be spaced 2 days away from Monday aka Wednesday, so we then shift each entry back one day until that temporary entry is Monday. We can then pop the temporary entry from the list.

```python
	while(schedule[0].day_of_week != pendulum.MONDAY):
		for day in range(len(schedule)):
			schedule[day] = schedule[day].add(days=1)
		
	schedule.pop(0)
```

The remainder of the function:
+ loops over the list to set the hour and minute of each day with the calls to `schedule[day].at(schedTime[day])`,
+ sets it the correct timezone with `schedule[day].in_tz(dtLocalName)`,
+ and adds a footer message to the banner before returning

### On Logging
### Project Map
