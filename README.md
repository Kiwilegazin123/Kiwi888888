--carregar biblioteca 📖
local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()


--janela principal🖥️
local Window = Fluent:CreateWindow({
    Title = "Fluent " .. Fluent.Version,
    TabWidth = 160, 
    Size = UDim2.fromOffset(580, 460),
    Theme = "Dark"
})


    Key = {
    KeySystem = false,
    Title = "Key System",
    Description = "Wolfpaq",
    KeyLink = "Wolfpaq",
    Keys = {"Wolfpaq"},
    Notifi = {
      Notifications = true,
      CorrectKey = "Running the Script...",
      Incorrectkey = "The key is incorrect",
      CopyKeyLink = "Copied to Clipboard"
    }
  }
})

MinimizeButton({
  Image = "rbxassetid://17802167990",
  Size = {42, 42},
  Color = Color3.fromRGB(0, 0, 0),
  Corner = true,
  Stroke = true,
  StrokeColor = Color3.fromRGB(255, 255, 255)
})

-- ID do som a ser reproduzido quando o código for executado
local soundId = "rbxassetid://1836973601"

-- Função para tocar o som
local function playSound()
    local sound = Instance.new("Sound")
    sound.SoundId = soundId
    sound.Parent = game.Workspace -- Coloque no Workspace para garantir que seja ouvido
    sound:Play()
end

-- Tocar o som assim que o script for executado
playSound()

local Main = MakeTab({Name = "Welcome"})

-- Create a label to show the number of players
local playerCountLabel = AddTextLabel(Main, "Jogadores No Servidor: " .. #game.Players:GetPlayers())

-- Função para atualizar o número de jogadores quando alguém entra ou sai
local function updatePlayerCount()
    playerCountLabel.Text = "Jogadores No Servidor: " .. #game.Players:GetPlayers()
end

-- Conecta a função ao evento de entrada de novos jogadores
game.Players.PlayerAdded:Connect(updatePlayerCount)

-- Conecta a função ao evento de saída de jogadores
game.Players.PlayerRemoving:Connect(updatePlayerCount)

-- Atualiza a contagem de jogadores no início (caso tenha jogadores ao carregar o script)
updatePlayerCount()

-- Criando a TextLabel
local Label = AddTextLabel(Main, "")

-- Função para atualizar o tempo na TextLabel
local function updateTime(label)
    while true do
        local currentTime = os.date("%H:%M:%S")
        label.Text = "Hora atual: " .. currentTime
        wait(1)  -- Atualiza a cada segundo
    end
end

-- Iniciando a atualização da TextLabel
coroutine.wrap(updateTime)(Label)

local Label = AddTextLabel(Main,
{"Welcome To Shnmaxhub"})
local Label = AddTextLabel(Main,
{"Team | Shnmaxscripts"})
local Label = AddTextLabel(Main,
{"Script Development Helpers: XXXTENTACION The Lucca"})
local Label = AddTextLabel(Main,
{"Last Update to Hub: 19/Day/2024/Year/Jun/Month"})
local Label = AddTextLabel(Main,
{"Code Developed By: Shnmaxscripts Owner"})
local Label = AddTextLabel(Main,
{"Use Responsibly"})
local Label = AddTextLabel(Main,
{"Have a Great Experience!"})

local Main = MakeTab({Name = "Trolling"})

local Label = AddTextLabel(Main,
{"Aviso [!] Use Conforme Sua Responsabilidade"})

local section = AddSection(Main, {"Selecione um Método de Fling"})

-- Interface para Selecionar Método de Kill
local killMethodDropdown = AddDropdown(Main, {
    Name = "Selecionar Método De Kill",
    Default = "Couch",
    Options = {"Nenhum", "Couch"},
    Callback = function(value)
        if value == "Couch" then
            local args = {
                [1] = "PickingTools",
                [2] = "Couch"
            }
            game:GetService("ReplicatedStorage").RE:FindFirstChild("1Too1l"):InvokeServer(unpack(args))
            print('Hello!')
        elseif value == "Nenhum" then
            -- Código a ser executado quando "Nenhum" for selecionado
            print("Nenhum método selecionado.")
        end
    end
})

local section = AddSection(Main, {"Matar Jogadores"})

-- Serviços necessários
local playerService = game:GetService('Players')
local runService = game:GetService('RunService')
local localPlayer = playerService.LocalPlayer
local backpack = localPlayer:FindFirstChildOfClass('Backpack')

-- Variáveis globais
local flingV14Toggle = false
local selectedFlingPlayerV14 = nil
local flingV14Connection
local playerSpawnedConnection
local spinFlingConnection
local bodyThrust

-- Função para obter a lista de jogadores
local function getPlayerList()
    local playerList = {}
    for _, player in ipairs(playerService:GetPlayers()) do
        if player ~= localPlayer then
            table.insert(playerList, player.Name)
        end
    end
    return playerList
end

-- Função para atualizar o dropdown
local function updateDropdown(dropdown)
    UpdateDropdown(dropdown, getPlayerList())
end

-- Função para equipar o item "Couch"
local function equipCouch()
    print("Tentando equipar o sofá...")
    if backpack then
        local couchItem = backpack:FindFirstChild("Couch")
        if couchItem then
            couchItem.Parent = localPlayer.Character
            local humanoid = localPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                humanoid:EquipTool(couchItem)
                print("Sofá equipado.")
            else
                print("Humanoide não encontrado.")
            end
        else
            warn("Sofá não encontrado na mochila.")
        end
    else
        print("Mochila não encontrada.")
    end
end

-- Função para teleportar para a coordenada
local function teleportToCoordinate()
    print("Teleportando para a coordenada...")
    local teleportPosition = Vector3.new(198, 4, 234) -- Coordenada para onde você deseja teleportar
    localPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(teleportPosition)
end

-- Função para flingar jogador (V14)
local function flingV14(targetPlayerName)
    local targetPlayer = playerService:FindFirstChild(targetPlayerName)
    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        -- Looping de teleportes no jogador selecionado
        flingV14Connection = runService.Heartbeat:Connect(function()
            if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
                local targetPosition = targetPlayer.Character.HumanoidRootPart.CFrame
                      if toggle then
                    -- Teleportando uma unidade para cima
                    localPlayer.Character.HumanoidRootPart.CFrame = targetPosition * CFrame.new(0, 2, 0)
                else
                    -- Teleportando uma unidade para baixo
                    localPlayer.Character.HumanoidRootPart.CFrame = targetPosition * CFrame.new(0, -3, 0)
                    end
                toggle = not toggle
              end
              
            -- Verifica se o jogador sentou no 'SeatCouch' e realiza o teleporte para a coordenada
            if targetPlayer.Character:FindFirstChild("Humanoid") and targetPlayer.Character.Humanoid.SeatPart then
                teleportToCoordinate()
                flingV14Connection:Disconnect()
                flingV14Connection = nil
            end
        end)
    else
        print("Jogador alvo não encontrado ou inválido.")
    end
end

-- Função para detectar quando o jogador renasce
local function onPlayerRespawned(targetPlayer)
    if flingV14Toggle then
        -- Aguardar o renascimento do jogador
        playerSpawnedConnection = targetPlayer.CharacterAdded:Connect(function()
            wait(1) -- Tempo para garantir que o personagem foi totalmente carregado
            if flingV14Toggle then
                equipCouch() -- Equipar o sofá quando o jogador renasce
                flingV14(targetPlayer.Name)
            end
        end)
    end
end

-- Função para verificar e equipar o sofá caso não esteja equipado
local function ensureCouchEquipped()
    local character = localPlayer.Character
    if character then
        local equipped = false
        for _, tool in ipairs(character:GetChildren()) do
            if tool:IsA("Tool") and tool.Name == "Couch" then
                equipped = true
                break
            end
        end
        if not equipped then
            equipCouch()
        end
    else
        print("Personagem não encontrado.")
    end
end

-- Função para desativar as colisões do personagem
local function disableCollisions(character)
    if character and character:FindFirstChild("Head") and character:FindFirstChild("UpperTorso") and character:FindFirstChild("LowerTorso") and character:FindFirstChild("HumanoidRootPart") then
        character.Head.CanCollide = false
        character.UpperTorso.CanCollide = false
        character.LowerTorso.CanCollide = false
        character.HumanoidRootPart.CanCollide = false
    else
        print("Parte do personagem não encontrada.")
    end
end

-- Função para reativar as colisões do personagem
local function resetCollisions(character)
    if character and character:FindFirstChild("Head") and character:FindFirstChild("UpperTorso") and character:FindFirstChild("LowerTorso") and character:FindFirstChild("HumanoidRootPart") then
        character.Head.CanCollide = true
        character.UpperTorso.CanCollide = true
        character.LowerTorso.CanCollide = true
        character.HumanoidRootPart.CanCollide = true
    end
end

-- Função para ativar o Spin Fling
local function activateSpinFling()
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()
    local power = 500 -- Pode ajustar isso para alterar a força do impulso

    -- Cria um novo BodyThrust
    bodyThrust = Instance.new("BodyThrust")
    bodyThrust.Parent = character.HumanoidRootPart
    bodyThrust.Force = Vector3.new(power, 500, power)
    bodyThrust.Location = character.HumanoidRootPart.Position

    -- Desativa as colisões
    spinFlingConnection = runService.Stepped:Connect(function()
        disableCollisions(character)
    end)

    print("Spin Fling ativado!")
end

-- Função para desativar o Spin Fling
local function deactivateSpinFling()
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()

    -- Desconecta a função de desativação de colisões
    if spinFlingConnection then
        spinFlingConnection:Disconnect()
        spinFlingConnection = nil
    end

    -- Remove o efeito de impulso do corpo
    if bodyThrust then
        bodyThrust:Destroy()
        bodyThrust = nil
    end

    -- Restaura as colisões do personagem
    resetCollisions(character)

    print("Spin Fling desativado!")
end

-- Função de callback para o toggle
local function onFlingV14Toggle(value)
    print("Toggle Fling V14:", value)
    flingV14Toggle = value
    if flingV14Toggle and selectedFlingPlayerV14 then
        local targetPlayer = playerService:FindFirstChild(selectedFlingPlayerV14)
        if targetPlayer then
            ensureCouchEquipped() -- Equipar o sofá ao ativar o toggle
            flingV14(targetPlayer.Name)
            onPlayerRespawned(targetPlayer)
            activateSpinFling() -- Ativar o Spin Fling quando o toggle é ativado
        end
    elseif not flingV14Toggle then
        -- Desconecta as conexões quando o toggle é desativado
        if flingV14Connection then
            flingV14Connection:Disconnect()
            flingV14Connection = nil
        end
        if playerSpawnedConnection then
            playerSpawnedConnection:Disconnect()
            playerSpawnedConnection = nil
        end
        deactivateSpinFling() -- Desativar o Spin Fling quando o toggle é desativado
    end
end

-- Adiciona o dropdown para selecionar o jogador
local playerDropdownV14Toggle = AddDropdown(Main, {
    Name = "Selecione o Jogador para Fling [V16]",
    Default = "",
    Options = getPlayerList(),
    Callback = function(playerName)
        selectedFlingPlayerV14 = playerName
        print("Jogador selecionado para Fling V16:", playerName)
    end
})

-- Atualiza a lista de jogadores quando os jogadores entram ou saem do jogo
playerService.PlayerAdded:Connect(function()
    print("Novo jogador adicionado. Atualizando a lista...")
    updateDropdown(playerDropdownV14Toggle)
end)

playerService.PlayerRemoving:Connect(function()
    print("Jogador saiu. Atualizando a lista...")
    updateDropdown(playerDropdownV14Toggle)
end)

-- Atualiza a lista de jogadores ao iniciar o script
updateDropdown(playerDropdownV14Toggle)

-- Variável para armazenar o estado da proteção
local voidProtectionEnabled = false

-- Função para ativar a proteção contra o vazio
local function ActivateVoidProtection()
    voidProtectionEnabled = true
    -- Definindo FallenPartsDestroyHeight para NaN para prevenir a destruição
    game.Workspace.FallenPartsDestroyHeight = 0/0
end

-- Função para desativar a proteção contra o vazio
local function DeactivateVoidProtection()
    voidProtectionEnabled = false
    -- Definindo FallenPartsDestroyHeight para um valor que permite destruição
    game.Workspace.FallenPartsDestroyHeight = -9999999999999 -- Ajuste este valor conforme necessário
end

-- Adiciona o Toggle e define o callback para ativar/desativar a proteção contra o vazio e a função original
AddToggle(Main, {
    Name = "Fling [V16]",
    Default = false,
    Callback = function(value)
        -- Mantém a funcionalidade original do Toggle
        onFlingV14Toggle(value)

        -- Ativa ou desativa a proteção contra o vazio
        if value then
            ActivateVoidProtection()
            print("Void protection activated.")
        else
            DeactivateVoidProtection()
            print("Void protection deactivated.")
        end

        -- Imprime o estado atual do Toggle
        print("Toggle de Fling [V16] foi alterado para:", value)
    end
})

local section = AddSection(Main, {"View"})

-- Função para enviar notificações
function MakeNotifi(notification)
    game.StarterGui:SetCore("SendNotification", {
        Title = notification.Title;
        Text = notification.Text;
        Duration = notification.Time;
    })
end

-- Variáveis e funções para a visualização dos jogadores
local viewEnabled = false
local selectedViewPlayer = nil
local characterAddedConnection = nil

local function toggleView(enabled)
    if enabled then
        if selectedViewPlayer then
            local player = selectedViewPlayer
            if player then
                game.Workspace.CurrentCamera.CameraSubject = player.Character
                if characterAddedConnection then
                    characterAddedConnection:Disconnect()
                end
                characterAddedConnection = player.CharacterAdded:Connect(function(character)
                    game.Workspace.CurrentCamera.CameraSubject = character
                end)
                MakeNotifi({
                    Title = "Visualizando " .. player.Name,
                    Text = "Você está visualizando o jogador: " .. player.Name,
                    Time = 6
                })
            else
                print("Jogador não encontrado.")
                viewEnabled = false
            end
        else
            print("Nenhum jogador selecionado para a visualização.")
            viewEnabled = false
        end
    else
        if characterAddedConnection then
            characterAddedConnection:Disconnect()
            characterAddedConnection = nil
        end
        game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character
    end
end

local value = "" -- Variável para armazenar o nome digitado

local function findPlayerByPartialNameOrNickname(partialName)
    value = partialName -- Atualiza a variável com o nome digitado completo
    for _, player in ipairs(game.Players:GetPlayers()) do
        if player.Name:lower():find(partialName:lower(), 1, true) or (player.DisplayName and player.DisplayName:lower():find(partialName:lower(), 1, true)) then
            return player
        end
    end
    return nil
end

-- Adicionando a caixa de texto para entrada do nome ou apelido do jogador
AddTextBox(Main, {
    Name = "Digite o Nome ou Apelido do Jogador",
    Default = "",
    PlaceholderText = "Digite aqui para view",
    ClearText = true,
    Callback = function(value)
        if value == "" then
            MakeNotifi({
                Title = "Erro",
                Text = "Nome do jogador não foi digitado.",
                Time = 5
            })
            if viewEnabled then
                toggleView(false)
            end
            return
        end

        selectedViewPlayer = findPlayerByPartialNameOrNickname(value)
        if selectedViewPlayer then
            print("Jogador encontrado: " .. selectedViewPlayer.Name)
            if viewEnabled then
                toggleView(false)
                toggleView(true)
            end
        else
            MakeNotifi({
                Title = "Erro",
                Text = "Nenhum jogador encontrado com esse nome ou apelido.",
                Time = 7
            })
            if viewEnabled then
                toggleView(false)
            end
        end
    end
})

-- Adicionando o toggle para ativar/desativar a visualização
AddToggle(Main, {
    Name = "View",
    Default = false,
    Callback = function(enabled)
        viewEnabled = enabled
        toggleView(enabled)
    end
})

-- Conectando eventos de jogador 
game.Players.PlayerRemoving:Connect(function(player)
    if selectedViewPlayer == player then
        selectedViewPlayer = nil
        if viewEnabled then
            toggleView(false)
            MakeNotifi({
                Title = "Jogador Saiu",
                Text = player.Name .. " saiu do jogo. Visualização desativada.",
                Time = 5
            })
        end
    end
end)

-- Função para manter a câmera no jogador selecionado
local function maintainView()
    while wait() do
        if viewEnabled and selectedViewPlayer then
            local player = selectedViewPlayer
            if player and game.Workspace.CurrentCamera.CameraSubject ~= player.Character then
                game.Workspace.CurrentCamera.CameraSubject = player.Character
            end
        end
    end
end

-- Iniciando a função de manutenção da câmera
spawn(maintainView)

local section = AddSection(Main, {"Flings Spins | Avatar"})

AddButton(Main, {
  Name = "Ficar Super Pequeno",
     Callback = function()
        -- Cria os argumentos para diminuir o tamanho do personagem
        local args = {
            [1] = "CharacterSizeDown",
            [2] = 4
        }
        -- Envia um pedido ao servidor para diminuir o tamanho do personagem
        game:GetService("ReplicatedStorage").RE:FindFirstChild("1Clothe1s"):FireServer(unpack(args))
    end
})

-- Serviço necessário para manipular as atualizações de tempo
local runService = game:GetService('RunService')
-- Referência ao jogador local
local player = game.Players.LocalPlayer
-- Variáveis para a conexão e o efeito de impulso do corpo
local connection
local bodyThrust

-- Função para desativar as colisões do personagem
local function disableCollisions(character)
    if character and character:FindFirstChild("Head") and character:FindFirstChild("UpperTorso") and character:FindFirstChild("LowerTorso") and character:FindFirstChild("HumanoidRootPart") then
        character.Head.CanCollide = false
        character.UpperTorso.CanCollide = false
        character.LowerTorso.CanCollide = false
        character.HumanoidRootPart.CanCollide = false
    end
end

-- Função para reativar as colisões do personagem
local function resetCollisions(character)
    if character and character:FindFirstChild("Head") and character:FindFirstChild("UpperTorso") and character:FindFirstChild("LowerTorso") and character:FindFirstChild("HumanoidRootPart") then
        character.Head.CanCollide = true
        character.UpperTorso.CanCollide = true
        character.LowerTorso.CanCollide = true
        character.HumanoidRootPart.CanCollide = true
    end
end

-- Função chamada quando o personagem é adicionado
local function onCharacterAdded(character)
    -- Desconecta qualquer conexão 
