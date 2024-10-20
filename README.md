# Asu's Bot Controller FE V0.2.1
This script let you control other instance of roblox with the roblox chat, like admins commands
## requirement
- **Multi-Instance** : You will need a software that let you open multiple instance of roblox at the same time, you can use [Roblox Account Manager](https://github.com/ic3w0lf22/Roblox-Account-Manager).
- **Multi-Instance Executor** : you need a software that allows you to run multiple roblox instances at the same time
- **A decent computer** : You'll need plenty of ram to run several instances of roblox at the same time (16GB).

## want to recieve news or need help?
Discord: https://discord.gg/zrAB2m5gvz

## How it work ?
You need to put the displayname of your bot in the bots table, put your name in the owner variable, and the number of bot you want to use in nbbot variable. When you run it, the script will check whether the displayname of the player executing this script is in the bots table. If so, he becomes a bot and will perform various actions according to the commands. Bots will listen to admin and owner chats.

## Commands

;status                              |  check if bots are active
;index                               |  show bots' index
;follow [plr]                        |  follow someone
;quit                                |  disconnect admins and owner from the script
;dance <number>                      |  make bots dance
;undance                             |  make bots stop dancing
;reset                               |  make bots reset
;jump                                |  make bots jump
;say (sentence)                      |  make bots say something
;unfollow                            |  unfollow the player that the bots are following
;orbit [plr] <radius> <speed>        |  orbit around someone V1 (normal orbit)
;orbit2 [plr] <radius> <speed>       |  orbit around someone V2 (cooler)
;orbit3 [plr] <radius> <speed>       |  orbit around someone V3
;orbit4 [plr] <radius> <speed>       |  orbit around someone V4
;orbit5 [plr] <radius> <speed>       |  orbit around someone V5
;orbit6 [plr] <radius> <speed>       |  orbit around someone V6 (chaotic)
;unorbit                             |  stop bots from orbiting
;goto [plr]                          |  teleport bots to a player
;align [plr]                         |  make a line with the bots
;ws <number>                         |  change bots' walk speed
;loopjump                            |  make bots jump in a loop
;unloopjump                          |  stop the jump loop
;circle <number>                     |  make bots form a circle around you
;channel <number>                    |  change the bot that says the messages
;worm [plr]                          |  make a worm/train/snake formation with bots
;unworm                              |  stop the worm/train/snake formation
;spin <number>                       |  make bots spin
;unspin                              |  make bots stop spinning
;admin [plr]                         |  give admin to someone, users with admin permission will be allowed to control the bots
;arch <number>                       |  make a half-circle with the bots
;stalk [plr]                         |  follow someone and walk around them
;unstalk                             |  stop following someone and walking around them
;help                                |  chat all available commands
;tower [plr]                         |  makes a tower of bots
;untower                             |  undo the tower
;fix                                 |  try to fix the bot if glitched

## to Do
- somme more funny commands
- improve script logics
  
## to fix
- ;unworm does not execute correctly
- fix ;admin and rework it because it's broken
- make bots listen better to chat
  
## Bot Controller script

```lua
--[[
Asu's Bot Controller FE V0.2

▀█████████▄  ▄██   ▄           ▄████████    ▄████████ ███    █▄  
  ███    ███ ███   ██▄        ███    ███   ███    ███ ███    ███ 
  ███    ███ ███▄▄▄███        ███    ███   ███    █▀  ███    ███ 
 ▄███▄▄▄██▀  ▀▀▀▀▀▀███        ███    ███   ███        ███    ███ 
▀▀███▀▀▀██▄  ▄██   ███      ▀███████████ ▀███████████ ███    ███ 
  ███    ██▄ ███   ███        ███    ███          ███ ███    ███ 
  ███    ███ ███   ███        ███    ███    ▄█    ███ ███    ███ 
▄█████████▀   ▀█████▀         ███    █▀   ▄████████▀  ████████▀  
                                                                 
@thereal_asu

server discord
https://discord.gg/zrAB2m5gvz                                  
]]

--Configuration
getgenv().Use_Displayname = true -- if true, put accounts displayname for bots | if false use the username of accounts
getgenv().bots = {"Asu_Bot1", "Asu_Bot2", "Asu_Bot3", "Asu_Bot4", "Asu_Bot5", "Asu_Bot6"} --bots
getgenv().owner = "TheReal_Asu2" --Owner (USER NAME, DO NOT PUT DISPLAYNAME)
getgenv().nbbot = 6 -- Number of bots you want to use
getgenv().prefix = ";" -- Prefix
getgenv().botrender = false -- when false, bots use less CPU
getgenv().printcmd = true -- if true, displays all commands available in the console

loadstring(game:HttpGet('https://raw.githubusercontent.com/TheRealAsu/RbxTools/refs/heads/main/Bot%20Controller%20Script'))()
--[[
INFO:

- do ;quits to deactivate the script
- activate script only once
- you can check whether bots are active by doing ;status
- if the bots don't execute the command, you'll have to redo the command until it's executed.
- put the bots you want to use in the places of the list. 

-------------------------------------------------------------------

args:
[plr] = player (you don't need to put the full username or display name of someone to make it work)
<number> = need to be a number to make it work
(string) = word or a setence
]]
```
### Version 0.2.1
