# dj-doomer
Discord music bot that plays music from YouTube

Documentation for Discord Music Bot
This documentation provides an overview of the functionalities and components of the music bot script using discord.py, yt_dlp, and dotenv. The bot can play, pause, resume, and stop music in a Discord voice channel.

1. Imports
The script imports the following libraries:

discord: Main library for creating the Discord bot.
os: Used to access environment variables.
asyncio: Handles asynchronous operations.
yt_dlp: Downloads and extracts media information from YouTube.
dotenv: Loads environment variables from a .env file.
2. Environment Setup
The load_dotenv() function loads the discord_token variable from a .env file. The bot token is used to authenticate the bot.

python
Copy code
load_dotenv()
TOKEN = os.getenv('discord_token')
3. Discord Client Initialization
The bot uses the discord.Client class with intents to enable specific permissions:

intents.message_content: Required to read message content.
python
Copy code
intents = discord.Intents.default()
intents.message_content = True
client = discord.Client(intents=intents)
4. Global Variables
queues: (Not implemented) Placeholder for managing song queues.
voice_clients: Stores active voice connections for each guild.
yt_dl_options: Options for yt_dlp to extract audio.
ffmpeg_options: Options for streaming audio with FFmpeg, including volume control.
5. Bot Events
5.1 on_ready()
Logs a message to the console when the bot is ready:

python
Copy code
@client.event
async def on_ready():
    print(f'{client.user} is now jamming')
5.2 on_message()
Handles user commands:

Command: ?play <URL>
Connects the bot to the user's voice channel.
Downloads and streams audio from the given URL.
Plays the audio in the voice channel.
Command: ?pause
Pauses the currently playing audio.

Command: ?resume
Resumes the paused audio.

Command: ?stop
Stops the audio playback and disconnects the bot from the voice channel.

Example Implementation:
python
Copy code
@client.event
async def on_message(message):
    if message.content.startswith("?play"):
        # Connect to the voice channel
        try:
            voice_client = await message.author.voice.channel.connect()
            voice_clients[voice_client.guild.id] = voice_client
        except Exception as e:
            print(e)
        
        # Stream the audio
        try:
            url = message.content.split()[1]
            loop = asyncio.get_event_loop()
            data = await loop.run_in_executor(None, lambda: ytdl.extract_info(url, download=False))
            song = data['url']
            player = discord.FFmpegOpusAudio(song, **ffmpeg_options)
            voice_clients[message.guild.id].play(player)
        except Exception as e:
            print(e)
6. Error Handling
Each command uses try...except blocks to catch and print errors during execution (e.g., connection issues, playback errors).

7. Running the Bot
The bot is started using client.run(TOKEN):

python
Copy code
client.run(TOKEN)
8. Prerequisites
Install dependencies:
bash
Copy code
pip install discord.py yt-dlp python-dotenv
FFmpeg:
Ensure FFmpeg is installed and available in your system's PATH.
9. .env File Example
The .env file should contain:

env
Copy code
discord_token=YOUR_DISCORD_BOT_TOKEN
10. Known Limitations
No Queue Management: The bot doesn’t queue songs; it plays one at a time.
Error Logging: Errors are only printed to the console.
Voice Connection Handling: The bot doesn’t check for existing connections before reconnecting.
This bot provides basic functionality for streaming music in Discord voice channels and can be expanded with features like playlists, song skipping, and dynamic volume control.
