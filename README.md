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

-- Botões de Funções Gerais
GeralTab:AddButton({
    Name = "Fly",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiOder-Fly-STABLE-23736"))()
        notify("Fly", "Fly ativado!")
    end
})

GeralTab:AddButton({
    Name = "Fly Car",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
    end
})

-- Noclip
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
    Callback = toggleTravessaParedes
})

-- Infinite Jump
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

-- Aba Visual
local VisualTab = Window:MakeTab({
    Name = "Visual",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Botões de ESP
VisualTab:AddButton({
    Name = "ESP Nome",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/rSUGN1fK"))()
        notify("ESP", "ESP nome ativado!")
    end
})

VisualTab:AddButton({
    Name = "ESP Linhas",
    Callback = function()
        loadstring(game:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP", "ESP linha ativado!")
    end
})

local Section = VisualTab:AddSection({
	Name = "Ativar/desativar"
})

-- Aba: Visual
Tabs.Main:AddParagraph({ Title ="FOV", Content = "Campo de Visão " })

-- Variável para armazenar o estado do FOV (ativo ou inativo)
local fovActive = false

-- Função de callback para o toggle
function toggleFov(state)
    fovActive = state
    if fovActive then
        print("FOV ativado. Você pode ajustar o valor do FOV.")
        -- Exemplo: defina o FOV inicial quando ativado
        setFOV(90)
    else
        print("FOV desativado. Voltando ao FOV padrão.")
        -- Exemplo: reverter para o FOV padrão quando desativado
        setFOV(70) -- Substitua 70 pelo valor padrão desejado
    end
end

-- Função para alterar o FOV
function setFOV(newFOV)
    -- Verifique se o valor de FOV está dentro de um intervalo aceitável (por exemplo, 30 a 320 graus)
    if newFOV < 30 or newFOV > 320 then
        print("FOV deve estar entre 30 e 320 graus.")
        return
    end

    -- Aqui você deve adicionar a função ou método específico do seu ambiente que altera o FOV
    -- Exemplo fictício: game.setCameraFOV(newFOV)
    game.setCameraFOV(newFOV)

    print("FOV alterado para " .. newFOV .. " graus.")
end

-- Adiciona o toggle com a função de callback
Tab:AddToggle({
    Name = "Campo de Visão",
    Default = false,
    Callback = togglecampodevisão
})

-- Aba Jogadores
local JogadoresTab = Window:MakeTab({
    Name = "Jogadores",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Funções de Jogadores
JogadoresTab:AddButton({
    Name = "Teleport",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/Infinity2346/Tect-Menu/main/Teleport%20Gui.lua"))()
        notify("Teleport", "Teleport ativado!")
    end
})

JogadoresTab:AddButton({
    Name = "BringParts",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
    end
})

-- Aba Configurações
localConfiguraçõesTab = Window:MakeTab({
    Name = "Configurações",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Botão Chat Bypass
ConfiguraçõesTab:AddButton({
    Name = "Chat Bypass",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    end
})

local Section = ConfiguraçõesTab:AddSection({
	Name = "Configuração do Personagem"
})

-- Função para resetar o personagem
local function resetCharacter()
    local player = game.Players.LocalPlayer
    if player.Character then
        player.Character:BreakJoints()  -- Reseta o personagem
        notify("Resetar", "Personagem resetado!")
    end
end

-- Botão para resetar o personagem
ConfiguraçõesTab:AddButton({
    Name = "Resetar Personagem",
    Callback = resetCharacter
})

-- Botão para Anti lag
ConfiguraçõesTab:AddButton({
    Name = "Anti lag",
    Callback = function()
        -- Aciona a verificação anti-lag para todos os jogadores
        local Players = game:GetService("Players")
        for _, player in ipairs(Players:GetPlayers()) do
            if player.Character then
                antiLagCheck(player)
            end
        end
    end
})

-- Anti-Lag Script (Server Side)
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local MAX_PARTS_PER_CHARACTER = 50  -- Limite de partes por personagem
local MAX_DISTANCE_FROM_ORIGIN = 1000  -- Distância máxima do personagem do ponto de origem

-- Função para verificar o número de partes do personagem
local function checkPartsCount(player)
    local character = player.Character
    if character then
        local partCount = 0
        for _, part in pairs(character:GetChildren()) do
            if part:IsA("BasePart") then
                partCount = partCount + 1
            end
        end
        
        if partCount > MAX_PARTS_PER_CHARACTER then
            -- Remova as partes adicionais ou desconecte o jogador
            player:Kick("Hack detectado: Número excessivo de partes no personagem!")
            warn(player.Name .. " foi expulso por ter muitas partes no personagem.")
        end
    end
end

-- Função para verificar a distância do personagem em relação à origem (evitar lugares impossíveis)
local function checkPlayerPosition(player)
    local character = player.Character
    if character then
        local humanoidRootPart = character:FindFirstChild("HumanoidRootPart")
        if humanoidRootPart then
            local distance = humanoidRootPart.Position.Magnitude
            if distance > MAX_DISTANCE_FROM_ORIGIN then
                player:Kick("Hack detectado: Posição excessiva!")
                warn(player.Name .. " foi expulso por estar longe demais da origem.")
            end
        end
    end
end

-- Função de verificação de lag para cada jogador
local function antiLagCheck(player)
    -- Verifique o número de partes do personagem
    checkPartsCount(player)
    
    -- Verifique a distância do personagem da origem
    checkPlayerPosition(player)
end

-- Verifique todos os jogadores no servidor periodicamente
RunService.Heartbeat:Connect(function()
    for _, player in ipairs(Players:GetPlayers()) do
        if player.Character then
            antiLagCheck(player)
        end
    end
end)

-- Anti-Lag Script (Client Side)
local UserInputService = game:GetService("UserInputService")

-- Função de monitoramento de FPS
local function monitorFPS()
    local lastTime = tick()
    local frameCount = 0
    local maxFrames = 60  -- Máximo de 60 FPS
    
    -- Monitoramento a cada segundo (ajuste conforme necessário)
    while true do
        wait(1)
        local deltaTime = tick() - lastTime
        frameCount = frameCount + 1
        
        -- Se a quantidade de frames por segundo exceder o limite, desconectar o jogador
        if deltaTime >= 1 then
            if frameCount > maxFrames then
                game.Players.LocalPlayer:Kick("Hack detectado: FPS excessivo!")
                warn(game.Players.LocalPlayer.Name .. " foi expulso por FPS excessivo.")
            end
            lastTime = tick()
            frameCount = 0
        end
    end
end

-- Iniciar o monitoramento de FPS no cliente
monitorFPS()
