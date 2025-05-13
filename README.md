local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer

local classicWalkAnimId = "http://www.roblox.com/asset/?id=180426354" -- Animação antiga de andar
local animTrack = nil
local animation = nil
local enabled = false

local function applyClassicAnimation()
	local character = player.Character or player.CharacterAdded:Wait()
	local humanoid = character:WaitForChild("Humanoid")

	-- Cria e carrega a animação
	animation = Instance.new("Animation")
	animation.AnimationId = classicWalkAnimId

	animTrack = humanoid:LoadAnimation(animation)
	animTrack.Priority = Enum.AnimationPriority.Movement
	animTrack:Play()
end

-- Escuta tecla Q
UserInputService.InputBegan:Connect(function(input, gameProcessed)
	if gameProcessed then return end
	if input.KeyCode == Enum.KeyCode.Q then
		if not enabled then
			enabled = true
			applyClassicAnimation()
		end
	end
end)
