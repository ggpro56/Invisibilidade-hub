# Invisibilidade-hub
Creator:senhor_guest6
-- Interface
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Criar a interface
local ScreenGui = Instance.new("ScreenGui")
local ToggleButton = Instance.new("TextButton")

ScreenGui.Parent = player.PlayerGui
ScreenGui.Name = "InvisibilityHub"

ToggleButton.Parent = ScreenGui
ToggleButton.Size = UDim2.new(0, 200, 0, 50)
ToggleButton.Position = UDim2.new(0, 20, 0, 20)
ToggleButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
ToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 24
ToggleButton.Text = "Ativar Invisibilidade"

-- Estado da invisibilidade
local invisivel = false

-- Função para alterar a visibilidade
local function toggleInvisibilidade()
    character = player.Character or player.CharacterAdded:Wait()

    invisivel = not invisivel

    for _, part in pairs(character:GetDescendants()) do
        if part:IsA("BasePart") and part.Name ~= "HumanoidRootPart" then
            part.Transparency = invisivel and 1 or 0
            if part:FindFirstChildOfClass("Decal") then
                for _, decal in pairs(part:GetChildren()) do
                    if decal:IsA("Decal") then
                        decal.Transparency = invisivel and 1 or 0
                    end
                end
            end
        end
    end

    ToggleButton.Text = invisivel and "Desativar Invisibilidade" or "Ativar Invisibilidade"
end

-- Conectar botão
ToggleButton.MouseButton1Click:Connect(toggleInvisibilidade)
