print("Script carregado")

-- Criação do menu
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")
local ToggleMenuButton = Instance.new("TextButton")

local FlyButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local WallHackButton = Instance.new("TextButton")
local TeleportButton = Instance.new("TextButton")
local ESPButton = Instance.new("TextButton")
local AnnoyButton = Instance.new("TextButton")
local VoidButton = Instance.new("TextButton")
local SpectateButton = Instance.new("TextButton")
local CreditsButton = Instance.new("TextButton")

-- Variáveis de estado
local flyEnabled = false
local speedEnabled = false
local flySpeed = 50 -- Velocidade inicial do Fly
local selectedSpeed = 16 -- Velocidade inicial do Speed
local selectedPlayer = nil

-- Propriedades do ScreenGui
ScreenGui.Name = "MenuGui"
ScreenGui.Parent = game.CoreGui

-- Propriedades do Frame
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.Position = UDim2.new(0.5, -150, 0.5, -150)
Frame.Size = UDim2.new(0, 300, 0, 300)
Frame.BackgroundTransparency = 0.2
Frame.BorderSizePixel = 0

-- Propriedades do Título
Title.Parent = Frame
Title.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
Title.Size = UDim2.new(1, 0, 0.15, 0)
Title.Text = "Menu Principal"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 22

-- Botão para fechar o menu
CloseButton.Parent = Frame
CloseButton.Position = UDim2.new(0.92, 0, 0.02, 0)
CloseButton.Size = UDim2.new(0.06, 0, 0.12, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.TextSize = 18

-- Botão para alternar o menu
ToggleMenuButton.Parent = ScreenGui
ToggleMenuButton.Position = UDim2.new(0, 10, 0, 10)
ToggleMenuButton.Size = UDim2.new(0, 80, 0, 30)
ToggleMenuButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
ToggleMenuButton.Text = "Menu"
ToggleMenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleMenuButton.Font = Enum.Font.SourceSansBold
ToggleMenuButton.TextSize = 18

-- Função para criar botões no menu
local function createButton(button, parent, position, text)
    button.Parent = parent
    button.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    button.Position = position
    button.Size = UDim2.new(0.4, 0, 0.1, 0)
    button.Text = text
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
end

-- Criação dos botões do menu
createButton(FlyButton, Frame, UDim2.new(0.05, 0, 0.2, 0), "Fly")
createButton(SpeedButton, Frame, UDim2.new(0.55, 0, 0.2, 0), "Speed")
createButton(WallHackButton, Frame, UDim2.new(0.05, 0, 0.35, 0), "Wall Hack")
createButton(ESPButton, Frame, UDim2.new(0.55, 0, 0.35, 0), "ESP")
createButton(TeleportButton, Frame, UDim2.new(0.05, 0, 0.5, 0), "Teleportar")
createButton(VoidButton, Frame, UDim2.new(0.55, 0, 0.5, 0), "Void")
createButton(SpectateButton, Frame, UDim2.new(0.05, 0, 0.65, 0), "Espectar")
createButton(CreditsButton, Frame, UDim2.new(0.55, 0, 0.65, 0), "Créditos")

-- Função para alternar a visibilidade do menu
ToggleMenuButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

CloseButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
end)

-- Funções dos botões
FlyButton.MouseButton1Click:Connect(function()
    flyEnabled = not flyEnabled
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    if flyEnabled then
        character.HumanoidRootPart.Velocity = Vector3.new(0, flySpeed, 0)
    else
        character.HumanoidRootPart.Velocity = Vector3.new(0, 0, 0)
    end
end)

SpeedButton.MouseButton1Click:Connect(function()
    speedEnabled = not speedEnabled
    local player = game.Players.LocalPlayer
    local humanoid = player.Character:FindFirstChild("Humanoid")
    if humanoid then
        humanoid.WalkSpeed = speedEnabled and 100 or 16
    end
end)

WallHackButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    for _, part in pairs(player.Character:GetChildren()) do
        if part:IsA("BasePart") then
            part.CanCollide = false
        end
    end
end)

TeleportButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if selectedPlayer and selectedPlayer.Character then
        player.Character:SetPrimaryPartCFrame(selectedPlayer.Character.PrimaryPart.CFrame)
    end
end)

ESPButton.MouseButton1Click:Connect(function()
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer and player.Character then
            local highlight = Instance.new("Highlight")
            highlight.Parent = player.Character
            highlight.FillColor = Color3.fromRGB(255, 0, 0)
            highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
        end
    end
end)

CreditsButton.MouseButton1Click:Connect(function()
    print("Script criado por você!")
end)iado por [Octam]")
end)
