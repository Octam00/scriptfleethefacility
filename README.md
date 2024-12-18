print("Script carregado")

-- Criação do menu
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")
local ToggleMenuButton = Instance.new("TextButton")

local FlyButton = Instance.new("TextButton")
local SpeedButton = Instance.new("TextButton")
local SpeedSlider = Instance.new("Frame")
local SliderBar = Instance.new("Frame")
local SliderButton = Instance.new("TextButton")

local WallHackButton = Instance.new("TextButton")
local TeleportButton = Instance.new("TextButton")
local ESPButton = Instance.new("TextButton")
local AnnoyButton = Instance.new("TextButton")
local CreditsButton = Instance.new("TextButton")
local VoidButton = Instance.new("TextButton")
local SpectateButton = Instance.new("TextButton")
local PlayerDropdown = Instance.new("TextButton")

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
Frame.Position = UDim2.new(0.5, -150, 0.5, -250)
Frame.Size = UDim2.new(0, 300, 0, 500)
Frame.BackgroundTransparency = 0.2
Frame.BorderSizePixel = 0

-- Propriedades do Título
Title.Parent = Frame
Title.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
Title.Size = UDim2.new(1, 0, 0.1, 0)
Title.Text = "Menu Principal"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 24

-- Propriedades do botão Fechar
CloseButton.Parent = Frame
CloseButton.Position = UDim2.new(0.9, -20, 0.02, 0)
CloseButton.Size = UDim2.new(0.08, 0, 0.06, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.TextSize = 18

-- Propriedades do botão de alternar menu
ToggleMenuButton.Parent = ScreenGui
ToggleMenuButton.Position = UDim2.new(0, 10, 0, 10)
ToggleMenuButton.Size = UDim2.new(0, 80, 0, 30)
ToggleMenuButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
ToggleMenuButton.Text = "Menu"
ToggleMenuButton.TextColor3 = Color3.fromRGB(255, 255, 255)
ToggleMenuButton.Font = Enum.Font.SourceSansBold
ToggleMenuButton.TextSize = 18

-- Criação de botões com função utilitária
local function createButton(button, parent, position, text)
    button.Parent = parent
    button.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
    button.Position = position
    button.Size = UDim2.new(0.8, 0, 0.08, 0)
    button.Text = text
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 18
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
end

-- Criação dos botões no menu
createButton(FlyButton, Frame, UDim2.new(0.1, 0, 0.15, 0), "Fly")
createButton(SpeedButton, Frame, UDim2.new(0.1, 0, 0.25, 0), "Speed")
createButton(WallHackButton, Frame, UDim2.new(0.1, 0, 0.35, 0), "Wall Hack")
createButton(ESPButton, Frame, UDim2.new(0.1, 0, 0.45, 0), "ESP")
createButton(TeleportButton, Frame, UDim2.new(0.1, 0, 0.55, 0), "Teleportar")
createButton(VoidButton, Frame, UDim2.new(0.1, 0, 0.65, 0), "Void")
createButton(SpectateButton, Frame, UDim2.new(0.1, 0, 0.75, 0), "Espectar")
createButton(CreditsButton, Frame, UDim2.new(0.1, 0, 0.85, 0), "Créditos")

-- Configuração do slider para velocidade
SpeedSlider.Parent = Frame
SpeedSlider.Position = UDim2.new(0.1, 0, 0.9, 0)
SpeedSlider.Size = UDim2.new(0.8, 0, 0.05, 0)
SpeedSlider.BackgroundColor3 = Color3.fromRGB(40, 40, 40)

SliderBar.Parent = SpeedSlider
SliderBar.Size = UDim2.new(1, 0, 1, 0)
SliderBar.BackgroundColor3 = Color3.fromRGB(100, 100, 100)

SliderButton.Parent = SpeedSlider
SliderButton.Size = UDim2.new(0, 20, 1, 0)
SliderButton.Position = UDim2.new(0.5, -10, 0, 0)
SliderButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)
SliderButton.Text = ""
SliderButton.BorderSizePixel = 0

-- Lógica do Slider
local isDragging = false
SliderButton.MouseButton1Down:Connect(function()
    isDragging = true
end)
game:GetService("UserInputService").InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        isDragging = false
    end
end)
game:GetService("UserInputService").InputChanged:Connect(function(input)
    if isDragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local sliderPos = math.clamp(input.Position.X - SpeedSlider.AbsolutePosition.X, 0, SpeedSlider.AbsoluteSize.X)
        local speedValue = math.floor((sliderPos / SpeedSlider.AbsoluteSize.X) * 100)
        selectedSpeed = speedValue
        SliderButton.Position = UDim2.new(sliderPos / SpeedSlider.AbsoluteSize.X, -10, 0, 0)
    end
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
    local player = game.Players.LocalPlayer
    player.Character.Humanoid.WalkSpeed = selectedSpeed
end)
