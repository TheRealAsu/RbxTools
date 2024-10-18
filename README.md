# Bot Controller
This script let you control other instance of roblox with the roblox chat, like admins commands
### requirement
- **Multi-Instance** : You will need a software that let you can open multiple instance of roblox at the same time, you can use [Roblox Account Manager](https://github.com/ic3w0lf22/Roblox-Account-Manager).
- **Multi-Instance Executor** : you need software that allows you to run multiple roblox instances at the same time
- **A decent computer** : You'll need plenty of ram to run several instances of roblox at the same time (16GB).

## Commands

- ;status                              |  check if bots are active
- ;index                               |  show bots' index
- ;follow [plr]                        |  follow someone
;quit                                |  disconnect admins and owner from the script
;dance <number>                      |  make bots dance
;undance                             |  make bots stop dancing
;reset                               |  make bots reset
;jump                                |  make bots jump
;say <sentence>                      |  make bots say something
;unfollow                            |  unfollow the player that the bots are following
;orbit [plr] <radius> <speed>        |  orbit around someone V1 (normal orbit)
;orbit2 [plr] <radius> <speed>       |  orbit around someone V2 (cooler)
;orbit3 [plr] <radius> <speed>       |  orbit around someone V3
;orbit4 [plr] <radius> <speed>       |  orbit around someone V4
;orbit5 [plr] <radius> <speed>       |  orbit around someone V5
;orbit6 [plr] <radius> <speed>       |  orbit around someone V6 (chaotic)
;unorbit                             |  stop bots from orbiting
;goto [plr]                          |  teleport bots to a player
;align                               |  make a line with the bots
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

## Bot Controller boot

```lua
--[[

▀█████████▄  ▄██   ▄           ▄████████    ▄████████ ███    █▄  
  ███    ███ ███   ██▄        ███    ███   ███    ███ ███    ███ 
  ███    ███ ███▄▄▄███        ███    ███   ███    █▀  ███    ███ 
 ▄███▄▄▄██▀  ▀▀▀▀▀▀███        ███    ███   ███        ███    ███ 
▀▀███▀▀▀██▄  ▄██   ███      ▀███████████ ▀███████████ ███    ███ 
  ███    ██▄ ███   ███        ███    ███          ███ ███    ███ 
  ███    ███ ███   ███        ███    ███    ▄█    ███ ███    ███ 
▄█████████▀   ▀█████▀         ███    █▀   ▄████████▀  ████████▀  
                                                                 
@thereal_asu                                      

]]

--Configuration
local bots = {"Asu_Bot1", "Asu_Bot2", "Asu_Bot3", "Asu_Bot4", "Asu_Bot5", "Asu_Bot6"} --USE DISPLAY NAME
local owner = "TheReal_Asu2" --Owner
local nbbot = 6 -- Number of bot.s you want to use
local prefix = ";" --Prefix
local botrender = true --when false, bots use less cpu

--[[
INFO:

- do ;quits to deactivate the script
- activate script only once
- you can check whether bots are active by doing ;status
- if the bots don't execute the command, you'll have to redo the command until it's executed.
- put the bots you want to use in the places of the list. 

--

args:
[plr] = player (you don't need to put the full username or display name of someone to make it work)
<number> = need to be a number to make it work
(string) = word or a setence

--

;status                              |  check if bots are active
;index                               |  show bots' index
;follow [plr]                        |  follow someone
;quit                                |  disconnect admins and owner from the script
;dance <number>                      |  make bots dance
;undance                             |  make bots stop dancing
;reset                               |  make bots reset
;jump                                |  make bots jump
;say <sentence>                      |  make bots say something
;unfollow                            |  unfollow the player that the bots are following
;orbit [plr] <radius> <speed>        |  orbit around someone V1 (normal orbit)
;orbit2 [plr] <radius> <speed>       |  orbit around someone V2 (cooler)
;orbit3 [plr] <radius> <speed>       |  orbit around someone V3
;orbit4 [plr] <radius> <speed>       |  orbit around someone V4
;orbit5 [plr] <radius> <speed>       |  orbit around someone V5
;orbit6 [plr] <radius> <speed>       |  orbit around someone V6 (chaotic)
;unorbit                             |  stop bots from orbiting
;goto [plr]                          |  teleport bots to a player
;align                               |  make a line with the bots
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


]]
```
