-- Mensagem de carregamento
print("Script carregado com sucesso!")

-- Criação do ScreenGui
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
local FreeCameraButton = Instance.new("TextButton")
local NoClipButton = Instance.new("TextButton")
local AutoFarmButton = Instance.new("TextButton")
local AntiBanButton = Instance.new("TextButton")
local SaveSettingsButton = Instance.new("TextButton")
local ToggleESPButton = Instance.new("TextButton")
local ChangeColorButton = Instance.new("TextButton")
local ShowCoordsButton = Instance.new("TextButton")
local SpeedMultiplierSlider = Instance.new("TextButton")

-- Função para criar botões
local function createButton(button, parent, position, text, color, size)
    button.Parent = parent
    button.BackgroundColor3 = color
    button.Position = position
    button.Size = size or UDim2.new(0.8, 0, 0.1, 0)
    button.Text = text
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.BorderSizePixel = 2
    button.BorderColor3 = Color3.fromRGB(255, 0, 0)
end

-- Criação do ScreenGui
ScreenGui.Name = "MenuGui"
ScreenGui.Parent = game.CoreGui

-- Propriedades do Frame
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.Position = UDim2.new(0.5, -150, 0.5, -200)
Frame.Size = UDim2.new(0, 300, 0, 700)
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
createButton(ToggleESPButton, Frame, UDim2.new(0.1, 0, 1.1, 0), "Alternar ESP", Color3.fromRGB(0, 255, 0))
createButton(ChangeColorButton, Frame, UDim2.new(0.1, 0, 1.2, 0), "Mudar Cor", Color3.fromRGB(0, 0, 255))
createButton(ShowCoordsButton, Frame, UDim2.new(0.1, 0, 1.3, 0), "Mostrar Coordenadas", Color3.fromRGB(255, 255, 0))
createButton(SpeedMultiplierSlider, Frame, UDim2.new(0.1, 0, 1.4, 0), "Multiplicador de Velocidade", Color3.fromRGB(0, 255, 255))

-- Variáveis de configuração
local flyEnabled = false
local speedEnabled = false
local wallHackEnabled = false
local espEnabled = false
local annoyEnabled = false
local selectedPlayer = nil
local espActive = false
local showCoords = false
local speedMultiplier = 1

-- Função para salvar configurações
local function saveSettings()
    -- Salvar configurações personalizadas (tamanho, posição, etc.)
    local settings = {
        flyEnabled = flyEnabled,
        speedEnabled = speedEnabled,
        wallHackEnabled = wallHackEnabled,
        espEnabled = espEnabled,
        annoyEnabled = annoyEnabled,
        selectedPlayer = selectedPlayer,
        speedMultiplier = speedMultiplier
    }
    -- Simulação de salvar dados
    print("Configurações salvas!")
end

-- Funções de configuração do menu e das funcionalidades

-- Função para alternar visibilidade do menu
ToggleMenuButton.MouseButton1Click:Connect(function()
    Frame.Visible = not Frame.Visible
end)

-- Função para fechar o menu
CloseButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
end)

-- Funções de Fly
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

-- Função para Speed
SpeedButton.MouseButton1Click:Connect(function()
    speedEnabled = not speedEnabled
    local player = game.Players.LocalPlayer
    local character = player.Character
    if character then
        character.Humanoid.WalkSpeed = speedEnabled and 100 * speedMultiplier or 16
    end
end)

-- Função para WallHack
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

-- Função para Teleporte
TeleportButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    if selectedPlayer and selectedPlayer.Character then
        player.Character:SetPrimaryPartCFrame(selectedPlayer.Character.PrimaryPart.CFrame)
    end
end)

-- Função para ESP
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

-- Função para alternar ESP
ToggleESPButton.MouseButton1Click:Connect(function()
    espActive = not espActive
    for _, player in pairs(game.Players:GetPlayers()) do
        if player ~= game.Players.LocalPlayer then
            if espActive then
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

-- Função para mudar a cor de fundo
ChangeColorButton.MouseButton1Click:Connect(function()
    Frame.BackgroundColor3 = Color3.fromRGB(math.random(255), math.random(255), math.random(255))
end)

-- Função para mostrar as coordenadas
ShowCoordsButton.MouseButton1Click:Connect(function()
    showCoords = not showCoords
    local player = game.Players.LocalPlayer
    if showCoords then
        local positionLabel = Instance.new("TextLabel")
        positionLabel.Parent = ScreenGui
        positionLabel.Position = UDim2.new(0, 10, 0, 40)
        positionLabel.Size = UDim2.new(0, 200, 0, 50)
        positionLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
        positionLabel.TextSize = 18
        positionLabel.Text = "Coordenadas: " .. tostring(player.Character.HumanoidRootPart.Position)
    end
end)

-- Função para configurar o multiplicador de velocidade
SpeedMultiplierSlider.MouseButton1Click:Connect(function()
    speedMultiplier = speedMultiplier + 0.5
    print("Novo multiplicador de velocidade: " .. speedMultiplier)
end)

-- Salvar configurações
SaveSettingsButton.MouseButton1Click:Connect(saveSettings)

-- Fim do código
print("Script carregado e pronto para uso.")
