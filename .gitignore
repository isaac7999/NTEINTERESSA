local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character or LocalPlayer.CharacterAdded:Wait()
local RootPart = Character:WaitForChild("HumanoidRootPart")
local TweenService = game:GetService("TweenService")

local ativado = false -- Estado inicial desligado

-- Criar GUI do botão
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
local Botao = Instance.new("TextButton")
Botao.Parent = ScreenGui
Botao.Size = UDim2.new(0, 150, 0, 50)
Botao.Position = UDim2.new(0, 50, 0, 50)
Botao.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Botao.TextColor3 = Color3.fromRGB(255, 255, 255)
Botao.Text = "Ativar Script"
Botao.Font = Enum.Font.SourceSansBold
Botao.TextSize = 20

-- Criar a notificação
local notification = Instance.new("TextLabel")
notification.Parent = ScreenGui
notification.Size = UDim2.new(0, 400, 0, 50)
notification.Position = UDim2.new(0.5, -200, 0, 100) -- Posição no centro da tela
notification.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
notification.BackgroundTransparency = 0.5
notification.TextColor3 = Color3.fromRGB(255, 255, 255)
notification.Text = "BY AMONG US"
notification.Font = Enum.Font.SourceSansBold
notification.TextSize = 30
notification.Visible = false -- Começa invisível

-- Função para teleportar
local function teleportTo(x, y, z, delayTime)
    if RootPart then
        RootPart.CFrame = CFrame.new(x, y, z)
        task.wait(delayTime or 0.1) -- Tempo de espera opcional, padrão mais rápido
    end
end

-- Função para ativar o ProximityPrompt
local function activateProximityPrompt()
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("ProximityPrompt") then
            local promptPart = obj.Parent
            if promptPart and (RootPart.Position - promptPart.Position).Magnitude < obj.MaxActivationDistance then
                fireproximityprompt(obj)
                return true
            end
        end
    end
    return false
end

-- Função para encontrar e teleportar para o botão mais próximo
local function teleportToClosestButton()
    local closestButton = nil
    local shortestDistance = math.huge

    -- Iterar por todos os ProximityPrompts (botões)
    for _, obj in ipairs(workspace:GetDescendants()) do
        if obj:IsA("ProximityPrompt") then
            local promptPart = obj.Parent
            if promptPart then
                local distance = (RootPart.Position - promptPart.Position).Magnitude
                if distance < shortestDistance then
                    shortestDistance = distance
                    closestButton = promptPart
                end
            end
        end
    end

    -- Teleportar para o botão mais próximo, se encontrado
    if closestButton then
        teleportTo(closestButton.Position.X, closestButton.Position.Y, closestButton.Position.Z, 0.2)
        return true
    end
    return false
end

-- Função para exibir a notificação com animação
local function showNotification()
    notification.Visible = true
    local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out)
    local goal = {Position = UDim2.new(0.5, -200, 0, 150)} -- Alvo da animação (para aparecer na tela)
    local tween = TweenService:Create(notification, tweenInfo, goal)
    tween:Play()

    -- Ficar visível por 2 segundos e depois desaparecer
    task.wait(2)
    local hideGoal = {Position = UDim2.new(0.5, -200, 0, 100)} -- Posição inicial para esconder
    local hideTween = TweenService:Create(notification, tweenInfo, hideGoal)
    hideTween:Play()

    task.wait(1) -- Espera a animação de esconder terminar
    notification.Visible = false
end

-- Alternar estado do script
Botao.MouseButton1Click:Connect(function()
    ativado = not ativado
    Botao.Text = ativado and "Desativar Script" or "Ativar Script"

    if ativado then
        showNotification()  -- Exibe a notificação quando o script é ativado

        while ativado do
            -- Coordenadas fornecidas
            local coordenadas = {
                {x = -551.8, y = 1.8, z = 9.5},
                {x = -555.1, y = 2.0, z = 9.7},
                {x = -616.4, y = 1.8, z = 13.7},
                {x = -616.4, y = 2.2, z = 9.6},
                {x = -550.6, y = 1.9, z = 41.0},
                {x = -546.6, y = 1.9, z = 40.5},
                {x = -500.4, y = 1.8, z = 10.3},
                {x = -494.5, y = 1.4, z = 10.5},
                {x = -485.4, y = 2.0, z = 35.5},
                {x = -486.2, y = 1.7, z = 40.4},
                {x = -489.6, y = 3.1, z = 42.0},
                {x = -494.9, y = 2.0, z = 41.0},
                {x = -529.7, y = 4.8, z = 40.1},
                {x = -584.7, y = 3.1, z = 2.9},
                {x = -454.4, y = 2.8, z = -7.5},
                {x = -454.0, y = 2.5, z = -3.5},
                {x = -454.7, y = 2.0, z = -36.8},
                {x = -454.8, y = 2.0, z = -41.3},
                {x = -377.9, y = 2.5, z = -26.0},
                {x = -377.8, y = 2.1, z = -31.8}
            }

            -- Iterar pelas coordenadas e coletar
            for _, coord in ipairs(coordenadas) do
                teleportTo(coord.x, coord.y, coord.z, 0.1) -- Teleporta rapidamente
                activateProximityPrompt() -- Coleta o item

                task.wait(0.2) -- Atraso pequeno antes de mover para a próxima coordenada
            end

            -- Teleportar para o botão mais próximo
            teleportToClosestButton()

            task.wait(0.8) -- Espera antes de repetir o processo
        end
    end
end)
