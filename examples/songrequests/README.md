# SongRequests

A sample project using Revlo's API to trigger Nightbot's !songs command.

This sample project allows you to run a secondary bot/account in your chat, which will trigger the !songs command on Nightbot upon a Revlo reward redemption. This allows you to restrict the !songs command to moderators in your channel, but allow regular viewers to redeem it for points through a Revlo reward.

To run this program you need:
- `python3` installed on your machine
- a Twitch account which will send !song commands to NightBot

## Install Instructions

* Open your terminal or Powershell and clone the project
```
git clone git://github.com/teamrevlo/revlo-python-client.git
cd revlo-python-client
pip install -r requirements.txt
```
* Retrieve your Revlo API Key by going to your account settings page.  [Revlo > Account Settings > API](https://www.revlo.co/settings/api)
* Find the reward\_id that belongs to your song request reward. You can get the id for each reward by pinging the rewards endpoint:
```
curl -H "x-api-key: $REVLO_API_KEY" https://api.revlo.co/1/rewards
```
* Deploy [Nightbot](https://beta.nightbot.tv) on your channel.
* Enable the `!songs` command on Nightbot & restrict it to moderators only.
* Retrieve your OAuth token. You can generate one with this [Twitch Chat Oauth Generator](http://twitchapps.com/tmi/). Sign in with the account you want posting !song requests in chat.
* Make a copy of config.sample.yml in the same folder with the filename `config.yml`. Your config.ini file should look something like this:
```
[revlo]
api_key=$REVLO_API_KEY
reward_id=$SONG_REQUEST_REWARD_ID

[twitch]
password=oauth:$OAUTH_TOKEN
channel=$YOUR_TWITCH_USERNAME
username=$YOUR_TWITCH_USERNAME
server=irc.chat.twitch.tv
port=6667
```

## Run instructions

* In your Terminal/Powershell, enter this command to start up the secondary bot
```
cd revlo-python-client/examples/songrequests
python song_requests.py
```

Then try redeeming your song request reward on Revlo & see if the command is posted in chat.
