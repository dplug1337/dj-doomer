Discord Music Bot 🎵
A simple Discord bot that plays music using YouTube links. The bot ensures a clean chat experience by updating its messages instead of spamming new ones.

Features
Play Music: Stream audio from YouTube links using ?play <URL>.
Pause/Resume Playback: Use ?pause and ?resume to control playback.
Stop Playback: Use ?stop to stop the music and disconnect the bot.
Clean Chat: The bot updates a single message for each command to prevent chat spam.
Commands
Command	Description
?play <URL>	Plays the audio from the given YouTube link.
?pause	Pauses the current song.
?resume	Resumes playback of the paused song.
?stop	Stops playback and disconnects the bot.
Setup
Clone the repository and install dependencies:
bash
Copy code
git clone https://github.com/your-repo/discord-music-bot.git
cd discord-music-bot
pip install -r requirements.txt
Create a .env file in the project directory and add your Discord bot token:
env
Copy code
discord_token=YOUR_DISCORD_BOT_TOKEN
Run the bot:
bash
Copy code
python bot.py
Dependencies
discord.py
yt-dlp
python-dotenv
How It Works
The bot listens for commands starting with ?.
For ?play, it streams audio directly from YouTube using yt-dlp and FFmpeg.
The bot updates the same message for processing, playback, or error status, keeping the chat clean.
Feel free to customize the placeholders like "your-repo" or "YOUR_DISCORD_BOT_TOKEN" with your actual values!
