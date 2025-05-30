--[[
	WARNING: Heads up! This script has not been verified by ScriptBlox. Use at your own risk!
]]

-- Variables
local part = Instance.new("Part")
part.Size = Vector3.new(5, 5, 5)
part.Position = Vector3.new(0, 5, 0)
part.Parent = workspace

-- Particle Effect Setup
local particleEmitter = Instance.new("ParticleEmitter")
particleEmitter.Parent = part
particleEmitter.Texture = "rbxassetid://117012443612361" -- Replace with your particle texture ID
particleEmitter.Lifetime = NumberRange.new(1)
particleEmitter.Rate = 10
particleEmitter.Speed = NumberRange.new(5)

-- Decal Spammer Function
local function spamDecals()
    for i = 1, 10 do
        local decal = Instance.new("Decal")
        decal.Texture = "rbxassetid://117012443612361" -- Replace with your decal ID
        decal.Parent = part
        wait(0.5) -- Adjust the wait time as needed
    end
end

-- Skybox Setup
local skybox = Instance.new("Sky")
skybox.SkyboxBk = "rbxassetid://117012443612361" -- Replace with your skybox ID
skybox.SkyboxDn = "rbxassetid://117012443612361"
skybox.SkyboxFt = "rbxassetid://117012443612361"
skybox.SkyboxLf = "rbxassetid://117012443612361"
skybox.SkyboxRt = "rbxassetid://117012443612361"
skybox.SkyboxUp = "rbxassetid://117012443612361"
skybox.Parent = game.Lighting

-- Execute the decal spammer
spamDecals()

-- Sound Setup
local sound1 = Instance.new("Sound")
sound1.SoundId = "rbxassetid://6070263388" -- Replace with your first sound ID
sound1.Looped = true -- Enable looping
sound1.Parent = game.Workspace

local sound2 = Instance.new("Sound")
sound2.SoundId = "rbxassetid://6070263388" -- Replace with your second sound ID
sound2.Looped = true -- Enable looping
sound2.Parent = game.Workspace

local currentSound = sound1

local function changeMusic()
    if currentSound.IsPlaying then
        currentSound:Stop() -- Stop the current sound before changing
    end
    
    currentSound = (currentSound == sound1) and sound2 or sound1
    currentSound:Play()
end

-- Jumpscare Functionality
local function triggerJumpscare()
    local jumpscareSound = Instance.new("Sound")
    jumpscareSound.SoundId = "rbxassetid://8884864842" -- Replace with your jumpscare sound ID
    jumpscareSound.Parent = game.Workspace
    jumpscareSound:Play()

    local jumpscareImage = Instance.new("ImageLabel")
    jumpscareImage.Image = "rbxassetid://117012443612361" -- Replace with your jumpscare image ID
    jumpscareImage.Size = UDim2.new(1, 0, 1, 0)
    jumpscareImage.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
    
    wait(2) -- Duration of the jumpscare
    jumpscareImage:Destroy() -- Remove the jumpscare image after display
end

-- Anti-Leave Realm Functionality
local function onPlayerLeave(player)
    if player.UserId == 666 then -- Check if the player is the guest with ID 666
        player:LoadCharacter() -- Reload the character to prevent leaving
        -- Optionally, change the map or teleport the player
    end
end

game.Players.PlayerRemoving:Connect(onPlayerLeave)

-- Bind the function to a key press or a GUI button
game:GetService("UserInputService").InputBegan:Connect(function(input)
    if input.KeyCode == Enum.KeyCode.M then -- Press 'M' to change music
        changeMusic()
    elseif input.KeyCode == Enum.KeyCode.J then -- Press 'J' to trigger jumpscare
        triggerJumpscare()
    end
end)

-- Start playing the initial sound
currentSound:Play()
 for _, player in pairs(game.Players:GetPlayers()) do
    local particleEmitter = Instance.new("ParticleEmitter")
    particleEmitter.Parent = player.Character:WaitForChild("HumanoidRootPart")
    particleEmitter.Texture = "rbxassetid://117012443612361"
    particleEmitter.Lifetime = NumberRange.new(1, 2)
    particleEmitter.Rate = 100
    particleEmitter.Velocity = NumberRange.new(0, 10)
end

