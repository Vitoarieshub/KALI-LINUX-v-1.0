local OrionLib = loadstring(game:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

local Window = OrionLib:MakeWindow({
    Name = "KALI LINUX",
    HidePremium = false,
    SaveConfig = true,
    ConfigFolder = "KALILINUXConfig"
})

-- Função de Notificação
local function notify(title, text)
    OrionLib:MakeNotification({
        Name = title,
        Content = text,
        Image = "rbxassetid://4483345998",
        Time = 5
    })
end

-- Aba Geral
local GeralTab = Window:MakeTab({
    Name = "Geral",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Função Fly
GeralTab:AddButton({
    Name = "Fly",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Vitoarieshub/Fly-universal-/refs/heads/main/README.md"))()
        notify("Fly", "Ativado!")
    end
})

-- Função Fly Car
GeralTab:AddButton({
    Name = "Fly Car",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
        notify("Fly Car", "Ativado!")
    end
})

-- Função Noclip
local noclipConnection
local function toggleNoclip(enable)
    if enable then
        if not noclipConnection then
            noclipConnection = game:GetService("RunService").Stepped:Connect(function()
                for _, part in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = false
                    end
                end
            end)
        end
        notify("Travessa Paredes", "Você pode atravessar paredes agora!")
    else
        if noclipConnection then
            noclipConnection:Disconnect()
            noclipConnection = nil
        end
        for _, part in pairs(game.Players.LocalPlayer.Character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
        notify("Travessa Paredes", "Desativado.")
    end
end

GeralTab:AddToggle({
    Name = "Travessa Paredes",
    Default = false,
    Callback = toggleNoclip
})

-- Função Pulo Infinito
local jumpConnection
local function toggleInfiniteJump(enable)
    if enable then
        if not jumpConnection then
            jumpConnection = game:GetService("UserInputService").JumpRequest:Connect(function()
                local player = game.Players.LocalPlayer
                local character = player.Character or player.CharacterAdded:Wait()
                local humanoid = character:WaitForChild("Humanoid")
                humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
            end)
        end
        notify("Pulo Infinito", "Ativado!")
    else
        if jumpConnection then
            jumpConnection:Disconnect()
            jumpConnection = nil
        end
        notify("Pulo Infinito", "Desativado.")
    end
end

GeralTab:AddToggle({
    Name = "Pulo Infinito",
    Default = false,
    Callback = toggleInfiniteJump
})

-- Função para definir a gravidade com base no valor digitado
GeralTab:AddTextbox({
    Name = "Gravidade",
    Default = "196.2",  -- Valor padrão de gravidade no Roblox
    TextDisappear = true,
    Callback = function(value)
        local gravityValue = tonumber(value)
        if gravityValue then
            -- Ajusta a gravidade do jogo
            game.Workspace.Gravity = gravityValue
            notify("Gravidade", "Foi ajustada para " .. value .. ".")
        else
            notify("Erro", "Por favor, digite um valor numérico para gravidade.")
        end
    end
})

-- Ajustar Altura do Pulo
GeralTab:AddTextbox({
    Name = "Altura do Pulo",
    Default = "50",
    TextDisappear = true,
    Callback = function(value)
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.JumpPower = tonumber(value)
            notify("Altura do Pulo", "Ajustada para " .. value)
        end
    end
})

-- Ajustar Velocidade
GeralTab:AddTextbox({
    Name = "Velocidade",
    Default = "20",
    TextDisappear = true,
    Callback = function(value)
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = tonumber(value)
            notify("Velocidade", "Ajustada para " .. value)
        end
    end
})

GeralTab:AddButton({
    Name = "Resetar Velocidade Pulo e Gravidade",
    Callback = function()
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")

        if humanoid then
            humanoid.WalkSpeed = 20 -- Velocidade padrão do Roblox
            humanoid.JumpPower = 50 -- Altura do pulo padrão do Roblox
            game.Workspace.Gravity = 196.2  -- Gravidade padrão do Roblox
            notify("Resetado", "Velocidade  Altura do Pulo e Gravidade foram resetadas!")
        else
            notify("Erro", "não encontrado!")
        end
    end
})

-- Aba Visuais
local VisuaisTab = Window:MakeTab({
    Name = "Visuais",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Funções de ESP
VisuaisTab:AddButton({
    Name = "ESP Nome",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/rSUGN1fK"))()
        notify("ESP Nome", "Ativado!")
    end
})

VisuaisTab:AddButton({
    Name = "ESP Linhas",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP Linhas", "Ativado!")
    end
})

-- Função para ajustar FOV
local function setFOV(newFOV)
    if newFOV < 30 or newFOV > 300 then
        notify("Erro", "FOV deve estar entre 30 e 300 graus.")
        return
    end
    game:GetService("Workspace").CurrentCamera.FieldOfView = newFOV
    notify("Campo de Visão", "Alterado para " .. newFOV .. " graus.")
end

-- Alternar Campo de Visão (FOV)
local fovActive = false
local function toggleFov(state)
    fovActive = state
    if fovActive then
        setFOV(300)
    else
        setFOV(70)
    end
end

VisuaisTab:AddToggle({
    Name = "Campo de Visão",
    Default = false,
    Callback = toggleFov
})

-- Aba Jogador
local JogadorTab = Window:MakeTab({
    Name = "Jogador",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

local playerDropdown
local EspectarConnection

-- Função para atualizar a lista de jogadores no dropdown
local function updatePlayerList(dropdown)
    local playerNames = {}
    for _, player in ipairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    dropdown:Refresh(playerNames, true)
end

-- Função para começar a espectar o jogador
local function spectatePlayer(playerName)
    local localPlayer = game.Players.LocalPlayer
    local player = game.Players:FindFirstChild(playerName)

    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        workspace.CurrentCamera.CameraSubject = player.Character.HumanoidRootPart
        notify("Espectador", "Você está agora espectando: " .. playerName)
    else
        notify("Erro", "Jogador não encontrado.")
    end
end

-- Função para parar de espectar e voltar para o personagem local
local function stopSpectating()
    workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:WaitForChild("Humanoid")
    notify("Espectador", "Você parou de espectar ó jogador .")
end

local Section = JogadorTab:AddSection({
	Name = "Espectar"
})

-- Criação do Dropdown para escolher o jogador para espectar
playerDropdown = JogadorTab:AddDropdown({
    Name = "Espectar Jogador",
    Options = {},
    Callback = function(selectedPlayer)
        spectatePlayer(selectedPlayer)
    end
})

-- Botão para Atualizar a Lista de Jogadores
JogadorTab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Callback = function()
        updatePlayerList(playerDropdown)
        notify("Atualizar Lista", "Lista de jogadores atualizada!")
    end
})

-- Botão para Parar de Espectar
JogadorTab:AddButton({
    Name = "Parar de Espectar",
    Callback = function()
        stopSpectating()
    end
})

-- Inicializar a Lista de Jogadores ao Carregar o Script
updatePlayerList(playerDropdown)

-- Eventos para Atualizar a Lista quando um Jogador Entra ou Sai
game.Players.PlayerAdded:Connect(function()
    updatePlayerList(playerDropdown)
end)

game.Players.PlayerRemoving:Connect(function()
    updatePlayerList(playerDropdown)
end)

local teleportDropdown

-- Função para atualizar a lista de jogadores no dropdown
local function updatePlayerList(dropdown)
    local playerNames = {}
    for _, player in ipairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    dropdown:Refresh(playerNames, true)
end

-- Função para teleportar para outro jogador
local function teleportToPlayer(playerName)
    local player = game.Players:FindFirstChild(playerName)
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local character = game.Players.LocalPlayer.Character
        if character then
            character:MoveTo(player.Character.HumanoidRootPart.Position)
            notify("Teleporte", "Teleportado para " .. playerName)
        end
    else
        notify("Erro", "Jogador não encontrado.")
    end
end

local Section = JogadorTab:AddSection({
	Name = "Teleporta"
})

-- Dropdown de Seleção de Jogador para teleportar
teleportDropdown = JogadorTab:AddDropdown({
    Name = "Teleportar para Jogador",
    Options = {},
    Default = nil,
    Callback = function(selectedPlayer)
        teleportToPlayer(selectedPlayer)
    end
})

-- Botão para Atualizar Lista de Jogadores
JogadorTab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Callback = function()
        updatePlayerList(teleportDropdown)
        notify("Atualizar Lista", "Lista de jogadores atualizada!")
    end
})

-- Inicializar a Lista de Jogadores ao Carregar o Script
updatePlayerList(teleportDropdown)

-- Eventos para Atualizar a Lista quando um Jogador Entra ou Sai
game.Players.PlayerAdded:Connect(function()
    updatePlayerList(teleportDropdown)
end)

game.Players.PlayerRemoving:Connect(function()
    updatePlayerList(teleportDropdown)
end)

-- Aba Troll
local TrollTab = Window:MakeTab({
    Name = "Troll",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

TrollTab:AddButton({
    Name = "Troll",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/38Jra00x"))()
        notify("Troll", "Ativado!")
    end
})

TrollTab:AddButton({
    Name = "BringParts",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
        notify("BringParts", "Ativado!")
    end
})

TrollTab:AddButton({
    Name = "Teleporte menu",
    Callback = function()
        loadstring(game:HttpGet('https://raw.githubusercontent.com/Infinity2346/Tect-Menu/main/Teleport%20Gui.lua'))()
        notify("Teleporte", "Ativado!")
    end
})

TrollTab:AddButton({
    Name = "Chat Bypass",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Ativado!")
    end
})

local Section = TrollTab:AddSection({
	Name = "configuração"
})

TrollTab:AddButton({
    Name = "Anti Kick",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Exunys/Anti-Kick/main/Anti-Kick.lua"))()
        notify("Anti Kick", "Ativado!")
    end
})

-- Função para aplicar o boost de FPS
local function applyFPSBoost()
    settings().Rendering.QualityLevel = Enum.QualityLevel.Level01
    game:GetService("Lighting").GlobalShadows = false

    for _, v in pairs(game:GetService("Workspace"):GetDescendants()) do
        if v:IsA("Part") or v:IsA("UnionOperation") or v:IsA("MeshPart") then
            v.Material = Enum.Material.SmoothPlastic
            v.Reflectance = 0
        elseif v:IsA("Decal") or v:IsA("Texture") then
            v:Destroy()
        elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
            v:Destroy()
        elseif v:IsA("PointLight") or v:IsA("SpotLight") or v:IsA("SurfaceLight") then
            v:Destroy()
        end
    end

    game:GetService("Workspace").CurrentCamera.FieldOfView = 70
    game:GetService("Workspace").CurrentCamera.MaxDistance = 500
    notify("FPS Boost", "Ativado com sucesso!")
end

-- Função para reverter as mudanças e voltar à qualidade normal
local function revertFPSBoost()
    settings().Rendering.QualityLevel = Enum.QualityLevel.Automatic
    game:GetService("Lighting").GlobalShadows = true
    notify("FPS Boost", "Desativado.")
end

local isFPSBoostActive = false  -- Inicia com o boost desativado

-- Função para alternar entre aplicar e reverter o boost de FPS
local function toggleFPSBoost()
    if isFPSBoostActive then
        revertFPSBoost()
    else
        applyFPSBoost()
    end
    isFPSBoostActive = not isFPSBoostActive
end

-- Botão para alternar o boost de FPS
TrollTab:AddButton({
    Name = "Boost FPS",
    Callback = function()
        toggleFPSBoost()
    end
})

OrionLib:Init()

local isMorning = false  -- Variável para controlar o estado da iluminação

-- Função para ajustar a iluminação para parecer de manhã
local function setMorningLighting()
    local lighting = game:GetService("Lighting")

    lighting.TimeOfDay = "07:00:00"  -- Define o horário para 7 da manhã
    lighting.Brightness = 2          -- Define o brilho
    lighting.ClockTime = 7           -- Ajusta o tempo do relógio
    lighting.OutdoorAmbient = Color3.fromRGB(175, 221, 255)  -- Cor de luz suave matinal
    lighting.FogEnd = 300            -- Define o fim da neblina
    lighting.FogColor = Color3.fromRGB(255, 244, 214)  -- Cor da neblina para um tom matinal
    lighting.GlobalShadows = true

    notify("Iluminação", "Agora é de manhã!")
end

-- Função para reverter a iluminação para a configuração original
local function resetLighting()
    local lighting = game:GetService("Lighting")

    lighting.TimeOfDay = "14:00:00"  -- Define o horário para 14 horas (2 da tarde)
    lighting.Brightness = 3          -- Ajusta o brilho de volta
    lighting.ClockTime = 14          -- Ajusta o tempo do relógio de volta
    lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)  -- Cor padrão
    lighting.FogEnd = 100000         -- Remove a neblina
    lighting.FogColor = Color3.fromRGB(255, 255, 255)  -- Cor padrão da neblina
    lighting.GlobalShadows = true

    notify("Iluminação", "Iluminação padrão restaurada!")
end

-- Função para alternar entre ativar e desativar a iluminação matinal
local function toggleLighting()
    if isMorning then
        resetLighting()
    else
        setMorningLighting()
    end
    isMorning = not isMorning  -- Inverte o estado
end

-- Botão para alternar a iluminação
TrollTab:AddButton({
    Name = "Deixa de Manhã",
    Callback = function()
        toggleLighting()
    end
})

-- Inicialização da interface OrionLib
OrionLib:Init()
