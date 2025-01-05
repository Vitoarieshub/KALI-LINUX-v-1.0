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

ConfiguraçõesTab:AddToggle({
    Name = "Anti void",
    Default = false,
    Callback = toggleIantivoid
})

local function enableAntiVoid()
    -- Definir o limite do vazio (abaixo desse ponto, o jogador será reposicionado)
    local threshold = -10
    -- Definir a posição segura para reposicionar o jogador
    local safePosition = Vector3.new(0, 50, 0)

    -- Conectar a função ao evento Stepped do RunService para verificar constantemente a posição do jogador
    game:GetService("RunService").Stepped:Connect(function()
        local player = game.Players.LocalPlayer
        if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            local hrp = player.Character.HumanoidRootPart
            -- Se o jogador estiver abaixo do limite, reposicioná-lo
            if hrp.Position.Y < threshold then
                hrp.CFrame = CFrame.new(safePosition)
                print("Anti Void: Jogador reposicionado para evitar cair no vazio.")
            end
        end
    end)
end

-- Ativar o Anti Void ao executar o script
enableAntiVoid()
