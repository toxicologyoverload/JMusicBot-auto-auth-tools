# JMusicBot-auto-auth-tools
This repository contains a couple of shell scripts to make the deployment of the "YouTube trusted session" patched [JMusicBot](https://github.com/jagrosh/MusicBot) easier.

Please also note this repository does not handle setting up IP rotation.


## Credit
These scripts use a version of [JMusicBot](https://github.com/jagrosh/MusicBot) compiled by [MichailiK](https://github.com/MichailiK) specifically based on this branch [9ec21bf](https://github.com/MichailiK/MusicBot/commit/9ec21bf3297e2056b6271813ecf151cd888d1dab).
<br> This project also utilises and installs [Docker]() and [youtube-trusted-session-generator](https://github.com/iv-org/youtube-trusted-session-generator).

## Instructions
This repository will only work on **x86-64 Linux Debian** based systems and has been tested as working on **ubuntu-24.04.1-live-server-amd64**.

### Step 1
In a clean Directory with no existing [JMusicBot](https://github.com/jagrosh/MusicBot) installation, git clone the repository: <br>
```git clone https://github.com/toxicologyoverload/JMusicBot-auto-auth-tools.git```
<br>
Next enter the repo:
``cd JMusicBot-auto-auth-tools/``

### Step 2
Run the "inital_setup.sh" shell script and follow prompts in terminal:<br>
``./inital_setup.sh``
<br> After Java has finished installing it will prompt for "Bot Token" and then for "Owner User ID", please follow the instructions from JMusicBot on getting [Bot Tokens](https://github.com/jagrosh/MusicBot/wiki/Getting-a-Bot-Token) and [UserIDs](https://github.com/jagrosh/MusicBot/wiki/Finding-Your-User-ID) to get this information.
<br>

After you have done this successfully and you see the following output ```[INFO] [Settings]: serversettings.json will be created in JMusicBot-auto-auth-tools/serversettings.json ``` if this is the case then exit out of the bot, in most cases this will be ``Ctrl+C``.

### Step 3
Next run ``./setup_auth.sh`` following any prompts in the terminal (This might take a while to run).

when its finished the ouput should look somthing like this:
```
Status: Downloaded newer image for quay.io/invidious/youtube-trusted-session-generator:latest
[INFO] internally launching GUI (X11 environment)
[INFO] starting Xvfb
[INFO] launching chromium instance
visitor_data: <contains data>
po_token: <contains token>
successfully removed temp profile /tmp/tmpltg5y6
```
Where <contains data\> and <contains token\> will contain some strings of characters, save both of these for the next step.

### Step 4

open your config.txt file and find the following lines:
```
// This sets the "Proof of Origin Token" and visitor data to use when playing back YouTube videos.
// It is recommend to obtain a PO token to avoid getting IP banned from YouTube.

ytpotoken = "PO_TOKEN_HERE"
ytvisitordata = "VISITOR_DATA_HERE"
```
Replace the "PO_TOKEN_HERE" with the string from "<contains token\>" and replace "VISITOR_DATA_HERE" with the string from "<contains data\>" from the previous step.

### Step 5
Make sure you have added your bot to a server you are in and run    ```./startbot.sh``` and it should now work!

Please note that if you need to regenerate your visitor_data and po_token again in future you only need to run: ```sudo docker run quay.io/invidious/youtube-trusted-session-generator```.

## Optional
If you want to prevent the bot messaging you about versions open the config.txt and find ```updatealerts=true``` and change it to false and restart your bot.