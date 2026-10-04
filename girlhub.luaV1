--[[ GIRL HUB TP V1 — com cerejas caindo 🍒 ]]--

local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local HttpService = game:GetService("HttpService")
local Stats = game:GetService("Stats")
local CoreGui = game:GetService("CoreGui")
local LP = Players.LocalPlayer

local SAVE_FILE = "girlhub_tp.json"
local TPCoords = nil
local SpeedValue = 16
local TPTime = 5

local function loadSave()
    if not (writefile and readfile and isfile) then return end
    if isfile(SAVE_FILE) then
        local ok, data = pcall(function() return HttpService:JSONDecode(readfile(SAVE_FILE)) end)
        if ok and data then
            TPCoords = data.tp
            SpeedValue = data.speed or 16
            TPTime = data.tptime or 5
        end
    end
end

local function saveData()
    if not writefile then return end
    pcall(function()
        writefile(SAVE_FILE, HttpService:JSONEncode({tp=TPCoords,speed=SpeedValue,tptime=TPTime}))
    end)
end

loadSave()

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "GirlHubTP"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.Parent = (gethui and gethui()) or CoreGui

-- HUD
local HUD = Instance.new("Frame")
HUD.Size = UDim2.new(0, 200, 0, 26)
HUD.Position = UDim2.new(0.5, -100, 0, 8)
HUD.BackgroundColor3 = Color3.fromRGB(255, 200, 225)
HUD.BackgroundTransparency = 0.15
HUD.BorderSizePixel = 0
HUD.Parent = ScreenGui
local HUDCorner = Instance.new("UICorner")
HUDCorner.CornerRadius = UDim.new(1, 0)
HUDCorner.Parent = HUD
local HUDStroke = Instance.new("UIStroke")
HUDStroke.Color = Color3.fromRGB(255, 120, 180)
HUDStroke.Thickness = 1.5
HUDStroke.Parent = HUD
local HUDText = Instance.new("TextLabel")
HUDText.Size = UDim2.new(1, 0, 1, 0)
HUDText.BackgroundTransparency = 1
HUDText.Text = "ping: -- ms  |  fps: --"
HUDText.TextColor3 = Color3.fromRGB(255, 255, 255)
HUDText.TextSize = 12
HUDText.Font = Enum.Font.GothamBold
HUDText.TextStrokeTransparency = 0
HUDText.TextStrokeColor3 = Color3.fromRGB(200, 80, 140)
HUDText.Parent = HUD

local fps = 0
local frameCount = 0
local lastTime = tick()
RunService.RenderStepped:Connect(function()
    frameCount = frameCount + 1
    local now = tick()
    if now - lastTime >= 1 then
        fps = frameCount
        frameCount = 0
        lastTime = now
    end
end)

task.spawn(function()
    while true do
        local ping = 0
        pcall(function()
            ping = math.floor(Stats.Network.ServerStatsItem["Data Ping"]:GetValue())
        end)
        HUDText.Text = "ping: " .. ping .. " ms  |  fps: " .. fps
        task.wait(0.5)
    end
end)

-- BOLINHA
local Toggle = Instance.new("TextButton")
Toggle.Size = UDim2.new(0, 40, 0, 40)
Toggle.Position = UDim2.new(0, 20, 0, 200)
Toggle.BackgroundColor3 = Color3.fromRGB(255, 182, 213)
Toggle.BorderSizePixel = 0
Toggle.Text = "🍒"
Toggle.TextSize = 22
Toggle.Font = Enum.Font.GothamBold
Toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
Toggle.AutoButtonColor = false
Toggle.Active = true
Toggle.Parent = ScreenGui
local ToggleCorner = Instance.new("UICorner")
ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = Toggle
local ToggleStroke = Instance.new("UIStroke")
ToggleStroke.Color = Color3.fromRGB(255, 120, 180)
ToggleStroke.Thickness = 2
ToggleStroke.Parent = Toggle

local tDragging, tDragInput, tDragStart, tStartPos = false, nil, nil, nil
Toggle.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        tDragging = true
        tDragStart = input.Position
        tStartPos = Toggle.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then tDragging = false end
        end)
    end
end)
Toggle.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        tDragInput = input
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if input == tDragInput and tDragging then
        local delta = input.Position - tDragStart
        Toggle.Position = UDim2.new(tStartPos.X.Scale, tStartPos.X.Offset + delta.X, tStartPos.Y.Scale, tStartPos.Y.Offset + delta.Y)
    end
end)

-- MENU
local Menu = Instance.new("Frame")
Menu.Size = UDim2.new(0, 250, 0, 340)
Menu.Position = UDim2.new(0.5, -125, 0.5, -170)
Menu.BackgroundColor3 = Color3.fromRGB(255, 200, 225)
Menu.BorderSizePixel = 0
Menu.Visible = true
Menu.Active = true
Menu.ClipsDescendants = true
Menu.Parent = ScreenGui
local MenuCorner = Instance.new("UICorner")
MenuCorner.CornerRadius = UDim.new(0, 12)
MenuCorner.Parent = Menu
local MenuStroke = Instance.new("UIStroke")
MenuStroke.Color = Color3.fromRGB(255, 120, 180)
MenuStroke.Thickness = 2
MenuStroke.Parent = Menu

-- ===== CEREJAS CAINDO DENTRO DO MENU =====
local cherryLayer = Instance.new("Frame")
cherryLayer.Name = "CherryLayer"
cherryLayer.Size = UDim2.new(1, 0, 1, 0)
cherryLayer.BackgroundTransparency = 1
cherryLayer.ClipsDescendants = true
cherryLayer.ZIndex = 0
cherryLayer.Parent = Menu

local cherryLabel = Instance.new("TextLabel")
cherryLabel.Size = UDim2.new(1, 0, 1, 0)
cherryLabel.BackgroundTransparency = 1
cherryLabel.Text = ""
cherryLabel.ZIndex = 0
cherryLabel.Parent = cherryLayer

-- função que cria uma cereja caindo
local function spawnCherry()
    local c = Instance.new("TextLabel")
    c.Size = UDim2.new(0, 20, 0, 20)
    c.BackgroundTransparency = 1
    c.Text = "🍒"
    c.TextSize = math.random(14, 22)
    c.Font = Enum.Font.GothamBold
    c.TextColor3 = Color3.fromRGB(255, 255, 255)
    c.ZIndex = 0
    c.Position = UDim2.new(math.random(0, 100) / 100, 0, 0, -30)
    c.Rotation = math.random(-30, 30)
    c.Parent = cherryLayer

    local duration = math.random(25, 50) / 10
    local targetPos = UDim2.new(c.Position.X.Scale, 0, 1, 30)
    local targetRot = c.Rotation + math.random(-180, 180)

    local tween = TweenService:Create(
        c,
        TweenInfo.new(duration, Enum.EasingStyle.Linear),
        {Position = targetPos, Rotation = targetRot}
    )
    tween:Play()

    tween.Completed:Connect(function()
        c:Destroy()
    end)
end

-- loop que gera cerejas a cada 0.4s
task.spawn(function()
    while true do
        if Menu.Visible then
            spawnCherry()
        end
        task.wait(0.4)
    end
end)

-- arrasto do menu
local mDragging, mDragInput, mDragStart, mStartPos = false, nil, nil, nil
Menu.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        mDragging = true
        mDragStart = input.Position
        mStartPos = Menu.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then mDragging = false end
        end)
    end
end)
Menu.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        mDragInput = input
    end
end)
UserInputService.InputChanged:Connect(function(input)
    if input == mDragInput and mDragging then
        local delta = input.Position - mDragStart
        Menu.Position = UDim2.new(mStartPos.X.Scale, mStartPos.X.Offset + delta.X, mStartPos.Y.Scale, mStartPos.Y.Offset + delta.Y)
    end
end)

-- HEADER (sempre visível)
local Header = Instance.new("TextLabel")
Header.Size = UDim2.new(1, 0, 0, 28)
Header.Position = UDim2.new(0, 0, 0, 8)
Header.BackgroundTransparency = 1
Header.Text = "girl hub tp V1"
Header.TextColor3 = Color3.fromRGB(255, 255, 255)
Header.TextSize = 18
Header.Font = Enum.Font.GothamBold
Header.TextStrokeTransparency = 0
Header.TextStrokeColor3 = Color3.fromRGB(200, 80, 140)
Header.ZIndex = 2
Header.Parent = Menu

local Sub = Instance.new("TextLabel")
Sub.Size = UDim2.new(1, 0, 0, 14)
Sub.Position = UDim2.new(0, 0, 0, 34)
Sub.BackgroundTransparency = 1
Sub.Text = ""
Sub.TextColor3 = Color3.fromRGB(255, 255, 255)
Sub.TextSize = 11
Sub.Font = Enum.Font.Gotham
Sub.ZIndex = 2
Sub.Parent = Menu

local LoadBarBG = Instance.new("Frame")
LoadBarBG.Size = UDim2.new(0, 180, 0, 8)
LoadBarBG.Position = UDim2.new(0.5, -90, 0, 54)
LoadBarBG.BackgroundColor3 = Color3.fromRGB(255, 170, 200)
LoadBarBG.BorderSizePixel = 0
LoadBarBG.ZIndex = 2
LoadBarBG.Parent = Menu
local LBG = Instance.new("UICorner")
LBG.CornerRadius = UDim.new(1, 0)
LBG.Parent = LoadBarBG
local LoadBar = Instance.new("Frame")
LoadBar.Size = UDim2.new(0, 0, 1, 0)
LoadBar.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
LoadBar.BorderSizePixel = 0
LoadBar.ZIndex = 3
LoadBar.Parent = LoadBarBG
local LBC = Instance.new("UICorner")
LBC.CornerRadius = UDim.new(1, 0)
LBC.Parent = LoadBar

local Discord = Instance.new("TextLabel")
Discord.Size = UDim2.new(1, 0, 0, 14)
Discord.Position = UDim2.new(0, 0, 0, 70)
Discord.BackgroundTransparency = 1
Discord.Text = ""
Discord.TextColor3 = Color3.fromRGB(255, 255, 255)
Discord.TextSize = 11
Discord.Font = Enum.Font.GothamBold
Discord.ZIndex = 2
Discord.Parent = Menu

local Fsociety = Instance.new("TextLabel")
Fsociety.Size = UDim2.new(1, 0, 0, 14)
Fsociety.Position = UDim2.new(0, 0, 0, 86)
Fsociety.BackgroundTransparency = 1
Fsociety.Text = ""
Fsociety.TextColor3 = Color3.fromRGB(255, 255, 255)
Fsociety.TextSize = 11
Fsociety.Font = Enum.Font.GothamBold
Fsociety.ZIndex = 2
Fsociety.Parent = Menu

local function typeText(label, text, delay)
    task.spawn(function()
        label.Text = ""
        for i = 1, #text do
            label.Text = string.sub(text, 1, i)
            task.wait(delay or 0.05)
        end
    end)
end

local function playIntro()
    Discord.Text = ""
    Fsociety.Text = ""
    Sub.Text = ""
    LoadBar.Size = UDim2.new(0, 0, 1, 0)
    Header.Text = "girl hub tp V1"

    typeText(Discord, "discord.gg/XMuM4azCh", 0.03)
    task.wait(#"discord.gg/XMuM4azCh" * 0.03 + 0.1)
    typeText(Sub, "carregando...", 0.03)
    TweenService:Create(LoadBar, TweenInfo.new(1.2, Enum.EasingStyle.Quad), {Size = UDim2.new(1, 0, 1, 0)}):Play()
    task.wait(1.3)
    Fsociety.Text = "fsociety"
    task.wait(0.6)

    local fadeTargets = {Sub, Discord, Fsociety, LoadBarBG}
    local tweens = {}
    for _, obj in ipairs(fadeTargets) do
        table.insert(tweens, TweenService:Create(obj, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 1, BackgroundTransparency = 1, TextStrokeTransparency = 1}))
    end
    table.insert(tweens, TweenService:Create(LoadBar, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 1}))
    for _, t in ipairs(tweens) do t:Play() end
    task.wait(0.6)

    Sub.Visible = false
    Discord.Visible = false
    Fsociety.Visible = false
    LoadBarBG.Visible = false
    LoadBar.Visible = false

    local shift = -95
    for _, obj in ipairs(Menu:GetChildren()) do
        if obj ~= cherryLayer and (obj:IsA("TextButton") or obj:IsA("TextBox") or (obj:IsA("TextLabel") and obj ~= Header and obj ~= Sub and obj ~= Discord and obj ~= Fsociety)) then
            obj.Position = UDim2.new(obj.Position.X.Scale, obj.Position.X.Offset, 0, obj.Position.Y.Offset + shift)
        end
    end
    TweenService:Create(Menu, TweenInfo.new(0.4, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {Size = UDim2.new(0, 250, 0, 260)}):Play()
end

local function makeButton(text, xPos, yPos, w, callback)
    local Btn = Instance.new("TextButton")
    Btn.Size = UDim2.new(0, w, 0, 30)
    Btn.Position = UDim2.new(0.5, xPos, 0, yPos)
    Btn.BackgroundColor3 = Color3.fromRGB(255, 170, 200)
    Btn.BorderSizePixel = 0
    Btn.Text = text
    Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    Btn.TextSize = 12
    Btn.Font = Enum.Font.GothamBold
    Btn.AutoButtonColor = true
    Btn.ZIndex = 2
    Btn.Parent = Menu
    local C = Instance.new("UICorner")
    C.CornerRadius = UDim.new(0, 8)
    C.Parent = Btn
    Btn.MouseButton1Click:Connect(callback)
    return Btn
end

local function createMarker(pos)
    local old = workspace:FindFirstChild("GirlHubMarker")
    if old then old:Destroy() end
    local part = Instance.new("Part")
    part.Name = "GirlHubMarker"
    part.Size = Vector3.new(2, 2, 2)
    part.Position = pos
    part.Anchored = true
    part.CanCollide = false
    part.Material = Enum.Material.Neon
    part.Color = Color3.fromRGB(255, 105, 180)
    part.Transparency = 0.3
    part.Parent = workspace
    local billboard = Instance.new("BillboardGui")
    billboard.Size = UDim2.new(0, 180, 0, 26)
    billboard.StudsOffset = Vector3.new(0, 2.5, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = part
    local lbl = Instance.new("TextLabel")
    lbl.Size = UDim2.new(1, 0, 1, 0)
    lbl.BackgroundTransparency = 1
    lbl.Text = "girl hub tp marcado!"
    lbl.TextColor3 = Color3.fromRGB(255, 105, 180)
    lbl.TextStrokeTransparency = 0
    lbl.TextStrokeColor3 = Color3.fromRGB(255, 255, 255)
    lbl.TextSize = 14
    lbl.Font = Enum.Font.GothamBold
    lbl.Parent = billboard
    task.spawn(function()
        while part.Parent do
            part.CFrame = part.CFrame * CFrame.Angles(0, math.rad(2), 0)
            RunService.Heartbeat:Wait()
        end
    end)
end

local function markLocation()
    local char = LP.Character
    if not char then Sub.Text = "sem personagem"; return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then Sub.Text = "aguarde"; return end
    TPCoords = hrp.Position
    createMarker(TPCoords)
    saveData()
    Sub.Visible = true
    Sub.Text = "marcado: " .. math.floor(TPCoords.X) .. ", " .. math.floor(TPCoords.Y) .. ", " .. math.floor(TPCoords.Z)
    task.delay(3, function() Sub.Text = "" end)
end

local function doTeleport()
    if not TPCoords then Sub.Text = "marque um local"; return end
    local char = LP.Character
    if not char then return end
    local hrp = char:FindFirstChild("HumanoidRootPart")
    if not hrp then return end
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not hum then return end

    local duration = 1 / math.max(TPTime, 0.01)
    local goalPos = TPCoords + Vector3.new(0, 3, 0)

    local parts = {}
    for _, d in ipairs(char:GetDescendants()) do
        if d:IsA("BasePart") or d:IsA("Decal") or d:IsA("Texture") then
            table.insert(parts, {part = d, oldTrans = d.Transparency})
        end
    end

    -- 1) PULO
    hum.Jump = true
    task.wait(0.25)

    -- 2) SOBE 6 STUDS
    local upCF = hrp.CFrame + Vector3.new(0, 6, 0)
    TweenService:Create(hrp, TweenInfo.new(0.25, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {CFrame = upCF}):Play()
    task.wait(0.3)
    hum.PlatformStand = true

    -- 3) SOME
    for _, info in ipairs(parts) do
        if info.part and info.part.Parent then
            TweenService:Create(info.part, TweenInfo.new(0.2), {Transparency = 1}):Play()
        end
    end
    task.wait(0.25)

    -- 4) FANTASMA ROSA VOA
    local ghost = hrp:Clone()
    ghost.Name = "GirlHubGhost"
    ghost.Anchored = true
    ghost.CanCollide = false
    ghost.CFrame = upCF
    ghost.Parent = workspace
    for _, d in ipairs(ghost:GetDescendants()) do
        if d:IsA("BasePart") then
            d.Anchored = true
            d.CanCollide = false
            d.Material = Enum.Material.Neon
            d.Color = Color3.fromRGB(255, 105, 180)
            d.Transparency = 0.3
            if d:IsA("MeshPart") then d.TextureID = "" end
        elseif d:IsA("Decal") or d:IsA("Texture") then
            d.Transparency = 1
        end
    end

    TweenService:Create(ghost, TweenInfo.new(duration, Enum.EasingStyle.Linear), {CFrame = CFrame.new(goalPos)}):Play()
    task.wait(duration + 0.05)

    -- 5) BONECO TELEPORTA E APARECE
    hrp.CFrame = CFrame.new(goalPos)
    hrp.AssemblyLinearVelocity = Vector3.zero
    hum.PlatformStand = false

    for _, info in ipairs(parts) do
        if info.part and info.part.Parent then
            TweenService:Create(info.part, TweenInfo.new(0.3), {Transparency = info.oldTrans or 0}):Play()
        end
    end

    -- 6) FANTASMA SOME
    for _, d in ipairs(ghost:GetDescendants()) do
        if d:IsA("BasePart") then
            TweenService:Create(d, TweenInfo.new(0.35), {Transparency = 1}):Play()
        end
    end
    task.delay(0.5, function() if ghost and ghost.Parent then ghost:Destroy() end end)
end

local function setSpeed(v)
    SpeedValue = v
    saveData()
    local char = LP.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then hum.WalkSpeed = v end
    end
end

makeButton("marcar local", -100, 110, 200, markLocation)
makeButton("ir pro tp", -100, 146, 200, doTeleport)

-- VELOCIDADE DO TP
local TPLabel = Instance.new("TextLabel")
TPLabel.Size = UDim2.new(1, 0, 0, 14)
TPLabel.Position = UDim2.new(0, 0, 0, 182)
TPLabel.BackgroundTransparency = 1
TPLabel.Text = "velocidade do tp:"
TPLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TPLabel.TextSize = 10
TPLabel.Font = Enum.Font.GothamBold
TPLabel.ZIndex = 2
TPLabel.Parent = Menu

local TPBox = Instance.new("TextBox")
TPBox.Size = UDim2.new(0, 90, 0, 26)
TPBox.Position = UDim2.new(0, 20, 0, 198)
TPBox.BackgroundColor3 = Color3.fromRGB(255, 220, 235)
TPBox.BorderSizePixel = 0
TPBox.Text = tostring(TPTime)
TPBox.TextColor3 = Color3.fromRGB(200, 80, 140)
TPBox.TextSize = 12
TPBox.Font = Enum.Font.GothamBold
TPBox.ZIndex = 2
TPBox.Parent = Menu
local TBC = Instance.new("UICorner")
TBC.CornerRadius = UDim.new(0, 6)
TBC.Parent = TPBox
TPBox.FocusLost:Connect(function()
    local n = tonumber(TPBox.Text)
    if n and n > 0 then TPTime = n; saveData() end
end)

local TPApply = Instance.new("TextButton")
TPApply.Size = UDim2.new(0, 110, 0, 26)
TPApply.Position = UDim2.new(0, 115, 0, 198)
TPApply.BackgroundColor3 = Color3.fromRGB(255, 170, 200)
TPApply.BorderSizePixel = 0
TPApply.Text = "aplicar tp"
TPApply.TextColor3 = Color3.fromRGB(255, 255, 255)
TPApply.TextSize = 12
TPApply.Font = Enum.Font.GothamBold
TPApply.ZIndex = 2
TPApply.Parent = Menu
local TAC = Instance.new("UICorner")
TAC.CornerRadius = UDim.new(0, 6)
TAC.Parent = TPApply
TPApply.MouseButton1Click:Connect(function()
    local n = tonumber(TPBox.Text)
    if n and n > 0 then TPTime = n; saveData() end
end)

-- SPEED DO PLAYER
local SpeedLabel = Instance.new("TextLabel")
SpeedLabel.Size = UDim2.new(1, 0, 0, 14)
SpeedLabel.Position = UDim2.new(0, 0, 0, 232)
SpeedLabel.BackgroundTransparency = 1
SpeedLabel.Text = "speed do player:"
SpeedLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
SpeedLabel.TextSize = 11
SpeedLabel.Font = Enum.Font.GothamBold
SpeedLabel.ZIndex = 2
SpeedLabel.Parent = Menu

local SpeedBox = Instance.new("TextBox")
SpeedBox.Size = UDim2.new(0, 90, 0, 26)
SpeedBox.Position = UDim2.new(0, 20, 0, 248)
SpeedBox.BackgroundColor3 = Color3.fromRGB(255, 220, 235)
SpeedBox.BorderSizePixel = 0
SpeedBox.Text = tostring(SpeedValue)
SpeedBox.TextColor3 = Color3.fromRGB(200, 80, 140)
SpeedBox.TextSize = 12
SpeedBox.Font = Enum.Font.GothamBold
SpeedBox.ZIndex = 2
SpeedBox.Parent = Menu
local SBC = Instance.new("UICorner")
SBC.CornerRadius = UDim.new(0, 6)
SBC.Parent = SpeedBox
SpeedBox.FocusLost:Connect(function()
    local n = tonumber(SpeedBox.Text)
    if n then setSpeed(n) end
end)

local ApplyBtn = Instance.new("TextButton")
ApplyBtn.Size = UDim2.new(0, 110, 0, 26)
ApplyBtn.Position = UDim2.new(0, 115, 0, 248)
ApplyBtn.BackgroundColor3 = Color3.fromRGB(255, 170, 200)
ApplyBtn.BorderSizePixel = 0
ApplyBtn.Text = "aplicar speed"
ApplyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ApplyBtn.TextSize = 12
ApplyBtn.Font = Enum.Font.GothamBold
ApplyBtn.ZIndex = 2
ApplyBtn.Parent = Menu
local ABC = Instance.new("UICorner")
ABC.CornerRadius = UDim.new(0, 6)
ABC.Parent = ApplyBtn
ApplyBtn.MouseButton1Click:Connect(function()
    local n = tonumber(SpeedBox.Text)
    if n then setSpeed(n) end
end)

Toggle.MouseButton1Click:Connect(function()
    Menu.Visible = not Menu.Visible
    if Menu.Visible and TPCoords then createMarker(TPCoords) end
end)

LP.CharacterAdded:Connect(function(char)
    task.wait(1)
    local hum = char:FindFirstChildOfClass("Humanoid")
    if hum then hum.WalkSpeed = SpeedValue end
end)

task.spawn(playIntro)
print("[Girl Hub TP V1] carregado.")
