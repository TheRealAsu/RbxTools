--get configs
local Use_Displayname = getgenv().Use_Displayname
local bots = getgenv().bots
local owner = getgenv().owner
local nbbot = getgenv().nbbot
local prefix = getgenv().prefix
local botrender = getgenv().botrender
local printcmd = getgenv().printcmd
local versionfromconfig = getgenv().version

-- cmd, bool and stuff
local cmdstatus = true
local cmdindex = true
local cmdfollow = true
local cmdquit = true
local cmddance = true
local cmdundance = true
local cmdreset = true
local cmdjump = true
local cmdsay = true
local cmdunfollow = true
local cmdreset = true
local cmdorbit = true
local cmdunorbit = true
local cmdgoto = true
local cmdalign = true
local cmdws = true
local cmdloopjump = true
local cmdunloopjump = true
local cmdcircle = true
local cmdchannel = true
local cmdworm = true
local cmdunworm = true
local cmdspin = true
local cmdunspin = true
local cmdadmin = true
local cmdarch = true
local cmdorbit2 = true
local cmdorbit3 = true
local cmdorbit4 = true
local cmdorbit5 = true
local cmdorbit6 = true
local cmdstalk = true
local cmdunstalk = true
local cmdhelp = true
local cmdtower = true
local cmduntower = true
local cmdfix = true

local towerbool = nil
local followbool = nil
local orbitbool = nil
local orbitbool2 = nil
local orbitbool3 = nil
local orbitbool4 = nil
local orbitbool5 = nil
local orbitbool6 = nil
local alignoffset = nil
local booljump = nil
local indexcircle = nil
local distance = nil
local channel = 1
local wormbool = nil
local boolspin = nil
local adminbool = nil
local stalkbool = nil
local Admins = {}

--version of the script
print("Asu's bot controller VERSION: 0.2.1")

--print cmds in console
if printcmd then
print("Asu's Bot Controller")
print("-------------------------------------------------------------------")
print("args:")
print("[plr] = player (you don't need to put the full username or display name of someone to make it work)")
print("<number> = need to be a number to make it work")
print("(string) = word or a sentence")
print("-------------------------------------------------------------------")
print(";status                              |  check if bots are active")
print(";index                               |  show bots' index")
print(";follow [plr]                        |  follow someone")
print(";quit                                |  disconnect admins and owner from the script")
print(";dance <number>                      |  make bots dance")
print(";undance                             |  make bots stop dancing")
print(";reset                               |  make bots reset")
print(";jump                                |  make bots jump")
print(";say (sentence)                      |  make bots say something")
print(";unfollow                            |  unfollow the player that the bots are following")
print(";orbit [plr] <radius> <speed>        |  orbit around someone V1 (normal orbit)")
print(";orbit2 [plr] <radius> <speed>       |  orbit around someone V2 (cooler)")
print(";orbit3 [plr] <radius> <speed>       |  orbit around someone V3")
print(";orbit4 [plr] <radius> <speed>       |  orbit around someone V4")
print(";orbit5 [plr] <radius> <speed>       |  orbit around someone V5")
print(";orbit6 [plr] <radius> <speed>       |  orbit around someone V6 (chaotic)")
print(";unorbit                             |  stop bots from orbiting")
print(";goto [plr]                          |  teleport bots to a player")
print(";align [plr]                         |  make a line with the bots")
print(";ws <number>                         |  change bots' walk speed")
print(";loopjump                            |  make bots jump in a loop")
print(";unloopjump                          |  stop the jump loop")
print(";circle <number>                     |  make bots form a circle around you")
print(";channel <number>                    |  change the bot that says the messages")
print(";worm [plr]                          |  make a worm/train/snake formation with bots")
print(";unworm                              |  stop the worm/train/snake formation")
print(";spin <number>                       |  make bots spin")
print(";unspin                              |  make bots stop spinning")
print(";admin [plr]                         |  give admin to someone, users with admin permission will be allowed to control the bots")
print(";arch <number>                       |  make a half-circle with the bots")
print(";stalk [plr]                         |  follow someone and walk around them")
print(";unstalk                             |  stop following someone and walking around them")
print(";help                                |  chat all available commands")
print(";tower [plr]                         |  makes a tower of bots")
print(";untower                             |  undo the tower")
print(";fix                                 |  try to fix the bot if glitched")
end

-- Services
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local TextChatService = game:GetService("TextChatService")
local VirtualUser = game:GetService("VirtualUser")

local player = game.Players.LocalPlayer
local displayName = player.DisplayName
local user = player.Name
local offset = math.random(0, 360)

local ownerPlayer = game.Players:FindFirstChild(owner)
local adminNotConnected = {}

-- index bot
local index

if Use_Displayname then
  for i, bot in ipairs(bots) do
    if displayName == bot then
      index = i
      break
    end
  end
else
  for i, bot in ipairs(bots) do
    if user == bot then
      index = i
      break
    end
  end
end

-- don't mess with it
if index then
    indexcircle = (360 / nbbot * index)
end

--disable/enable render (less cpu usage)
if index and botrender then
  RunService:Set3dRenderingEnabled(false)
else
  RunService:Set3dRenderingEnabled(true)
end

-- Isindex
if not index then
  if player.Name == owner then
  else
    warn("No bot or owner corresponding with: " .. table.concat(bots, ", ") .. " or " .. owner .. " for this instance.")
    return
  end
end

-- Chat message
local function chatMessage(str)
  str = tostring(str)
  if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
    TextChatService.TextChannels.RBXGeneral:SendAsync(str)
  else
    game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(str, "All")
  end
end

-- make life easy, with this you don't have to type someone's whole name
local function findPlayerByName(partialName)
  if partialName:lower() == "me" then
    return game.Players:FindFirstChild(owner)
  end

  if partialName:lower() == "random" then
    local players = game.Players:GetPlayers()
    if #players > 0 then
      return players[math.random(1, #players)]
    end
  end

  local bestMatch = nil
  local bestMatchScore = 0

  for _, plr in pairs(game.Players:GetPlayers()) do
    local nameMatch = plr.Name:lower():find(partialName:lower())
    local displayNameMatch = plr.DisplayName:lower():find(partialName:lower())

    if nameMatch or displayNameMatch then
      local score = (nameMatch and #plr.Name or 0) + (displayNameMatch and #plr.DisplayName or 0)
      if score > bestMatchScore then
        bestMatchScore = score
        bestMatch = plr
      end
    end
  end

  return bestMatch
end

--no more bots flinging away with this
local function removeVelocity()
  for _, v in pairs(player.Character:GetDescendants()) do
      if v:IsA("BasePart") then
          v.Velocity = Vector3.new(0, 0, 0)
          v.RotVelocity = Vector3.new(0, 0, 0)
      elseif v:IsA("BodyVelocity") then
          v.Velocity = Vector3.new(0, 0, 0)
      elseif v:IsA("BodyAngularVelocity") then
          v.AngularVelocity = Vector3.new(0, 0, 0)
      elseif v:IsA("BodyPosition") then
          v.Position = v.Position
      elseif v:IsA("BodyGyro") then
          v.CFrame = v.CFrame
      end
  end
end

-- this function make the script a bit more smarter
local function disablebool()
towerbool = false
followbool = false
orbitbool = false
orbitbool2 = false
orbitbool3 = false
orbitbool4 = false
orbitbool5 = false
orbitbool6 = false
booljump = false
wormbool = false
boolspin = false
stalkbool = false
end

-- ;fix
local function fix()
removeVelocity()
towerbool = false
followbool = false
orbitbool = false
orbitbool2 = false
orbitbool3 = false
orbitbool4 = false
orbitbool5 = false
orbitbool6 = false
booljump = false
wormbool = false
boolspin = false
stalkbool = false
game.Workspace.Gravity = 196.2
player.Character:BreakJoints()
end
-- ;circle
local function tpcircle(distance)
  if distance == 0 then
    distance = 0.0001 -- yes because you can't divide by 0
  end

  local targetPlayer = Players:FindFirstChild(owner)
  if not targetPlayer or not targetPlayer.Character then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  local player = Players.LocalPlayer
  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter:FindFirstChild("HumanoidRootPart")
  if not playerHumanoidRootPart then
    return
  end

  removeVelocity()
  local angle = math.rad(0 + indexcircle)
  local offsetX = distance * math.cos(angle)
  local offsetZ = distance * math.sin(angle)
  local newPosition = targetHumanoidRootPart.Position + Vector3.new(offsetX, 0, offsetZ)
  local newCFrame = CFrame.new(newPosition, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = newCFrame
end

-- ;arch
local function tparch(distance)
  if distance == 0 then
    distance = 0.0001
  end

  local targetPlayer = Players:FindFirstChild(owner)
  if not targetPlayer or not targetPlayer.Character then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end
  
  local player = Players.LocalPlayer
  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter:FindFirstChild("HumanoidRootPart")
  if not playerHumanoidRootPart then
    return
  end
  
  removeVelocity()
  local angle = math.rad(0 + (indexcircle)/2)
  local offsetX = distance * math.cos(angle)
  local offsetZ = distance * math.sin(angle)
  local newPosition = targetHumanoidRootPart.Position + Vector3.new(offsetX, 0, offsetZ)
  local newCFrame = CFrame.new(newPosition, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = newCFrame
end

-- ;align
local function align(targetPlayer)
  if not targetPlayer or not targetPlayer.Character then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  if player and player.Character then
    local localHumanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
    if localHumanoidRootPart then

      removeVelocity()
      local offset = targetHumanoidRootPart.CFrame.RightVector * -5 * index  -- NEGATIVE IS LEFT, change this if you want it to go right
      localHumanoidRootPart.CFrame = targetHumanoidRootPart.CFrame + offset
    end
  end
end

-- ;goto
local function goto(targetPlayer)
  if not targetPlayer or not targetPlayer.Character then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  if player and player.Character then
    local localHumanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
    if localHumanoidRootPart then
      removeVelocity()
      localHumanoidRootPart.CFrame = targetHumanoidRootPart.CFrame + Vector3.new(0, 0, 0)
    end
  end
end

-- ;tower
local function tower(targetPlayer)
  if not targetPlayer or not targetPlayer.Character then
      return
  end

  local targetHumanoidRootPart = targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
      return
  end

  towerbool = true

  local heartbeatConnection
  heartbeatConnection = RunService.Heartbeat:Connect(function()
      if not towerbool or not targetHumanoidRootPart or not targetPlayer.Character then
          heartbeatConnection:Disconnect()
          return
      end

      if player and player.Character then
          local localHumanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")
          if localHumanoidRootPart then
              local offset = targetHumanoidRootPart.CFrame.UpVector * 5 * index
              localHumanoidRootPart.CFrame = targetHumanoidRootPart.CFrame + offset

              removeVelocity()
          end
      end
  end)
end

-- ;follow
local function followPlayer(targetPlayer)
  if targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    while followbool and targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") do
      local humanoidRootPart = targetPlayer.Character.HumanoidRootPart
      player.Character.Humanoid:MoveTo(humanoidRootPart.Position)
      wait(0.1)
    end
  else
    warn("Target player or their character is not valid.")
  end
end

-- ;spin from IY
local function spin(spinSpeed)
  local character = player.Character or player.CharacterAdded:Wait()

  local root = character:FindFirstChild("HumanoidRootPart")

  if root then
    local existingSpin = root:FindFirstChild("Spinning")
    if existingSpin then
      existingSpin:Destroy()
    end

    local Spin = Instance.new("BodyAngularVelocity")
    Spin.Name = "Spinning"
    Spin.Parent = root
    Spin.MaxTorque = Vector3.new(0, math.huge, 0)
    Spin.AngularVelocity = Vector3.new(0, spinSpeed, 0)

    while boolspin do
      wait(0.1)
    end

    Spin:Destroy()
  end
end

-- ;worm
local function worm(msgtarget2)
  local displayName = player.DisplayName
  local indexworm = table.find(bots, displayName)

  if not indexworm then
    return
  end

  if indexworm > 1 then
    local targetBotName = bots[indexworm - 1]
    local targetPlayer = findPlayerByName(targetBotName)
    if targetPlayer then
      wormbool = true

      while  wormbool and targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") do
        local humanoidRootPart = targetPlayer.Character.HumanoidRootPart
        player.Character.Humanoid:MoveTo(humanoidRootPart.Position)
        wait(0.1)
      end
    else
    end
  else

    if msgtarget2 and msgtarget2.Character and msgtarget2.Character:FindFirstChild("HumanoidRootPart") then
      followbool = true
      while followbool and msgtarget2 and msgtarget2.Character and msgtarget2.Character:FindFirstChild("HumanoidRootPart") do
        local humanoidRootPart = msgtarget2.Character.HumanoidRootPart
        player.Character.Humanoid:MoveTo(humanoidRootPart.Position)
        wait(0.1)
      end
    else
    end
  end
end

-- ;orbit from IY but modified
local function orbitPlayer(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  removeVelocity()
  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(0, math.rad(rotation), 0) -- if you are bored try to mess with values
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;orbit2
local function orbitPlayer2(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool2 or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  removeVelocity()
  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(math.rad(rotation), math.rad(rotation), 0)
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;orbit3
local function orbitPlayer3(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  removeVelocity()
  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool3 or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(math.rad(rotation), math.rad(rotation), math.rad(rotation))
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;orbit4
local function orbitPlayer4(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  removeVelocity()
  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool4 or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(math.rad(rotation),0, math.rad(rotation))
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;orbit5
local function orbitPlayer5(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool5 or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  removeVelocity()
  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(math.rad(math.random(0, 360)), math.rad(math.random(0, 360)), math.rad(math.random(0, 360)))
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;orbit6
local function orbitPlayer6(targetPlayer, speed, r)
  game.Workspace.Gravity = 0

  if r == 0 then
    r = 0.0001
  end

  local playerCharacter = player.Character
  local playerHumanoidRootPart = playerCharacter and playerCharacter:FindFirstChild("HumanoidRootPart")

  if not playerHumanoidRootPart then
    return
  end

  local targetHumanoidRootPart = targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart")
  if not targetHumanoidRootPart then
    return
  end

  local rotation = indexcircle
  local orbitConnection
  orbitConnection = RunService.Heartbeat:Connect(function()
  if not orbitbool6 or not targetPlayer or not targetPlayer.Character or not targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    orbitConnection:Disconnect()
    return
  end

  removeVelocity()
  local newCFrame = CFrame.new(targetHumanoidRootPart.Position)
  * CFrame.Angles(math.rad(math.random(0, 360)), math.rad(math.random(0, 360)), 0)
  * CFrame.new(r, 0, 0)
  playerHumanoidRootPart.CFrame = newCFrame
  local lookAtCFrame = CFrame.new(playerHumanoidRootPart.Position, targetHumanoidRootPart.Position)
  playerHumanoidRootPart.CFrame = lookAtCFrame
  rotation = (rotation + speed) % 360
  end)
end

-- ;stalk
local function stalkPlayer(targetPlayer)
  if targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
    while stalkbool and targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") do
      local humanoidRootPart = targetPlayer.Character.HumanoidRootPart
      local botHumanoidRootPart = player.Character:FindFirstChild("HumanoidRootPart")

      if botHumanoidRootPart then
        local distance = (botHumanoidRootPart.Position - humanoidRootPart.Position).Magnitude

        if distance > 25 then --make them tp if they are too far from the player, otherwise the cmd would be useless
          botHumanoidRootPart.CFrame = humanoidRootPart.CFrame + humanoidRootPart.CFrame.LookVector * -2.06546464
        else
          local randomOffset = Vector3.new(math.random(-8, 8),0,math.random(-8, 8))
          local moveToPosition = humanoidRootPart.Position + randomOffset
          player.Character.Humanoid:MoveTo(moveToPosition)
        end
      end
      wait(0.28) -- small delay otherwise it looks like they're having an seizure
    end
  else
    warn("Target player or their character is not valid.")
  end
end

-- ;admin
local function admin(targetPlayer)
  if not table.find(Admins, targetPlayer.Name) then
    table.insert(Admins, targetPlayer.Name)
    table.insert(adminNotConnected, targetPlayer.Name)
  else
  end
end

-- check chat for cmds
local function connectChatListener(playerpower)
  playerpower.Chatted:Connect(function(message)
  if playerpower.Name == owner or table.find(Admins, playerpower.Name) then
    if message:sub(1, #prefix) == prefix then
      local command = message:sub(#prefix + 1)
      if command == "status" and cmdstatus and table.find(bots, displayName) then
        chatMessage(displayName .. " (Bot " .. index .. ") is active!")
        wait(2)

      elseif command:sub(1, 6) == "admin " and table.find(bots, displayName) and cmdadmin then
        local adminargs = command:sub(7)
        local targetPlayerforadmin = findPlayerByName(adminargs)

        if targetPlayerforadmin then
          admin(targetPlayerforadmin)
          if index == channel then
            chatMessage(targetPlayerforadmin.Name .. ' is now an admin.')
          end
        else
          if index == channel then
            chatMessage("Player not found.")
          end
        end
        wait(2)

      elseif command == "quit" and table.find(bots, displayName) and cmdquit then
        cmdstatus = false
        cmdindex = false
        cmdfollow = false
        cmdquit = false
        cmddance = false
        cmdundance = false
        cmdreset = false
        cmdjump = false
        cmdsay = false
        cmdunfollow = false
        followbool = false
        cmdreset = false
        cmdorbit = false
        orbitbool = false
        cmdunorbit = false
        cmdgoto = false
        cmdalign = false
        cmdws = false
        booljump = false
        cmdloopjump = false
        cmdunloopjump = false
        cmdcircle = false
        cmdchannel = false
        orbitbool = false
        orbitbool5 = false
        orbitbool2 = false
        orbitbool3 = false
        orbitbool4 = false
        orbitbool6 = false
        wormbool = false
        cmdworm = false
        cmdunworm = false
        cmdspin = false
        cmdunspin = false
        boolspin = false
        cmdadmin = false
        adminbool = false
        cmdarch = false
        cmdorbit2 = false
        cmdorbit3 = false
        cmdorbit4 = false
        cmdorbit5 = false
        cmdorbit6 = false
        cmdstalk = false
        stalkbool = false
        cmdunstalk = false
        cmdhelp = false
        towerbool = false
        cmdtower = false
        cmduntower = false
        cmdfix = false
        Admins = {}
        adminNotConnected = {}
        chatMessage("quit")
        wait(2)


      elseif command == "index" and cmdindex and table.find(bots, displayName) then
        chatMessage(displayName .. " index is (" .. index .. ")")
        wait(2)

      elseif command:sub(1, 8) == "channel " and cmdchannel and table.find(bots, displayName) then
        local chnl = tonumber(command:sub(9))

        if chnl > nbbot or chnl < 1 then
          if index == channel then
            chatMessage("Error: channel must be between 1 and " .. nbbot)
          end
        else
          channel = chnl
          if index == channel then
            chatMessage("Channel is now: " .. channel)
          end
        end
        wait(2)

      elseif command:sub(1, 15) == "unloopjump" and cmdunloopjump and table.find(bots, displayName) then
        booljump = false
        wait(2)
      
      elseif command:sub(1, 8) == "untower" and cmduntower and table.find(bots, displayName) then
          towerbool = false
          wait(2)

      elseif command == "loopjump" and cmdloopjump and table.find(bots, displayName) then
        booljump = true
        while booljump do
          player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
          wait(0.8)
        end
        wait(2)

      elseif command:sub(1, 6) == "align " and cmdalign and table.find(bots, displayName) then
        disablebool()
        local playerName = command:sub(7)
        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          align(targetPlayer)
          wait(2)
        else
          chatMessage("Player not found: " .. playerName)
        end
          align(targetPlayer)
          if index == channel then
            chatMessage("yes sir!")
          end
          wait(2)

      elseif command:sub(1, 7) == "dance" and table.find(bots, displayName) and cmddance then
        chatMessage("/e dance")
        wait(2)

      elseif command:sub(1, 7) == "dance 1" and table.find(bots, displayName) and cmddance then
        chatMessage("/e dance1")
        wait(2)

      elseif command:sub(1, 7) == "dance 2" and table.find(bots, displayName) and cmddance then
        chatMessage("/e dance2")
        wait(2)

      elseif command:sub(1, 7) == "dance 3" and table.find(bots, displayName) and cmddance then
        chatMessage("/e dance3")
        wait(2)

      elseif command:sub(1, 7) == "dance 4" and table.find(bots, displayName) and cmddance then
        chatMessage("/e dance 4")
        wait(2)

    elseif command:sub(1, 5) == "help" and table.find(bots, displayName) and cmdhelp then --max character per message is 155
    if index == channel then
        chatMessage("available commands:")
        chatMessage(";status ;index ;follow [plr] ;quit ;dance <number> ;undance ;reset ;jump ;say <sentence> ;unfollow ;orbit [plr] <radius> <speed>")
        chatMessage(";orbit2 [plr] <radius> <speed> ;orbit3 [plr] <radius> <speed> ;orbit4 [plr] <radius> <speed> ;orbit5 [plr] <radius> <speed>")
        chatMessage(";orbit6 [plr] <radius> <speed> ;unorbit ;goto [plr] ;align ;ws <number> ;loopjump ;unloopjump ;circle <number> ;channel <number>")
        chatMessage(";worm [plr] ;unworm ;spin <number> ;unspin ;admin [plr] ;arch <number> ;stalk [plr] ;unstalk ;help")
        end
    wait(2)

      elseif command:sub(1, 5) == "spin " and table.find(bots, displayName) and cmdspin then
        local spinarg = tonumber(command:sub(6))
        spin(spinarg)
        boolspin = true
        wait(2)

      elseif command:sub(1, 6) == "unspin" and table.find(bots, displayName) and cmdunspin then
        boolspin = false
        wait(2)

      elseif command:sub(1, 3) == "ws " and table.find(bots, displayName) and cmdws then
        local wsarg = tonumber(command:sub(4))
        if wsarg then
          player.Character.Humanoid.WalkSpeed = wsarg
          wait(2)
        else
        end

      elseif command:sub(1, 7) == "undance" and table.find(bots, displayName) and cmddance then
        player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        wait(2)

      elseif command:sub(1, 7) == "circle " and table.find(bots, displayName) and cmdcircle then
        disablebool()
        local circlearg = tonumber(command:sub(8)) or 8
        tpcircle(circlearg)
        wait(2)

      elseif command:sub(1, 5) == "arch " and table.find(bots, displayName) and cmdarch then
        disablebool()
        local archarg = tonumber(command:sub(6)) or 8
        tparch(archarg)
        wait(2)

      elseif command:sub(1, 4) == "say " and table.find(bots, displayName) and cmdsay then
        local msgcontent = command:sub(5)
        chatMessage(msgcontent)
        wait(2)

      elseif command:sub(1, 4) == "fix" and table.find(bots, displayName) and cmdfix then
        fix()
        chatmessage("Bot number "..index.."is fixed")
        wait(2)

      elseif command:sub(1, 7) == "jump" and table.find(bots, displayName) and cmdjump then
        player.Character.Humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
        wait(2)

    elseif command:sub(1, 9) == "unorbit" and table.find(bots, displayName) and cmdunorbit then
        orbitbool = false
        orbitbool2 = false
        orbitbool3 = false
        orbitbool4 = false
        orbitbool5 = false
        orbitbool6 = false

        if index == channel then
          chatMessage("stopped orbiting")
        end
        game.Workspace.Gravity = 196.2
        wait(2)

    elseif command:sub(1, 5) == "goto " and table.find(bots, displayName) and cmdgoto then
      disablebool()
        local playerName = command:sub(6)
        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          goto(targetPlayer)
          wait(2)
        else
          chatMessage("Player not found: " .. playerName)
        end

    elseif command:sub(1, 6) == "tower " and table.find(bots, displayName) and cmdtower then
      disablebool()
        local playerName = command:sub(7)
        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          tower(targetPlayer)
          wait(2)
        else
          chatMessage("Player not found: " .. playerName)
        end

      elseif command:sub(1, 9) == "unfollow" and table.find(bots, displayName) and cmdunfollow then
        followbool = false
        if index == channel then
          chatMessage("stopped following")
        end
        wait(2)

    elseif command:sub(1, 6) == "unworm" and table.find(bots, displayName) and cmdunworm then
        wormbool = false
        if index == channel then
          chatMessage("stopped worm")
        end
        wait(2)

    elseif command:sub(1, 6) == "orbit " and table.find(bots, displayName) and cmdorbit then
      disablebool()
        orbitbool = false
        local args = command:split(" ")
        local playerName = args[2] 
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool = true

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end
          orbitPlayer(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 7) == "orbit2 " and table.find(bots, displayName) and cmdorbit2 then
      disablebool()
        orbitbool2 = false
        local args = command:split(" ")
        local playerName = args[2]
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool2 = true 

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end
          orbitPlayer2(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 7) == "orbit3 " and table.find(bots, displayName) and cmdorbit3 then
      disablebool()
        orbitbool3 = false
        local args = command:split(" ")
        local playerName = args[2]
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool3 = true

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end
          orbitPlayer3(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end
    elseif command:sub(1, 7) == "orbit4 " and table.find(bots, displayName) and cmdorbit4 then
      disablebool()
        orbitbool4 = false
        local args = command:split(" ")
        local playerName = args[2]
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool4 = true

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end
          orbitPlayer4(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 7) == "orbit6 " and table.find(bots, displayName) and cmdorbit6 then
      disablebool()
        orbitbool6 = false
        local args = command:split(" ")
        local playerName = args[2]
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool6 = true 

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end
          orbitPlayer6(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 7) == "orbit5 " and table.find(bots, displayName) and cmdorbit5 then
      disablebool()
        orbitbool5 = false
        local args = command:split(" ")
        local playerName = args[2]
        local r = tonumber(args[3])
        local speed = tonumber(args[4])

        local targetPlayer = findPlayerByName(playerName)
        if targetPlayer then
          orbitbool5 = true

          if index == channel then
            chatMessage("Bots are now orbiting " .. targetPlayer.Name)
          end

          orbitPlayer5(targetPlayer, speed, r)

          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 6) == "reset" and table.find(bots, displayName) and cmdreset then
      disablebool()
        player.Character:BreakJoints()
        game.Workspace.Gravity = 196.2
        wait(2)

    elseif command:sub(1, 5) == "worm " and table.find(bots, displayName) and cmdworm then
      disablebool()
        local playerName = command:sub(6) -- Obtenir le nom du joueur à suivre
        local targetPlayer = findPlayerByName(playerName)
        wormbool = false
        worm(targetPlayer)
        wait(2)

    elseif command:sub(1, 7) == "unstalk" and table.find(bots, displayName) and cmdunstalk then
        stalkbool = false
        if index == channel then
          chatMessage("Bots stopped stalking")
        end
        wait(2)

    elseif command:sub(1, 6) == "stalk " and table.find(bots, displayName) and cmdstalk then
      disablebool()
        stalkbool = false
        local playerName = command:sub(7)
        local targetPlayer = findPlayerByName(playerName)
        stalkbool = true
        if targetPlayer then
          if index == channel then
            chatMessage("Bots are now stalking " .. targetPlayer.Name .. ".")
          end
          stalkPlayer(targetPlayer)
          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end

    elseif command:sub(1, 7) == "follow " and table.find(bots, displayName) and cmdfollow then
      disablebool()
        followbool = false
        local playerName = command:sub(8)
        local targetPlayer = findPlayerByName(playerName)
        followbool = true
        if targetPlayer then
          if index == channel then
            chatMessage("Bots are now following " .. targetPlayer.Name .. ".")
          end
          followPlayer(targetPlayer)
          wait(2)
        else
          if index == channel then
            chatMessage("Player not found: " .. playerName)
          end
        end
      end
    end
  end
 end)
end

--listen to players
player.Chatted:Connect(function(message)

end)

--listen to owner
if ownerPlayer then
  connectChatListener(ownerPlayer)
end

--listen to admins
while adminbool do
  for _, adminName in pairs(adminNotConnected) do
    local adminPlayer = game.Players:FindFirstChild(adminName)
    if adminPlayer then
      connectChatListener(adminPlayer)
      table.remove(adminNotConnected, table.find(adminNotConnected, adminName))
    end
  end
  wait(2)
end

--listen to admins
game.Players.PlayerAdded:Connect(function(player)
if table.find(Admins, player.Name) then
  connectChatListener(player)
end
end)
