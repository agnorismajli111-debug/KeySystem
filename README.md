-- ULTIMATE AGNX GUI v2.0
-- Created with premium features

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

-- Create ScreenGui with blur effect
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AgnXUltimate"
screenGui.Parent = LocalPlayer:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

-- Background blur
local blur = Instance.new("BlurEffect")
blur.Size = 0
blur.Parent = game:GetService("Lighting")

-- Create main frame with glass effect
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 400, 0, 350)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -175)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 25, 35)
mainFrame.BackgroundTransparency = 0.15
mainFrame.BorderSizePixel = 0
mainFrame.ClipsDescendants = true
mainFrame.Parent = screenGui

-- Glass border
local border = Instance.new("Frame")
border.Size = UDim2.new(1, 0, 1, 0)
border.Position = UDim2.new(0, 0, 0, 0)
border.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
border.BackgroundTransparency = 0.85
border.BorderSizePixel = 1
border.BorderColor3 = Color3.fromRGB(100, 150, 255)
border.Parent = mainFrame

-- Make draggable
local dragging = false
local dragStart = nil
local startPos = nil

mainFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = mainFrame.Position
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
        local delta = input.Position - dragStart
        mainFrame.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

UserInputService.InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = false
    end
end)

-- Title bar with gradient
local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 40)
titleBar.Position = UDim2.new(0, 0, 0, 0)
titleBar.BackgroundColor3 = Color3.fromRGB(30, 40, 60)
titleBar.BackgroundTransparency = 0.3
titleBar.BorderSizePixel = 0
titleBar.Parent = mainFrame

-- Gradient overlay
local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(40, 60, 120)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(80, 40, 160))
})
gradient.Parent = titleBar

-- Title with glow effect
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, -80, 1, 0)
titleLabel.Position = UDim2.new(0, 10, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "✦ AGNX ULTIMATE ✦"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.TextSize = 18
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextXAlignment = Enum.TextXAlignment.Left
titleLabel.TextYAlignment = Enum.TextYAlignment.Center
titleLabel.Parent = titleBar

-- Close button with hover animation
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 35, 0, 35)
closeButton.Position = UDim2.new(1, -38, 0, 2.5)
closeButton.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "✕"
closeButton.TextSize = 18
closeButton.Font = Enum.Font.GothamBold
closeButton.BorderSizePixel = 0
closeButton.Parent = titleBar

closeButton.MouseEnter:Connect(function()
    TweenService:Create(closeButton, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 0, 0)}):Play()
end)
closeButton.MouseLeave:Connect(function()
    TweenService:Create(closeButton, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(200, 50, 50)}):Play()
end)

closeButton.MouseButton1Click:Connect(function()
    -- Fade out animation
    TweenService:Create(mainFrame, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
    TweenService:Create(blur, TweenInfo.new(0.3), {Size = 0}):Play()
    task.wait(0.3)
    screenGui:Destroy()
    blur:Destroy()
end)

-- Minimize button
local minButton = Instance.new("TextButton")
minButton.Size = UDim2.new(0, 35, 0, 35)
minButton.Position = UDim2.new(1, -76, 0, 2.5)
minButton.BackgroundColor3 = Color3.fromRGB(50, 50, 80)
minButton.TextColor3 = Color3.fromRGB(255, 255, 255)
minButton.Text = "─"
minButton.TextSize = 18
minButton.Font = Enum.Font.GothamBold
minButton.BorderSizePixel = 0
minButton.Parent = titleBar

local minimized = false
minButton.MouseButton1Click:Connect(function()
    minimized = not minimized
    if minimized then
        TweenService:Create(mainFrame, TweenInfo.new(0.3), {Size = UDim2.new(0, 400, 0, 40)}):Play()
        buttonContainer.Visible = false
        minButton.Text = "□"
    else
        TweenService:Create(mainFrame, TweenInfo.new(0.3), {Size = UDim2.new(0, 400, 0, 350)}):Play()
        task.wait(0.3)
        buttonContainer.Visible = true
        minButton.Text = "─"
    end
end)

-- Button container with scroll
local buttonContainer = Instance.new("ScrollingFrame")
buttonContainer.Size = UDim2.new(1, -20, 1, -70)
buttonContainer.Position = UDim2.new(0, 10, 0, 50)
buttonContainer.BackgroundTransparency = 1
buttonContainer.BorderSizePixel = 0
buttonContainer.ScrollBarThickness = 4
buttonContainer.ScrollBarImageColor3 = Color3.fromRGB(100, 150, 255)
buttonContainer.CanvasSize = UDim2.new(0, 0, 0, 260)
buttonContainer.Parent = mainFrame

-- Button grid layout
local grid = Instance.new("UIGridLayout")
grid.SortOrder = Enum.SortOrder.LayoutOrder
grid.CellPadding = UDim2.new(0, 8, 0, 8)
grid.CellSize = UDim2.new(0, 118, 0, 40)
grid.Parent = buttonContainer

-- Define versions with colors
local versions = {
    {
        name = "⚡ v1.o",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v1.0/refs/heads/main/README.md"))()',
        color = Color3.fromRGB(52, 152, 219)
    },
    {
        name = "⚡ v2.o",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v1.o/refs/heads/main/README.md"))()',
        color = Color3.fromRGB(46, 204, 113)
    },
    {
        name = "⚡ v3.o",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v3.o/refs/heads/main/README.md"))()',
        color = Color3.fromRGB(241, 196, 15)
    },
    {
        name = "🔒 v4.o (PB)",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/...l/refs/heads/main/README.md"))()',
        requiresKey = true,
        key = "pxGGGsarQgstLSUGab",
        color = Color3.fromRGB(231, 76, 60)
    },
    {
        name = "🔓 v4.o (F)",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v4.1.o/refs/heads/main/Loader.lua"))()',
        color = Color3.fromRGB(155, 89, 182)
    },
    {
        name = "🔒 v5.o",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/A.../refs/heads/main/README.md"))()',
        requiresKey = true,
        key = "AgnXKey5.o.1",
        color = Color3.fromRGB(231, 76, 60)
    },
    {
        name = "🏆 .win",
        loadstring = 'loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX.win/refs/heads/main/README.md"))()',
        color = Color3.fromRGB(255, 215, 0)
    }
}

-- Store UI elements
local buttons = {}
local currentMode = nil
local inputFrame = nil
local textBox = nil
local submitBtn = nil
local returnBtn = nil

-- Enhanced message function
local function showNotification(title, message, isSuccess)
    local notif = Instance.new("Frame")
    notif.Size = UDim2.new(0, 300, 0, 60)
    notif.Position = UDim2.new(0.5, -150, 0, 10)
    notif.BackgroundColor3 = isSuccess and Color3.fromRGB(46, 204, 113) or Color3.fromRGB(231, 76, 60)
    notif.BackgroundTransparency = 0.1
    notif.BorderSizePixel = 0
    notif.Parent = screenGui
    
    local glow = Instance.new("Frame")
    glow.Size = UDim2.new(1, 0, 1, 0)
    glow.Position = UDim2.new(0, 0, 0, 0)
    glow.BackgroundColor3 = isSuccess and Color3.fromRGB(46, 204, 113) or Color3.fromRGB(231, 76, 60)
    glow.BackgroundTransparency = 0.5
    glow.BorderSizePixel = 0
    glow.Parent = notif
    
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Size = UDim2.new(1, 0, 0, 20)
    titleLabel.Position = UDim2.new(0, 10, 0, 5)
    titleLabel.BackgroundTransparency = 1
    titleLabel.Text = title
    titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    titleLabel.TextSize = 14
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.TextXAlignment = Enum.TextXAlignment.Left
    titleLabel.Parent = notif
    
    local msgLabel = Instance.new("TextLabel")
    msgLabel.Size = UDim2.new(1, -20, 0, 20)
    msgLabel.Position = UDim2.new(0, 10, 0, 30)
    msgLabel.BackgroundTransparency = 1
    msgLabel.Text = message
    msgLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    msgLabel.TextSize = 12
    msgLabel.Font = Enum.Font.Gotham
    msgLabel.TextXAlignment = Enum.TextXAlignment.Left
    msgLabel.Parent = notif
    
    TweenService:Create(notif, TweenInfo.new(0.3), {Position = UDim2.new(0.5, -150, 0, 20)}):Play()
    task.wait(2)
    TweenService:Create(notif, TweenInfo.new(0.3), {Position = UDim2.new(0.5, -150, 0, -80)}):Play()
    task.wait(0.3)
    notif:Destroy()
end

-- Execute and close with animation
local function executeAndClose(versionData)
    local success, err = pcall(function()
        local loadFunc = loadstring(versionData.loadstring)
        if loadFunc then
            loadFunc()
            showNotification("✅ SUCCESS", versionData.name .. " loaded!", true)
        else
            showNotification("❌ ERROR", "Failed to load " .. versionData.name, false)
        end
    end)
    
    if not success then
        showNotification("❌ ERROR", tostring(err), false)
    end
    
    task.wait(0.5)
    -- Fade and close
    TweenService:Create(mainFrame, TweenInfo.new(0.3), {BackgroundTransparency = 1}):Play()
    TweenService:Create(blur, TweenInfo.new(0.3), {Size = 0}):Play()
    task.wait(0.3)
    screenGui:Destroy()
    blur:Destroy()
end

-- Show buttons
local function showButtons()
    if inputFrame then
        inputFrame.Visible = false
    end
    for _, btn in pairs(buttons) do
        btn.Visible = true
    end
    currentMode = nil
end

-- Create input system
local function createInputSystem()
    if inputFrame then
        inputFrame.Visible = true
        return
    end
    
    inputFrame = Instance.new("Frame")
    inputFrame.Size = UDim2.new(1, -20, 1, -70)
    inputFrame.Position = UDim2.new(0, 10, 0, 50)
    inputFrame.BackgroundTransparency = 1
    inputFrame.Parent = mainFrame
    
    -- Return button
    returnBtn = Instance.new("TextButton")
    returnBtn.Size = UDim2.new(0, 80, 0, 35)
    returnBtn.Position = UDim2.new(1, -85, 0, 0)
    returnBtn.BackgroundColor3 = Color3.fromRGB(200, 50, 50)
    returnBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    returnBtn.Text = "↩ RETURN"
    returnBtn.TextSize = 11
    returnBtn.Font = Enum.Font.GothamBold
    returnBtn.BorderSizePixel = 0
    returnBtn.Parent = inputFrame
    
    returnBtn.MouseEnter:Connect(function()
        TweenService:Create(returnBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(255, 0, 0)}):Play()
    end)
    returnBtn.MouseLeave:Connect(function()
        TweenService:Create(returnBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(200, 50, 50)}):Play()
    end)
    returnBtn.MouseButton1Click:Connect(showButtons)
    
    -- Key icon
    local keyIcon = Instance.new("TextLabel")
    keyIcon.Size = UDim2.new(0, 40, 0, 40)
    keyIcon.Position = UDim2.new(0, 0, 0, 30)
    keyIcon.BackgroundTransparency = 1
    keyIcon.Text = "🔑"
    keyIcon.TextSize = 30
    keyIcon.Parent = inputFrame
    
    -- Info label
    local infoLabel = Instance.new("TextLabel")
    infoLabel.Size = UDim2.new(1, -50, 0, 25)
    infoLabel.Position = UDim2.new(0, 45, 0, 30)
    infoLabel.BackgroundTransparency = 1
    infoLabel.Text = "ENTER KEY FOR " .. currentMode.name:upper()
    infoLabel.TextColor3 = Color3.fromRGB(200, 220, 255)
    infoLabel.TextSize = 13
    infoLabel.Font = Enum.Font.GothamBold
    infoLabel.TextXAlignment = Enum.TextXAlignment.Left
    infoLabel.Parent = inputFrame
    
    -- TextBox with glass effect
    textBox = Instance.new("TextBox")
    textBox.Size = UDim2.new(0, 200, 0, 35)
    textBox.Position = UDim2.new(0, 0, 0, 65)
    textBox.BackgroundColor3 = Color3.fromRGB(30, 40, 60)
    textBox.BackgroundTransparency = 0.5
    textBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    textBox.Text = "Enter key..."
    textBox.TextSize = 13
    textBox.Font = Enum.Font.Gotham
    textBox.ClearTextOnFocus = false
    textBox.Parent = inputFrame
    
    -- TextBox glow
    local textGlow = Instance.new("Frame")
    textGlow.Size = UDim2.new(1, 0, 1, 0)
    textGlow.Position = UDim2.new(0, 0, 0, 0)
    textGlow.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
    textGlow.BackgroundTransparency = 0.8
    textGlow.BorderSizePixel = 0
    textGlow.Parent = textBox
    
    -- Submit button with animation
    submitBtn = Instance.new("TextButton")
    submitBtn.Size = UDim2.new(0, 100, 0, 35)
    submitBtn.Position = UDim2.new(0, 210, 0, 65)
    submitBtn.BackgroundColor3 = Color3.fromRGB(46, 204, 113)
    submitBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    submitBtn.Text = "✓ SUBMIT"
    submitBtn.TextSize = 13
    submitBtn.Font = Enum.Font.GothamBold
    submitBtn.BorderSizePixel = 0
    submitBtn.Parent = inputFrame
    
    submitBtn.MouseEnter:Connect(function()
        TweenService:Create(submitBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(39, 174, 96)}):Play()
        TweenService:Create(submitBtn, TweenInfo.new(0.2), {Size = UDim2.new(0, 110, 0, 35)}):Play()
    end)
    submitBtn.MouseLeave:Connect(function()
        TweenService:Create(submitBtn, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(46, 204, 113)}):Play()
        TweenService:Create(submitBtn, TweenInfo.new(0.2), {Size = UDim2.new(0, 100, 0, 35)}):Play()
    end)
    
    submitBtn.MouseButton1Click:Connect(function()
        local input = textBox.Text
        if currentMode and currentMode.requiresKey then
            if input == currentMode.key then
                showNotification("✅ CORRECT KEY!", "Access granted for " .. currentMode.name, true)
                task.wait(0.5)
                executeAndClose(currentMode)
            else
                showNotification("❌ INVALID KEY", "Wrong key for " .. currentMode.name, false)
                -- Shake animation
                TweenService:Create(textBox, TweenInfo.new(0.1), {Position = UDim2.new(0, 10, 0, 65)}):Play()
                task.wait(0.1)
                TweenService:Create(textBox, TweenInfo.new(0.1), {Position = UDim2.new(0, -10, 0, 65)}):Play()
                task.wait(0.1)
                TweenService:Create(textBox, TweenInfo.new(0.1), {Position = UDim2.new(0, 0, 0, 65)}):Play()
            end
        end
    end)
end

-- Handle button click
local function handleButtonClick(versionData)
    if versionData.requiresKey then
        for _, btn in pairs(buttons) do
            btn.Visible = false
        end
        currentMode = versionData
        createInputSystem()
    else
        executeAndClose(versionData)
    end
end

-- Create buttons with animations
for i, versionData in ipairs(versions) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 118, 0, 40)
    button.BackgroundColor3 = versionData.color
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Text = versionData.name
    button.TextSize = 12
    button.Font = Enum.Font.GothamBold
    button.BorderSizePixel = 0
    button.Parent = buttonContainer
    button.LayoutOrder = i
    
    -- Glow effect
    local glow = Instance.new("Frame")
    glow.Size = UDim2.new(1, 0, 1, 0)
    glow.Position = UDim2.new(0, 0, 0, 0)
    glow.BackgroundColor3 = versionData.color
    glow.BackgroundTransparency = 0.7
    glow.BorderSizePixel = 0
    glow.Parent = button
    
    -- Hover animation
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {Size = UDim2.new(0, 125, 0, 45)}):Play()
        TweenService:Create(glow, TweenInfo.new(0.2), {BackgroundTransparency = 0.3}):Play()
    end)
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {Size = UDim2.new(0, 118, 0, 40)}):Play()
        TweenService:Create(glow, TweenInfo.new(0.2), {BackgroundTransparency = 0.7}):Play()
    end)
    
    -- Click animation
    button.MouseButton1Click:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.1), {Size = UDim2.new(0, 110, 0, 35)}):Play()
        task.wait(0.1)
        TweenService:Create(button, TweenInfo.new(0.1), {Size = UDim2.new(0, 125, 0, 45)}):Play()
        task.wait(0.1)
        TweenService:Create(button, TweenInfo.new(0.1), {Size = UDim2.new(0, 118, 0, 40)}):Play()
        handleButtonClick(versionData)
    end)
    
    buttons[versionData.name] = button
end

-- Initialize blur
TweenService:Create(blur, TweenInfo.new(0.5), {Size = 12}):Play()

-- Entrance animation
mainFrame.BackgroundTransparency = 1
mainFrame.Size = UDim2.new(0, 300, 0, 250)
TweenService:Create(mainFrame, TweenInfo.new(0.5, Enum.EasingStyle.Back), {
    BackgroundTransparency = 0.15,
    Size = UDim2.new(0, 400, 0, 350)
}):Play()

print("✦ AGNX ULTIMATE v2.0 LOADED ✦")
print("Created with premium features")
