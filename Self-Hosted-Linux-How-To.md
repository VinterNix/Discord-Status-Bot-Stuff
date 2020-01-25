# Self-Hosted Linux Instructions

This instruction set has been created while using the CentOS operating system. While the instructions are similar, commands will vary per OS. Please refer to your Distro’s Help KB’s for assistance.

If you require any assistance please join our **[Discord Support Server](https://discord.gg/aMDa2TB)**

(This guide assumes you know the basic operation and securement of a linux os and thus does not refer or offer steps on how to do so)


Download the bot `wget https://cdn.movinto.net/discord-statusbot/”***-discord-statusbot-linux-amd64.zip”`


Extract contents `unzip -a ***-discord-statusbot-linux-amd64.zip`


Create your **[Discord App](https://discordapp.com/developers)** & Edit the configuration file as required.


Run your bot with `./discord-statusbot -config /config.json`



	#Auto-Start/Start-On-Boot/Restart-On-Failure

To get real fancy, you can setup the bot to take advantage of the systemctl to restart, start/stop and auto-start upon failure. This will also enable background usage as a non-root user. This is real easy and we have already created the scripting needed to complete this.

(This setup will also allow you to run multiple instances without needing multiple installs of the bot)

Create a non-root user, in this case we will use: “statusbot” `adduser statusbot`
(If you do NOT intend to move files to the new user’s home directory, you can use the “-M” after “adduser” to prevent the creation of a home directory)


Let’s lock the account to prevent ssh logins: `usermod -L statusbot`


Give ownership of the bot’s files to our new user: `chown -R statusbot:statusbot /path/to/bot/folder`


**[Download/Copy](https://github.com/VinterNix/Discord-Status-Bot-Stuff/blob/master/startscript.sh)** the bash file to tell the system what to execute.


Upload/Create it where you would like. To keep it simple, upload it to the same directory your bot’s files are located.
Edit the file as needed with your file paths.


Make the script executable `chmod -x startscript.sh`


**[Download/Copy](https://github.com/VinterNix/Discord-Status-Bot-Stuff/blob/master/statusbot%40.service)** the systemctl service file.


Upload/Create it here: `/etc/systemd/system` 


Edit all the paths to reflect your setup. If you do not update the paths in this file, bad things could happen or you will receive errors during startups.


Assuming you have kept the same file names throughout this installation, use the following commands to activate the service file.

(Make sure you update the following commands with the name of the config file you want the bot to run…..WITHOUT the “.json”)

For every instance of the bot, you must create a NEW config file and repeat the following steps:

*These commands must be run as root

1. `systemctl enable statusbot@config`
2. `systemctl daemon-reload`
3. `systemctl start statusbot@config`

And you are done! If you require any assistance please join our **[Discord Support Server](https://discord.gg/aMDa2TB)**

