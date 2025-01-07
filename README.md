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

-- Função Fly
GeralTab:AddButton({
    Nome = "Mosca",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-AntiOder-Fly-STABLE-23736"))()
        notificar("Voar", "Voar ativado!")
    fim
})

-- Função Fly Car
GeralTab:AddButton({
    Nome = "Carro Voador",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-Car-Mobile-gui-11884"))()
        notify("Fly Car", "Fly Car ativado!")
    fim
})

-- Função Noclip
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
        notify("Noclip", "Você pode atravessar paredes agora!")
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
        notify("Noclip", "Travessa Paredes desativada.")
    fim
fim

GeralTab:AddToggle({
    Nome = "Travessa Paredes",
    Padrão = falso,
    Retorno de chamada = toggleNoclip
})

-- Função Pulo Infinito
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
            notify("Altura do Pulo", "Altura do Pulo ajustada para " .. valor)
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
local VisuaIsTab = Janela:CriarTab({
    Nome = "Visuais",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Funções de ESP
VisualizarTab:AdicionarBotão({
    Nome = "ESP Nome",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/rSUGN1fK"))()
        notify("ESP", "ESP nome ativado!")
    fim
})

VisualizarTab:AdicionarBotão({
    Nome = "ESP Linhas",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/nnHbfvGW"))()
        notify("ESP", "ESP linhas ativadas!")
    fim
})

-- Função para ajustar FOV
função local setFOV(newFOV)
    se newFOV < 30 ou newFOV > 120 então
        notify("Erro", "FOV deve estar entre 30 e 120 graus.")
        retornar
    fim
    jogo:GetService("Espaço de trabalho").CurrentCamera.FieldOfView = novoFOV
    notify("Campo de Visão", "Campo de Visão alterado para " .. newFOV .. " graus.")
fim

-- Alternar Campo de Visão (FOV)
local fovActive = falso
função local toggleFov(estado)
    fovActive = estado
    se fovActive então
        definirFOV(90)
    outro
        definirFOV(70)
    fim
fim

VisualizarTab:AdicionarAlternar({
    Nome = "Campo de Visão",
    Padrão = falso,
    Retorno de chamada = toggleFov
})

-- Aba Jogador
local JogadorTab = Window:MakeTab({
    Nome = "Jogador",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Função para Espectar outro jogador
função local spectatePlayer(playerName)
    local localPlayer = jogo.Jogadores.LocalPlayer
    jogador local = jogo.Jogadores:FindFirstChild(playerName)

    se jogador e jogador.Personagem e jogador.Personagem:FindFirstChild("HumanoidRootPart") então
        humanoide local = localPlayer.Character:FindFirstChildOfClass("Humanoide")
        se humanóide então
            humanoid.PlatformStand = falso
            humanoid.Sit = falso
        fim
        
        para _, parte em pares(localPlayer.Character:GetDescendants()) faça
            se parte:IsA("BasePart") então
                part.CanCollide = falso
            fim
        fim

        espaço de trabalho.CurrentCamera.CameraSubject = jogador.Personagem.HumanoidRootPart
        notify("Espectar", "Você está esperando " .. playerName)
    outro
        notify("Erro", "Jogador não encontrado.")
    fim
fim

função local stopSpectating()
    local localPlayer = jogo.Jogadores.LocalPlayer
    espaço de trabalho.CurrentCamera.CameraSubject = localPlayer.Character:FindFirstChildOfClass("Humanoid")

    para _, parte em pares(localPlayer.Character:GetDescendants()) faça
        se parte:IsA("BasePart") então
            part.CanCollide = verdadeiro
        fim
    fim

    notify("Espectar", "Você parou de Espectar.")
fim

função local updatePlayerList(dropdown)
    nomes de jogadores locais = {}
    para _, jogador em ipairs(game.Players:GetPlayers()) faça
        tabela.insert(playerNames, jogador.Nome)
    fim
    dropdown:Atualizar(playerNames, true)
fim

playerDropdown local = JogadorTab:AddDropdown({
    Nome = "Espectar Jogador",
    Opções = {},
    Padrão = nulo,
    Retorno de chamada = função(jogador selecionado)
        espectadorJogador(jogador selecionado)
    fim
})

JogadorTab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Retorno de chamada = função()
        atualizarPlayerList(playerDropdown)
        notify("Atualizar Lista", "Lista de jogadores atualizada!")
    fim
})

atualizarPlayerList(playerDropdown)

jogo.Jogadores.JogadorAdicionado:Conectar(função()
    atualizarPlayerList(playerDropdown)
fim)

jogo.Jogadores.JogadorRemovendo:Conectar(função()
    atualizarPlayerList(playerDropdown)
fim)

local Jogador = Tab:AddSection({
	Name = "Teleporte"
})

função local teleportToPlayer(playerName)
    jogador local = jogo.Jogadores:FindFirstChild(playerName)
    se jogador e jogador.Personagem e jogador.Personagem:FindFirstChild("HumanoidRootPart") então
        personagem local = jogo.Jogadores.JogadorLocal.Personagem
        se personagem então
            personagem: MoveTo (jogador. Personagem. HumanoidRootPart. Posição)
            notify("Teleporte", "Teletransportado para " .. playerName)
        fim
    outro
        notify("Erro", "Jogador ou parte do jogador não encontrado.")
    fim
fim

jogador localTeleportDropdown = JogadorTab:AddDropdown({
    Name = "Teletransportar para Jogador",
    Opções = {},
    Padrão = nulo,
    Retorno de chamada = função(jogador selecionado)
        teleportToPlayer(jogador selecionado)
    fim
})

JogadorTab:AddButton({
    Name = "Atualizar Lista de Jogadores",
    Retorno de chamada = função()
        updatePlayerList(playerTeleportDropdown)
        notify("Atualizar Lista", "Lista de jogadores atualizada!")
    fim
})

updatePlayerList(playerTeleportDropdown)

jogo.Jogadores.JogadorAdicionado:Conectar(função()
    updatePlayerList(playerTeleportDropdown)
fim)

jogo.Jogadores.JogadorRemovendo:Conectar(função()
    updatePlayerList(playerTeleportDropdown)
fim)

-- Função de teleporte
JogadorTab:AddButton({
    Nome = "Teleporte 2",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet('https://raw.githubusercontent.com/Infinity2346/Tect-Menu/main/Teleport%20Gui.lua'))()
        notify("Teleporte", "Teleporte ativado!")
    fim
})

-- Aba Troll
local TrollTab = Janela:CriarTab({
    Nome = "Troll",
    Ícone = "rbxassetid://4483345998",
    PremiumOnly = falso
})

-- Funções de Troll
TrollTab:AdicionarBotão({
    Nome = "BringParts",
    Retorno de chamada = função()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Better-Bring-Parts-Ui-SOLARA-and-Fixed-Lags-21780"))()
        notify("BringParts", "BringParts ativado!")
    fim
})

TrollTab:AdicionarBotão({
    Nome = "Troll",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://pastebin.com/raw/38Jra00x"))()
        notify("Troll", "Troll ativado!")
    fim
})

TrollTab:AdicionarBotão({
    Nome = "Ignorar bate-papo",
    Retorno de chamada = função()
        loadstring(jogo:HttpGet("https://raw.githubusercontent.com/AlgariBot/lua/refs/heads/Lua-Script-Executor/LocalNeverPatchedBypass.txt"))()
        notify("Chat Bypass", "Chat Bypass ativado!")
    fim
})
