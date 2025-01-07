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
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiOder-Fly-STABLE-23736"))()
        notify("Fly", "Fly ativado!")
    end
})

-- Função Fly Car
GeralTab:AddButton({
    Name = "Fly Car",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
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
        notify("Noclip", "Você pode atravessar paredes agora!")
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
        notify("Noclip", "Travessa Paredes desativado.")
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
    if newFOV < 30 or newFOV > 320 then
        notify("Erro", "FOV deve estar entre 30 e 320 graus.")
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
        setFOV(90)
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
        notify("Erro", "Jogador ou parte do jogador não encontrado.")
    end
end

-- Atualizar Lista de Jogadores
local function updatePlayerList(dropdown)
    local playerNames = {}
    for _, player in ipairs(game.Players:GetPlayers()) do
        table.insert(playerNames, player.Name)
    end
    dropdown:Refresh(playerNames, true)
end

-- Dropdown de Seleção de Jogador
local playerDropdown = JogadorTab:AddDropdown({
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
        updatePlayerList(playerDropdown)
        notify("Atualizar Lista", "Lista de jogadores atualizada!")
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

-- Funções de Troll
TrollTab:AddButton({
    Name = "BringParts",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
        notify("BringParts", "BringParts ativado!")
    end
})

TrollTab:AddButton({
    Name = "Troll",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/38Jra00x"))()
        notify("Troll", "Troll ativado!")
    end
})

-- Função Chat Bypass
TrollTab:AddButton({
    Name = "Chat Bypass",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    end
})
