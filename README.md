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
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Vitoarieshub/Fly-universal-/main/Fly.lua"))()
        notify("Fly", "Fly ativado!")
    end
})

-- Função Fly Car
GeralTab:AddButton({
    Name = "Fly Car",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/TxzeBi3F"))()
        notify("Fly Car", "Fly Car ativado!")
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
        notify("Travessa Paredes", "Travessa Paredes desativado.")
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
        notify("Pulo Infinito", "Pulo infinito ativado!")
    else
        if jumpConnection then
            jumpConnection:Disconnect()
            jumpConnection = nil
        end
        notify("Pulo Infinito", "Pulo infinito desativado.")
    end
end

GeralTab:AddToggle({
    Name = "Pulo Infinito",
    Default = false,
    Callback = toggleInfiniteJump
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
            notify("Altura do Pulo", "Altura do Pulo ajustada para " .. value)
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
            notify("Velocidade", "Velocidade ajustada para " .. value)
        end
    end
})

GeralTab:AddButton({
    Name = "Resetar Velocidade e Pulo",
    Callback = function()
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:FindFirstChildOfClass("Humanoid")

        if humanoid then
            humanoid.WalkSpeed = 16 -- Velocidade padrão do Roblox
            humanoid.JumpPower = 50 -- Altura do pulo padrão do Roblox
            notify("Resetado", "Velocidade e Altura do Pulo foram resetadas!")
        else
            notify("Erro", "Humanoide não encontrado!")
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
        notify("ESP", "ESP nome ativado!")
    end
})

VisuaisTab:AddButton({
    Name = "ESP Linhas",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP", "ESP linhas ativado!")
    end
})

-- Função para ajustar FOV
local function setFOV(newFOV)
    if newFOV < 30 or newFOV > 120 then
        notify("Erro", "FOV deve estar entre 30 e 120 graus.")
        return
    end
    game:GetService("Workspace").CurrentCamera.FieldOfView = newFOV
    notify("Campo de Visão", "Campo de Visão alterado para " .. newFOV .. " graus.")
end

-- Alternar Campo de Visão (FOV)
local fovActive = false
local function toggleFov(state)
    fovActive = state
    if fovActive then
        setFOV(120)
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
        notify("Erro", "Jogador não encontrado ou não tem HumanoidRootPart.")
    end
end

-- Função para parar de espectar e voltar para o personagem local
local function stopSpectating()
    workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:WaitForChild("Humanoid")
    notify("Espectador", "Você parou de espectar o jogador.")
end

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
        notify("Troll", "Troll ativado!")
    end
})

TrollTab:AddButton({
    Name = "BringParts",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/QmNv5KYh"))()
        notify("BringParts", "BringParts ativado!")
    end
})

TrollTab:AddButton({
    Name = "Teleporte menu",
    Callback = function()
        loadstring(game:HttpGet('https://pastebin.com/raw/ynP6WYDn'))()
        notify("Teleporte", "Teleporte ativado!")
    end
})

TrollTab:AddButton({
    Name = "Chat Bypass",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/vrMt6p4y"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    end
})

-- Aba Configuração
local ConfiguraçãoTab = Window:MakeTab({
    Name = "Configuração",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

ConfiguraçãoTab:AddButton({
    Name = "Anti-Kick",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/w1xj2UrR"))()
        notify("Anti Kick", "Anti Kick ativado!")
    end
})
