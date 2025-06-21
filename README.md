--[[
    🟦 Ultimate Shooter Mini UI + ESP (Android Premium) 🟦
    Uso educacional! Não use para prejudicar outros jogadores!
    Key de acesso: azul
    Logo: GitHub
    Interface arredondada
    Munição infinita corrigida (não buga dano)
]]

if game:GetService("RunService"):IsClient() then
    -- SISTEMA DE KEY (antes de tudo)
    local KEY = "azul"
    local accessGranted = false

    local Players = game:GetService("Players")
    local LocalPlayer = Players.LocalPlayer

    local keyGui = Instance.new("ScreenGui")
    keyGui.Name = "KeySystemUI"
    pcall(function() keyGui.Parent = game:GetService("CoreGui") end)
    if not keyGui.Parent then keyGui.Parent = LocalPlayer:WaitForChild("PlayerGui") end

    local keyFrame = Instance.new("Frame")
    keyFrame.Size = UDim2.new(0, 260, 0, 170)
    keyFrame.Position = UDim2.new(0.5, -130, 0.5, -85)
    keyFrame.BackgroundColor3 = Color3.fromRGB(27,29,35)
    keyFrame.BackgroundTransparency = 0.05
    keyFrame.BorderSizePixel = 0
    keyFrame.AnchorPoint = Vector2.new(0.5, 0.5)
    keyFrame.Parent = keyGui

    -- Deixa a interface arredondada
    local keyUICorner = Instance.new("UICorner")
    keyUICorner.CornerRadius = UDim.new(0, 24)
    keyUICorner.Parent = keyFrame

    -- GITHUB LOGO (acima da mensagem)
    local logo = Instance.new("ImageLabel")
    logo.BackgroundTransparency = 1
    logo.Size = UDim2.new(0,48,0,48)
    logo.Position = UDim2.new(0.5,-24,0,6)
    logo.Image = "rbxassetid://11293271856" -- GitHub Octocat
    logo.ZIndex = 2
    logo.Parent = keyFrame
    local logoCorner = Instance.new("UICorner")
    logoCorner.CornerRadius = UDim.new(1,0)
    logoCorner.Parent = logo

    -- Mensagem extra acima do título
    local infoMsg = Instance.new("TextLabel")
    infoMsg.Size = UDim2.new(1, 0, 0, 18)
    infoMsg.Position = UDim2.new(0, 0, 0, 54)
    infoMsg.BackgroundTransparency = 1
    infoMsg.Text = "Bem-vindo! Para acessar o menu, digite a key."
    infoMsg.TextColor3 = Color3.fromRGB(80,180,255)
    infoMsg.Font = Enum.Font.Gotham
    infoMsg.TextSize = 14
    infoMsg.Parent = keyFrame

    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, 0, 0, 32)
    title.BackgroundTransparency = 1
    title.Position = UDim2.new(0, 0, 0, 72)
    title.Text = "🔐 Digite a Key de Acesso"
    title.TextColor3 = Color3.fromRGB(80,180,255)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 17
    title.Parent = keyFrame

    local input = Instance.new("TextBox")
    input.Size = UDim2.new(0.85, 0, 0, 32)
    input.Position = UDim2.new(0.075, 0, 0, 108)
    input.PlaceholderText = "Digite a key aqui..."
    input.Text = ""
    input.BackgroundColor3 = Color3.fromRGB(44,44,55)
    input.TextColor3 = Color3.fromRGB(80,180,255)
    input.Font = Enum.Font.Gotham
    input.TextSize = 16
    input.BorderSizePixel = 0
    input.Parent = keyFrame
    local inputCorner = Instance.new("UICorner")
    inputCorner.CornerRadius = UDim.new(0,12)
    inputCorner.Parent = input

    local avisotxt = Instance.new("TextLabel")
    avisotxt.Size = UDim2.new(1, 0, 0, 18)
    avisotxt.Position = UDim2.new(0, 0, 1, -24)
    avisotxt.BackgroundTransparency = 1
    avisotxt.Text = ""
    avisotxt.TextColor3 = Color3.fromRGB(255,75,75)
    avisotxt.Font = Enum.Font.Gotham
    avisotxt.TextSize = 14
    avisotxt.Parent = keyFrame

    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.85, 0, 0, 28)
    btn.Position = UDim2.new(0.075, 0, 1, -36)
    btn.BackgroundColor3 = Color3.fromRGB(80,180,255)
    btn.Text = "Liberar"
    btn.Font = Enum.Font.GothamBold
    btn.TextColor3 = Color3.fromRGB(255,255,255)
    btn.TextSize = 16
    btn.BorderSizePixel = 0
    btn.Parent = keyFrame
    local btnCorner = Instance.new("UICorner")
    btnCorner.CornerRadius = UDim.new(0,10)
    btnCorner.Parent = btn

    btn.MouseButton1Click:Connect(function()
        if input.Text == KEY then
            accessGranted = true
            keyGui:Destroy()
        else
            avisotxt.Text = "Key inválida!"
            wait(1)
            avisotxt.Text = ""
        end
    end)

    -- Aguarda digitar a key correta antes de liberar o script
    while not accessGranted do
        wait()
    end

    -- CLIENT SCRIPT (StarterPlayerScripts) - começa aqui após key
    local DAMAGE = 250
    local Camera = workspace.CurrentCamera
    local UserInputService = game:GetService("UserInputService")
    local StarterGui = game:GetService("StarterGui")
    local RunService = game:GetService("RunService")

    -- Estado das opções
    local state = {
        Shooter = false,
        Aimbot = true,
        Wallbang = true,
        HitAlwaysOn = true,
        ESP = true,
        NeverMiss = true,
        Teleguiado = true,
        InfiniteHealth = true,
        InfiniteAmmo = true
    }

    -- Interface
    local gui = Instance.new("ScreenGui")
    gui.Name = "UltimateShooterMiniUI_ESP_Android_Premium"
    pcall(function() gui.Parent = game:GetService("CoreGui") end)
    if not gui.Parent then gui.Parent = LocalPlayer:WaitForChild("PlayerGui") end

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 270, 0, 320)
    frame.Position = UDim2.new(0, 15, 0.7, 0)
    frame.BackgroundColor3 = Color3.fromRGB(27,29,35)
    frame.BackgroundTransparency = 0.08
    frame.BorderSizePixel = 0
    frame.Active = true
    frame.Draggable = true
    frame.Parent = gui

    -- Frame arredondado
    local frameCorner = Instance.new("UICorner")
    frameCorner.CornerRadius = UDim.new(0, 24)
    frameCorner.Parent = frame

    -- GITHUB LOGO NA INTERFACE PRINCIPAL (acima do título)
    local logo2 = Instance.new("ImageLabel")
    logo2.BackgroundTransparency = 1
    logo2.Size = UDim2.new(0,44,0,44)
    logo2.Position = UDim2.new(0.5,-22,0,8)
    logo2.Image = "rbxassetid://11293271856" -- GitHub Octocat
    logo2.ZIndex = 2
    logo2.Parent = frame
    local logo2Corner = Instance.new("UICorner")
    logo2Corner.CornerRadius = UDim.new(1,0)
    logo2Corner.Parent = logo2

    local topBar = Instance.new("Frame")
    topBar.Size = UDim2.new(1, 0, 0, 28)
    topBar.Position = UDim2.new(0,0,0,52)
    topBar.BackgroundColor3 = Color3.fromRGB(34,139,230)
    topBar.BorderSizePixel = 0
    topBar.Parent = frame
    local topBarCorner = Instance.new("UICorner")
    topBarCorner.CornerRadius = UDim.new(0, 12)
    topBarCorner.Parent = topBar

    local title = Instance.new("TextLabel")
    title.Size = UDim2.new(1, -56, 1, 0)
    title.Position = UDim2.new(0, 58, 0, 0)
    title.BackgroundTransparency = 1
    title.Text = "Ultimate Shooter"
    title.TextColor3 = Color3.fromRGB(210,255,255)
    title.Font = Enum.Font.GothamBold
    title.TextSize = 16
    title.TextXAlignment = Enum.TextXAlignment.Left
    title.Parent = topBar

    local minBtn = Instance.new("TextButton")
    minBtn.Size = UDim2.new(0, 28, 0, 28)
    minBtn.Position = UDim2.new(1, -56, 0, 0)
    minBtn.BackgroundColor3 = Color3.fromRGB(25,25,35)
    minBtn.Text = "_"
    minBtn.Font = Enum.Font.GothamBold
    minBtn.TextColor3 = Color3.new(1,1,1)
    minBtn.TextSize = 17
    minBtn.BorderSizePixel = 0
    minBtn.Parent = topBar
    local minBtnCorner = Instance.new("UICorner")
    minBtnCorner.CornerRadius = UDim.new(0,8)
    minBtnCorner.Parent = minBtn

    local xBtn = Instance.new("TextButton")
    xBtn.Size = UDim2.new(0, 28, 0, 28)
    xBtn.Position = UDim2.new(1, -28, 0, 0)
    xBtn.BackgroundColor3 = Color3.fromRGB(220,35,35)
    xBtn.Text = "X"
    xBtn.Font = Enum.Font.GothamBold
    xBtn.TextColor3 = Color3.new(1,1,1)
    xBtn.TextSize = 15
    xBtn.BorderSizePixel = 0
    xBtn.Parent = topBar
    local xBtnCorner = Instance.new("UICorner")
    xBtnCorner.CornerRadius = UDim.new(0,8)
    xBtnCorner.Parent = xBtn

    local optFrame = Instance.new("Frame")
    optFrame.Size = UDim2.new(1, 0, 1, -80)
    optFrame.Position = UDim2.new(0,0,0,80)
    optFrame.BackgroundTransparency = 1
    optFrame.Parent = frame

    local listLayout = Instance.new("UIListLayout")
    listLayout.Parent = optFrame
    listLayout.SortOrder = Enum.SortOrder.LayoutOrder
    listLayout.Padding = UDim.new(0, 6)

    -- Cria switches dinâmicos
    local switches = {}
    local function makeSwitch(txt, key)
        local btn = Instance.new("TextButton")
        btn.Size = UDim2.new(1, -24, 0, 28)
        btn.Position = UDim2.new(0, 12, 0, 0)
        btn.BackgroundColor3 = state[key] and Color3.fromRGB(40,180,40) or Color3.fromRGB(220,40,40)
        btn.Text = txt .. (state[key] and " [ON]" or " [OFF]")
        btn.Font = Enum.Font.GothamBold
        btn.TextColor3 = Color3.new(1,1,1)
        btn.TextSize = 16
        btn.BorderSizePixel = 0
        btn.Parent = optFrame
        btn.AutoButtonColor = false
        local btnCorner = Instance.new("UICorner")
        btnCorner.CornerRadius = UDim.new(0,8)
        btnCorner.Parent = btn

        btn.MouseEnter:Connect(function() btn.BackgroundTransparency = 0.18 end)
        btn.MouseLeave:Connect(function() btn.BackgroundTransparency = 0 end)

        btn.MouseButton1Click:Connect(function()
            state[key] = not state[key]
            btn.Text = txt .. (state[key] and " [ON]" or " [OFF]")
            btn.BackgroundColor3 = state[key] and Color3.fromRGB(40,180,40) or Color3.fromRGB(220,40,40)
            if key == "ESP" then updateEsp() end
        end)
        switches[key] = btn
    end

    makeSwitch("Shooter", "Shooter")
    makeSwitch("Aimbot", "Aimbot")
    makeSwitch("Wallbang", "Wallbang")
    makeSwitch("HitAlwaysOn", "HitAlwaysOn")
    makeSwitch("ESP", "ESP")
    makeSwitch("NeverMiss", "NeverMiss")
    makeSwitch("Teleguiado", "Teleguiado")
    makeSwitch("Vida Infinita", "InfiniteHealth")
    makeSwitch("Munição Infinita", "InfiniteAmmo")

    -- Minimizar e fechar
    local minimized = false
    minBtn.MouseButton1Click:Connect(function()
        minimized = not minimized
        optFrame.Visible = not minimized
        frame.Size = minimized and UDim2.new(0,270,0,80) or UDim2.new(0,270,0,320)
    end)
    xBtn.MouseButton1Click:Connect(function()
        gui:Destroy()
        clearEsp()
    end)

    -- Ativa tudo após respawn
    local function autoEnable()
        for k,_ in pairs(state) do
            state[k] = true
            if switches[k] then
                switches[k].Text = switches[k].Text:gsub("%[.-%]", "[ON]")
                switches[k].BackgroundColor3 = Color3.fromRGB(40,180,40)
            end
        end
        updateEsp()
    end

    local function charListen()
        if LocalPlayer.Character then
            local hum = LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if hum then
                hum.Died:Connect(function()
                    wait(2.5)
                    autoEnable()
                    StarterGui:SetCore("SendNotification", {
                        Title = "Ultimate Shooter",
                        Text = "Opções reativadas após respawn!",
                        Duration = 2
                    })
                end)
            end
        end
    end
    LocalPlayer.CharacterAdded:Connect(charListen)
    if LocalPlayer.Character then charListen() end

    -- Vida infinita
    RunService.RenderStepped:Connect(function()
        if state.InfiniteHealth and LocalPlayer.Character and LocalPlayer.Character:FindFirstChild("Humanoid") then
            local hum = LocalPlayer.Character:FindFirstChild("Humanoid")
            if hum.Health < hum.MaxHealth then hum.Health = hum.MaxHealth end
        end
    end)

    -- MUNIÇÃO INFINITA (corrigida para não bugar o dano)
    local function setAmmo(inst)
        for _,v in ipairs(inst:GetDescendants()) do
            if (v:IsA("IntValue") or v:IsA("NumberValue")) and (v.Name:lower():find("ammo") or v.Name:lower():find("muni")) then
                -- Apenas recarrega quando acabar/ammo baixa, mantém valor razoável
                if v.Value < 5 then
                    v.Value = 30 -- ou o valor padrão da arma!
                end
            end
        end
    end
    RunService.RenderStepped:Connect(function()
        if state.InfiniteAmmo then
            if LocalPlayer.Backpack then
                for _,tool in ipairs(LocalPlayer.Backpack:GetChildren()) do
                    if tool:IsA("Tool") then setAmmo(tool) end
                end
            end
            if LocalPlayer.Character then
                for _,tool in ipairs(LocalPlayer.Character:GetChildren()) do
                    if tool:IsA("Tool") then setAmmo(tool) end
                end
            end
        end
    end)

    -- Funções utilitárias para inimigos
    local function getClosestEnemyPart(partName)
        local closest, minDist = nil, math.huge
        for _,plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild(partName) then
                local humanoid = plr.Character:FindFirstChild("Humanoid")
                if humanoid and humanoid.Health > 0 then
                    local dist = (LocalPlayer.Character.Head.Position - plr.Character[partName].Position).Magnitude
                    if dist < minDist then
                        minDist, closest = dist, plr.Character[partName]
                    end
                end
            end
        end
        return closest
    end

    local function getClosestEnemyHumanoid()
        local closest, minDist = nil, math.huge
        for _,plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local humanoid = plr.Character:FindFirstChild("Humanoid")
                if humanoid and humanoid.Health > 0 then
                    local dist = (LocalPlayer.Character.Head.Position - plr.Character.HumanoidRootPart.Position).Magnitude
                    if dist < minDist then
                        minDist, closest = dist, humanoid
                    end
                end
            end
        end
        return closest
    end

    local function getHumanoidNearPoint(point, radius)
        local closest, minDist = nil, radius
        for _,plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local humanoid = plr.Character:FindFirstChild("Humanoid")
                if humanoid and humanoid.Health > 0 then
                    local dist = (point - plr.Character.HumanoidRootPart.Position).Magnitude
                    if dist < minDist then
                        minDist, closest = dist, humanoid
                    end
                end
            end
        end
        return closest
    end

    -- Tiro teleguiado e atirar (touch e mouse)
    local function getTeleguiadoPoint(origin)
        local humanoid = getClosestEnemyHumanoid()
        if humanoid and humanoid.Parent and humanoid.Parent:FindFirstChild("HumanoidRootPart") then
            return humanoid.Parent.HumanoidRootPart.Position
        end
        return nil
    end

    local function shootByTouch(touchPos)
        if not state.Shooter then return end
        if not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("Head") then return end
        local origin = LocalPlayer.Character.Head.Position
        local targetPos

        if state.Teleguiado then
            local target = getTeleguiadoPoint(origin)
            if target then targetPos = target end
        elseif state.NeverMiss then
            local head = getClosestEnemyPart("Head")
            if head then targetPos = head.Position end
        elseif state.Aimbot then
            local head = getClosestEnemyPart("Head")
            if head then targetPos = head.Position end
        end

        if not targetPos then
            local ray = Camera:ViewportPointToRay(touchPos.X, touchPos.Y)
            local aimPoint = ray and (ray.Origin + ray.Direction * 500)
            if state.HitAlwaysOn then
                local humanoid = getHumanoidNearPoint(aimPoint, 13)
                if humanoid and humanoid.Parent and humanoid.Parent:FindFirstChild("Head") then
                    targetPos = humanoid.Parent.Head.Position
                else
                    targetPos = aimPoint
                end
            else
                targetPos = aimPoint
            end
        end

        local direction = (targetPos - origin).Unit * 2000
        local rayParams = RaycastParams.new()
        rayParams.FilterDescendantsInstances = {LocalPlayer.Character}
        rayParams.FilterType = Enum.RaycastFilterType.Blacklist
        rayParams.IgnoreWater = true

        local result = workspace:Raycast(origin, direction, rayParams)
        local hitPos = result and result.Position or (origin + direction)
        local humanoidHit = nil
        if state.HitAlwaysOn or state.Wallbang or state.NeverMiss or state.Teleguiado then
            humanoidHit = getHumanoidNearPoint(hitPos, 13)
        end
        if not humanoidHit and result and result.Instance then
            local humanoid = result.Instance.Parent:FindFirstChild("Humanoid") or (result.Instance.Parent.Parent and result.Instance.Parent.Parent:FindFirstChild("Humanoid"))
            humanoidHit = humanoid
        end
        if not humanoidHit then
            humanoidHit = getHumanoidNearPoint(hitPos, 13)
        end

        if humanoidHit and humanoidHit ~= LocalPlayer.Character:FindFirstChild("Humanoid") and humanoidHit.Health > 0 then
            humanoidHit.Health = math.max(humanoidHit.Health - DAMAGE, 0)
        end
    end

    -- Touch e Mouse
    UserInputService.TouchTap:Connect(function(touchPositions, processed)
        if processed or not state.Shooter then return end
        if #touchPositions > 0 then
            shootByTouch(Vector2.new(touchPositions[1].X, touchPositions[1].Y))
        end
    end)
    UserInputService.InputBegan:Connect(function(input, processed)
        if processed or not state.Shooter then return end
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            local mousePos = UserInputService:GetMouseLocation()
            shootByTouch(Vector2.new(mousePos.X, mousePos.Y))
        end
    end)

    -- ESP (aprimorado)
    local espBoxes = {}
    function clearEsp()
        for _,v in pairs(espBoxes) do
            if v and v.Adornee then v:Destroy() end
        end
        espBoxes = {}
    end

    function updateEsp()
        clearEsp()
        if not state.ESP then return end
        for _,plr in ipairs(Players:GetPlayers()) do
            if plr ~= LocalPlayer and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
                local human = plr.Character:FindFirstChild("Humanoid")
                if human and human.Health > 0 then
                    local box = Instance.new("BoxHandleAdornment")
                    box.Adornee = plr.Character.HumanoidRootPart
                    box.Size = plr.Character:GetExtentsSize() + Vector3.new(0.5,0.5,0.5)
                    box.Color3 = Color3.fromRGB(0,255,0)
                    box.Transparency = 0.65
                    box.ZIndex = 10
                    box.AlwaysOnTop = true
                    box.Parent = gui
                    espBoxes[#espBoxes+1] = box
                end
            end
        end
    end

    Players.PlayerAdded:Connect(function() if state.ESP then wait(0.5) updateEsp() end end)
    Players.PlayerRemoving:Connect(function() if state.ESP then wait(0.5) updateEsp() end end)
    LocalPlayer.CharacterAdded:Connect(function() wait(1) if state.ESP then updateEsp() end end)
    RunService.RenderStepped:Connect(function()
        if state.ESP then updateEsp() end
    end)

    autoEnable()
    updateEsp()
end

-- SERVER SCRIPT (ServerScriptService, reforçado)
if game:GetService("RunService"):IsServer() then
    local Players = game:GetService("Players")
    Players.PlayerAdded:Connect(function(player)
        player.CharacterAdded:Connect(function(character)
            local humanoid = character:WaitForChild("Humanoid")
            humanoid:GetPropertyChangedSignal("Health"):Connect(function()
                if humanoid.Health > humanoid.MaxHealth then
                    humanoid.Health = humanoid.MaxHealth
                    warn("[Server] Tentativa de cheat bloqueada para "..player.Name)
                end
                if humanoid.Health < 0 then
                    humanoid.Health = 0
                end
            end)
        end)
    end)
end
