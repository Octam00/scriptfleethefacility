print("Script carregado")

-- Criação do menu
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local FlyButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local WallHackButton = Instance.new("TextButton")
local TeleportButton = Instance.new("TextButton")
local ESPButton = Instance.new("TextButton")
local AnnoyButton = Instance.new("TextButton")
local CreditsButton = Instance.new("TextButton")
local CloseButton = Instance.new("TextButton")
local ToggleMenuButton = Instance.new("TextButton")
local PlayerDropdown = Instance.new("TextButton")
local SpectateButton = Instance.new("TextButton")
local VoidButton = Instance.new("TextButton")

-- Propriedades do ScreenGui
ScreenGui.Name = "MenuGui"
ScreenGui.Parent = game.CoreGui

-- Propriedades do Frame
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.Position = UDim2.new(0.5, -150, 0.5, -200)
Frame.Size = UDim2.new(0, 300, 0, 500)
Frame.BackgroundTransparency = 0.3
Frame.BorderSizePixel = 2
Frame.BorderColor3 = Color3.fromRGB(255, 0, 0)

-- Propriedades do TextLabel
TextLabel.Parent = Frame
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
TextLabel.Size = UDim2.new(1, 0, 0.1, 0)
TextLabel.Text = "Menu Principal"
TextLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.Font = Enum.Font.SourceSansBold
TextLabel.TextSize = 24

-- Função para criar botões
local function createButton(button, parent, position, text, color)
    button.Parent = parent
    button.BackgroundColor3 = color
    button.Position = position
    button.Size = UDim2.new(0.8, 0, 0.1, 0)
    button.Text = text
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BorderSizePixel = 2
    button.BorderColor3 = Color3.fromRGB(255, 0, 0)
end

-- Criação dos botões
createButton(FlyButton, Frame, UDim2.new(0.1, 0, 0.2, 0), "Fly", Color3.fromRGB(255, 0, 0))
createButton(SpeedButton, Frame, UDim2.new(0.1, 0, 0.3, 0), "Speed", Color3.fromRGB(255, 0, 0))
createButton(WallHackButton, Frame, UDim2.new(0.1, 0, 0.4, 0), "Atravessar Parede", Color3.fromRGB(255, 0, 0))
createButton(TeleportButton, Frame, UDim2.new(0.1, 0, 0.5, 0), "Teleportar", Color3.fromRGB(255, 0, 0))
createButton(ESPButton, Frame, UDim2.new(0.1, 0, 0.6, 0), "ESP", Color3.fromRGB(255, 0, 0))
createButton(AnnoyButton, Frame, UDim2.new(0.1, 0, 0.7, 0), "Irritar", Color3.fromRGB(255, 0, 0))
createButton(CreditsButton, Frame, UDim2.new(0.1, 0, 0.8, 0), "Créditos", Color3.fromRGB(255, 0, 0))
createButton(SpectateButton, Frame, UDim2.new(0.1, 0, 0.9, 0), "Espectar", Color3.fromRGB(255, 0, 0))
createButton(VoidButton, Frame, UDim2.new(0.1, 0, 1.0, 0), "Void", Color3.fromRGB(255, 0, 0))
createButton(CloseButton, Frame, UDim2.new(0.9, -20, 0, 10), "X", Color3.fromRGB(255, 0, 0))
createButton(ToggleMenuButton, ScreenGui, UDim2.new(0, 10, 0, 10), "Menu", Color3.fromRGB(255, 0, 0))

-- Criação do dropdown de jogadores
PlayerDropdown.Parent = Frame
PlayerDropdown.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
PlayerDropdown.Position = UDim2.new(0.1, 0, 0.1, 0)
PlayerDropdown.Size = UDim2.new(0.8, 0, 0.1, 0)
PlayerDropdown.Text = "Selecionar Jogador"
PlayerDropdown.Font = Enum.Font.SourceSansBold
PlayerDropdown.TextSize = 18
PlayerDropdown.TextColor3 = Color3.fromRGB(255, 255, 255)
PlayerDropdown.BorderSizePixel = 2
PlayerDropdown.BorderColor3 = Color3.fromRGB(255, 0, 0)

-- Variáveis de estado
local flyEnabled = false
local speedEnabled = false
local wallHackEnabled = false
local espEnabled = false
local annoyEnabled = false
local selectedPlayer = nil

-- Função para atualizar a lista de jogadores
local function updatePlayerDropdown()
    local players = game.Players:GetPlayers()
    local dropdownText = "Selecionar Jogador\n"
    for _, player in pairs(players) do
        dropdownText = dropdownText .. player.Name .. "\n"
    end
    PlayerDropdown.Text = dropdownText
end

-- Atualizar a lista de jogadores ao iniciar
updatePlayerDropdown()

-- Função para selecionar jogador
PlayerDropdown.MouseButton1Click:Connect(function()
    local players = game.Players:GetPlayers()
    local dropdownText = "Selecionar Jogador\n"
    for _, player in pairs(players) do
        dropdownText = dropdownText .. player.Name .. "\n"
    end
    PlayerDropdown.Text = dropdownText
    PlayerDropdown.MouseButton1Click:Connect(function()
        local mouse = game.Players.LocalPlayer:GetMouse()
        mouse.Button1Down:Connect(function()
            for _, player in pairs(players) do
                if mouse.Target and mouse.Target.Parent == player.Character then
                    selectedPlayer = player
                    PlayerDropdown.Text = "Selecionado: " .. player.Name
                    break
                end
            end
        end)
    end)
end)

-- Funções dos botões
FlyButton.MouseButton1Click:Connect(function()
    flyEnabled = not flyEnabled
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        if flyEnabled then
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Physics)
            character.HumanoidRootPart.Velocity = Vector3.new(0, 50, 0)
        else
            character.Humanoid:ChangeState(Enum.HumanoidStateType.Running)
            character.HumanoidRootPart.Velocity = Vector3.new(0, 0, 0)
        end
    end
end)

SpeedButton.MouseButton1Click:Connect(function()
    speedEnabled = not speedEnabled
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        character.Humanoid.WalkSpeed = speedEnabled and 100 or 16
    end
end)

WallHackButton.MouseButton1Click:Connect(function()
    wallHackEnabled = not wallHackEnabled
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = not wallHackEnabled
            end
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
    espEnabled = not espEnabled
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            if espEnabled then
                local highlight = Instance.new("Highlight")
                highlight.Parent = player.Character
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
            else
                for _, highlight in pairs(player.Character:GetChildren()) do
                    if highlight:IsA("Highlight") then
                        highlight:Destroy()
                    end
                end
            end
        end
    end
end)

AnnoyButton.MouseButton1Click:Connect(function()
    annoyEnabled = not annoyEnabled
    local player = game.Players.LocalPlayer
    for _, otherPlayer in pairs(game.Players:GetPlayers()) do
        if otherPlayer ~= player then
            if annoyEnabled then
                otherPlayer:Kick("Você foi irritado!")
            end
        end
    end
end)

CreditsButton.MouseButton1Click:Connect(function()
    -- Código para mostrar créditos
    print("Script criado por [Seu Nome]")
end)

SpectateButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if selectedPlayer and selectedPlayer.Character then
        player.CameraMode = Enum.CameraMode.LockFirstPerson
        workspace.CurrentCamera.CameraSubject = selectedPlayer.Character.Humanoid
    else
        player.CameraMode = Enum.CameraMode.Classic
        workspace.CurrentCamera.CameraSubject = player.Character.Humanoid
    end
end)

VoidButton.MouseButton1Click:Connect(function()
    if selectedPlayer and selectedPlayer.Character then
        selectedPlayer.Character:SetPrimaryPartCFrame(CFrame.new(0, -500, 0))
    end
end)

CloseButton.MouseButton1Click:Connect(function()
    -- Código para ocultar o menu
    Frame.Visible = not Frame.Visible
end)

ToggleMenuButton.MouseButton1Click:Connect(function()
    -- Código para ocultar/mostrar o menu
    Frame.Visible = not Frame.Visible
end)

-- Sistema básico para evitar banimento
local function antiBan()
    local player = game.Players.LocalPlayer
    player.Chatted:Connect(function(message)
        if message:lower():find("hack") or message:lower():find("cheat") then
            player:Kick("Uso de hacks detectado. Banimento evitado.")
        end
    end)
end

antiBan()
