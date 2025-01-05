local OrionLib = loadstring(jogo:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

Janela local = OrionLib:MakeWindow({
    Nome = "KALI LINUX",
    HidePremium = falso,
    SaveConfig = verdadeiro,
    ConfigFolder = "KALILINUXConfig"
})

-- Função de Notificação
função local notificar(título, texto)
    OrionLib:MakeNotification({
        Nome = título,
        Conteúdo = texto,
        Imagem = "rbxassetid://4483345998",
        Tempo = 5
    })
fim

-- Aba Geral
local GeralTab = Janela:CriarTab({
    Nome = "Geral",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botões de Funções Gerais
GeralTab:AddButton({
    Nome = "Mosca",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiOder-Fly-STABLE-23736"))()
        notificar("Voar", "Voar ativado!")
    fim
})

GeralTab:AddButton({
    Nome = "Carro Voador",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
        notify("Fly Car", "Fly Car ativado!")
    fim
})

-- Sem clipe
Conexão local noclip
função local toggleNoclip(enable)
    se habilitar então
        se não noclipConnection então
            noclipConnection = jogo:GetService("RunService").Stepped:Connect(função()
                para _, parte em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
                    se parte:IsA("BasePart") então
                        part.CanCollide = falso
                    fim
                fim
            fim)
        fim
        notify("Noclip", "Travessia de paredes ativada!")
    outro
        se noclipConnection então
            noclipConnection:Desconectar()
            noclipConnection = nulo
        fim
        para _, parte em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
            se parte:IsA("BasePart") então
                part.CanCollide = verdadeiro
            fim
        fim
        notify("Noclip", "Travessia de paredes desativada.")
    fim
fim

GeralTab:AddToggle({
    Nome = "Noclip",
    Padrão = falso,
    Retorno de chamada = toggleNoclip
})

-- Salto Infinito
conexão de salto local
função local toggleInfiniteJump(habilitar)
    se habilitar então
        se não jumpConnection então
            jumpConnection = jogo:GetService("UserInputService").JumpRequest:Connect(função()
                jogador local = jogo.Jogadores.JogadorLocal
                caractere local = player.Character ou player.CharacterAdded:Wait()
                humanoide local = personagem:WaitForChild("Humanoide")
                humanoide:ChangeState(Enum.HumanoidStateType.Jumping)
            fim)
        fim
        notify("Pulo Infinito", "Pulo infinito ativado!")
    outro
        se jumpConnection então
            jumpConnection:Desconectar()
            jumpConnection = nulo
        fim
        notify("Pulo Infinito", "Pulo infinito desativado.")
    fim
fim

GeralTab:AddToggle({
    Nome = "Pulo Infinito",
    Padrão = falso,
    Retorno de chamada = toggleInfiniteJump
})

-- Ajustar Altura do Pulo
GeralTab:AddTextbox({
    Nome = "Altura do Pulo",
    Padrão = "50",
    TextDisappear = verdadeiro,
    Retorno de chamada = função(valor)
        humanoide local = jogo.Jogadores.JogadorLocal.Personagem:FindFirstChild("Humanoide")
        se humanóide então
            humanoid.JumpPower = tonumber(valor)
            notify("Altura do Pulo", "Altura do pulso ajustada para " .. valor)
        fim
    fim
})

-- Ajustar Velocidade
GeralTab:AddTextbox({
    Nome = "Velocidade",
    Padrão = "20",
    TextDisappear = verdadeiro,
    Retorno de chamada = função(valor)
        humanoide local = jogo.Jogadores.JogadorLocal.Personagem:FindFirstChild("Humanoide")
        se humanóide então
            humanoid.WalkSpeed = tonumber(valor)
            notify("Velocidade", "Velocidade ajustada para " .. valor)
        fim
    fim
})

-- Aba Visual
VisualTab local = Janela:CriarTab({
    Nome = "Visual",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botões de ESP
GuiaVisual:AdicionarBotão({
    Nome = "ESP Nome",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/rSUGN1fK"))()
        notify("ESP", "ESP nome ativado!")
    fim
})

GuiaVisual:AdicionarBotão({
    Nome = "ESP Linhas",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP", "ESP linha ativada!")
    fim
})

-- Campo de Visão
função local toggleFOV(estado)
    se estado então
        jogo.Espaço de trabalho.Câmera atual.Campo de visão = 90
        notify("FOV", "Campo de visão ativado.")
    outro
        jogo.Espaço de trabalho.Câmera atual.Campo de visão = 70
        notify("FOV", "Campo de Visão desativado.")
    fim
fim

GuiaVisual:AdicionarAlternar({
    Nome = "Campo de Visão",
    Padrão = falso,
    Retorno de chamada = toggleFOV
})

-- Aba Jogadores
local JogadoresTab = Window:MakeTab({
    Nome = "Jogadores",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Funções dos Jogadores
JogadoresTab:AddButton({
    Nome = "Teletransporte",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://raw.githubusercontent.com/Infinity2346/Tect-Menu/main/Teleport%20Gui.lua"))()
        notify("Teleporte", "Teleporte ativado!")
    fim
})
local OrionLib = loadstring(jogo:HttpGet("https://raw.githubusercontent.com/shlexware/Orion/main/source"))()

Janela local = OrionLib:MakeWindow({
    Nome = "KALI LINUX",
    HidePremium = falso,
    SaveConfig = verdadeiro,
    ConfigFolder = "KALILINUXConfig"
})

-- Função de Notificação
função local notificar(título, texto)
    OrionLib:MakeNotification({
        Nome = título,
        Conteúdo = texto,
        Imagem = "rbxassetid://4483345998",
        Tempo = 5
    })
fim

-- Aba Geral
local GeralTab = Janela:CriarTab({
    Nome = "Geral",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botões de Funções Gerais
GeralTab:AddButton({
    Nome = "Mosca",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiOder-Fly-STABLE-23736"))()
        notificar("Voar", "Voar ativado!")
    fim
})

GeralTab:AddButton({
    Nome = "Carro Voador",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
        notify("Fly Car", "Fly Car ativado!")
    fim
})

-- Sem clipe
Conexão local noclip
função local toggleNoclip(enable)
    se habilitar então
        se não noclipConnection então
            noclipConnection = jogo:GetService("RunService").Stepped:Connect(função()
                para _, parte em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
                    se parte:IsA("BasePart") então
                        part.CanCollide = falso
                    fim
                fim
            fim)
        fim
        notify("Noclip", "Travessia de paredes ativada!")
    outro
        se noclipConnection então
            noclipConnection:Desconectar()
            noclipConnection = nulo
        fim
        para _, parte em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
            se parte:IsA("BasePart") então
                part.CanCollide = verdadeiro
            fim
        fim
        notify("Noclip", "Travessia de paredes desativada.")
    fim
fim

GeralTab:AddToggle({
    Nome = "Noclip",
    Padrão = falso,
    Retorno de chamada = toggleNoclip
})

-- Salto Infinito
conexão de salto local
função local toggleInfiniteJump(habilitar)
    se habilitar então
        se não jumpConnection então
            jumpConnection = jogo:GetService("UserInputService").JumpRequest:Connect(função()
                jogador local = jogo.Jogadores.JogadorLocal
                caractere local = player.Character ou player.CharacterAdded:Wait()
                humanoide local = personagem:WaitForChild("Humanoide")
                humanoide:ChangeState(Enum.HumanoidStateType.Jumping)
            fim)
        fim
        notify("Pulo Infinito", "Pulo infinito ativado!")
    outro
        se jumpConnection então
            jumpConnection:Desconectar()
            jumpConnection = nulo
        fim
        notify("Pulo Infinito", "Pulo infinito desativado.")
    fim
fim

GeralTab:AddToggle({
    Nome = "Pulo Infinito",
    Padrão = falso,
    Retorno de chamada = toggleInfiniteJump
})

-- Ajustar Altura do Pulo
GeralTab:AddTextbox({
    Nome = "Altura do Pulo",
    Padrão = "50",
    TextDisappear = verdadeiro,
    Retorno de chamada = função(valor)
        humanoide local = jogo.Jogadores.JogadorLocal.Personagem:FindFirstChild("Humanoide")
        se humanóide então
            humanoid.JumpPower = tonumber(valor)
            notify("Altura do Pulo", "Altura do pulso ajustada para " .. valor)
        fim
    fim
})

-- Ajustar Velocidade
GeralTab:AddTextbox({
    Nome = "Velocidade",
    Padrão = "20",
    TextDisappear = verdadeiro,
    Retorno de chamada = função(valor)
        humanoide local = jogo.Jogadores.JogadorLocal.Personagem:FindFirstChild("Humanoide")
        se humanóide então
            humanoid.WalkSpeed = tonumber(valor)
            notify("Velocidade", "Velocidade ajustada para " .. valor)
        fim
    fim
})

-- Aba Visual
VisualTab local = Janela:CriarTab({
    Nome = "Visual",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botões de ESP
GuiaVisual:AdicionarBotão({
    Nome = "ESP Nome",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/rSUGN1fK"))()
        notify("ESP", "ESP nome ativado!")
    fim
})

GuiaVisual:AdicionarBotão({
    Nome = "ESP Linhas",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP", "ESP linha ativada!")
    fim
})

-- Campo de Visão
função local toggleFOV(estado)
    se estado então
        jogo.Espaço de trabalho.Câmera atual.Campo de visão = 90
        notify("FOV", "Campo de visão ativado.")
    outro
        jogo.Espaço de trabalho.Câmera atual.Campo de visão = 70
        notify("FOV", "Campo de Visão desativado.")
    fim
fim

GuiaVisual:AdicionarAlternar({
    Nome = "Campo de Visão",
    Padrão = falso,
    Retorno de chamada = toggleFOV
})

-- Aba Jogadores
local JogadoresTab = Window:MakeTab({
    Nome = "Jogadores",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Funções dos Jogadores
JogadoresTab:AddButton({
    Nome = "Teletransporte",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://raw.githubusercontent.com/Infinity2346/Tect-Menu/main/Teleport%20Gui.lua"))()
        notify("Teleporte", "Teleporte ativado!")
    fim
})

JogadoresTab:AddButton({
    Nome = "BringParts",
    Retorno de chamada = função()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
        notify("BringParts", "BringParts ativado!")
    fim
})

-- Aba Configurações
localConfiguraçõesTab = Window:MakeTab({
    Nome = "Configurações",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botão Ignorar Chat
Guia Configurações:AddButton({
    Nome = "Ignorar bate-papo",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    fim
})

Guia Configurações:AddToggle({
    Nome = "Anti Vazio",
    Padrão = falso,
    Retorno de chamada = toggleAntiVoid
})

-- Anti Vazio
local antiVoidEnabled = falso
antiVoidConnection local

função local toggleAntiVoid(estado)
    antiVoidEnabled = estado
    se antiVoidEnabled então
        antiVoidConnection = jogo:GetService("RunService").Stepped:Connect(função()
            jogador local = jogo.Jogadores.JogadorLocal
            se player.Character e player.Character:FindFirstChild("HumanoidRootPart") então
                hrp local = jogador.Personagem.ParteRaizHumanoide
                se hrp.Position.Y < -10 então
                    hrp.CFrame = CFrame.novo(0, 50, 0)
                    notify("Anti Void", "Você foi salvo do vazio!")
                fim
            fim
        fim)
    outro
        se antiVoidConnection então
            antiVoidConnection:Disconnect()
            antiVoidConnection = nulo
        fim
        notify("Anti Void", "Anti Void desativado.")
    fim
fim

JogadoresTab:AddButton({
    Nome = "BringParts",
    Retorno de chamada = função()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
        notify("BringParts", "BringParts ativado!")
    fim
})

-- Aba Configurações
localConfiguraçõesTab = Window:MakeTab({
    Nome = "Configurações",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Botão Ignorar Chat
Guia Configurações:AddButton({
    Nome = "Ignorar bate-papo",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    fim
})

Guia Configurações:AddToggle({
    Nome = "Anti Vazio",
    Padrão = falso,
    Retorno de chamada = toggleAntiVoid
})

-- Anti Vazio
local antiVoidEnabled = falso
antiVoidConnection local

função local toggleAntiVoid(estado)
    antiVoidEnabled = estado
    se antiVoidEnabled então
        antiVoidConnection = jogo:GetService("RunService").Stepped:Connect(função()
            jogador local = jogo.Jogadores.JogadorLocal
            se player.Character e player.Character:FindFirstChild("HumanoidRootPart") então
                hrp local = jogador.Personagem.ParteRaizHumanoide
                se hrp.Position.Y < -10 então
                    hrp.CFrame = CFrame.novo(0, 50, 0)
                    notify("Anti Void", "Você foi salvo do vazio!")
                fim
            fim
        fim)
    outro
        se antiVoidConnection então
            antiVoidConnection:Disconnect()
            antiVoidConnection = nulo
        fim
        notify("Anti Void", "Anti Void desativado.")
    fim
fim
