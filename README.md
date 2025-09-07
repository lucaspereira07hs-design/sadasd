-- LocalScript: Infinite Jump com botão na tela

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local infiniteJumpEnabled = false

-- Criar a interface (GUI)
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "InfiniteJumpGui"
screenGui.ResetOnSpawn = false -- mantém o botão mesmo após a morte
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Criar o botão
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 160, 0, 40)
button.Position = UDim2.new(0, 10, 0, 60) -- posição na tela
button.Text = "Infinite Jump: OFF"
button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
button.TextColor3 = Color3.new(1, 1, 1)
button.Font = Enum.Font.SourceSansBold
button.TextSize = 18
button.Parent = screenGui

-- Função para alternar o estado
local function toggleInfiniteJump()
	infiniteJumpEnabled = not infiniteJumpEnabled
	if infiniteJumpEnabled then
		button.Text = "Infinite Jump: ON"
		button.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
	else
		button.Text = "Infinite Jump: OFF"
		button.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
	end
end

-- Conecta o clique do botão
button.MouseButton1Click:Connect(toggleInfiniteJump)

-- Ativa o pulo infinito quando a tecla de pulo for pressionada
UserInputService.JumpRequest:Connect(function()
	if infiniteJumpEnabled then
		local character = player.Character
		if character then
			local humanoid = character:FindFirstChildOfClass("Humanoid")
			if humanoid then
				humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
			end
		end
	end
end)
