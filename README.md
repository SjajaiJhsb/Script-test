-- Criar a interface de usuário
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local Button = Instance.new("TextButton")

-- Configurar a interface de usuário
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.new(1, 1, 1)
Frame.Position = UDim2.new(0.5, -100, 0.5, -50)
Frame.Size = UDim2.new(0, 200, 0, 100)
Frame.Active = true
Frame.Draggable = true

Button.Parent = Frame
Button.BackgroundColor3 = Color3.new(0.5, 0.5, 0.5)
Button.Position = UDim2.new(0.25, 0, 0.25, 0)
Button.Size = UDim2.new(0.5, 0, 0.5, 0)
Button.Text = "Ativar Voo"

-- Variável para controlar o estado do voo
local vooAtivo = false

-- Função para ativar/desativar o voo
local function toggleVoo()
    vooAtivo = not vooAtivo
    if vooAtivo then
        Button.Text = "Desativar Voo"
        -- Código para ativar o voo
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
        humanoid.PlatformStand = true
        character.HumanoidRootPart.BodyVelocity = Instance.new("BodyVelocity", character.HumanoidRootPart)
        character.HumanoidRootPart.BodyVelocity.Velocity = Vector3.new(0, 50, 0)
    else
        Button.Text = "Ativar Voo"
        -- Código para desativar o voo
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoid = character:WaitForChild("Humanoid")
        humanoid.PlatformStand = false
        if character.HumanoidRootPart:FindFirstChild("BodyVelocity") then
            character.HumanoidRootPart.BodyVelocity:Destroy()
        end
    end
end

-- Conectar a função ao botão
Button.MouseButton1Click:Connect(toggleVoo)
