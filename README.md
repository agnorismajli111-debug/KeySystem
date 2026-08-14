-- Key System GUI with two key types
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Create main screen GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "KeySystem"
screenGui.ResetOnSpawn = false
screenGui.Parent = playerGui

-- Main frame
local mainFrame = Instance.new("Frame")
mainFrame.Name = "MainFrame"
mainFrame.Size = UDim2.new(0, 400, 0, 250)
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -125)
mainFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
mainFrame.BackgroundTransparency = 0.3
mainFrame.BorderSizePixel = 0
mainFrame.Parent = screenGui

-- Corner rounding for main frame
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 12)
corner.Parent = mainFrame

-- Title
local title = Instance.new("TextLabel")
title.Name = "Title"
title.Size = UDim2.new(1, 0, 0, 50)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundTransparency = 1
title.Text = "🔑 KEY SYSTEM"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextSize = 24
title.Font = Enum.Font.GothamBold
title.Parent = mainFrame

-- Key input field
local keyInput = Instance.new("TextBox")
keyInput.Name = "KeyInput"
keyInput.Size = UDim2.new(0.8, 0, 0, 40)
keyInput.Position = UDim2.new(0.1, 0, 0.3, 0)
keyInput.BackgroundColor3 = Color3.fromRGB(50, 50, 60)
keyInput.BackgroundTransparency = 0.2
keyInput.Text = ""
keyInput.TextColor3 = Color3.fromRGB(255, 255, 255)
keyInput.TextSize = 16
keyInput.Font = Enum.Font.Gotham
keyInput.PlaceholderText = "Enter your key here..."
keyInput.PlaceholderColor3 = Color3.fromRGB(150, 150, 160)
keyInput.ClearTextOnFocus = false
keyInput.Parent = mainFrame

-- Corner rounding for input
local inputCorner = Instance.new("UICorner")
inputCorner.CornerRadius = UDim.new(0, 8)
inputCorner.Parent = keyInput

-- Submit button
local submitButton = Instance.new("TextButton")
submitButton.Name = "SubmitButton"
submitButton.Size = UDim2.new(0.4, 0, 0, 45)
submitButton.Position = UDim2.new(0.3, 0, 0.55, 0)
submitButton.BackgroundColor3 = Color3.fromRGB(70, 120, 200)
submitButton.Text = "SUBMIT"
submitButton.TextColor3 = Color3.fromRGB(255, 255, 255)
submitButton.TextSize = 18
submitButton.Font = Enum.Font.GothamBold
submitButton.Parent = mainFrame

-- Corner rounding for button
local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0, 8)
buttonCorner.Parent = submitButton

-- Status label
local statusLabel = Instance.new("TextLabel")
statusLabel.Name = "StatusLabel"
statusLabel.Size = UDim2.new(1, 0, 0, 30)
statusLabel.Position = UDim2.new(0, 0, 0.78, 0)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = "Enter your key to continue"
statusLabel.TextColor3 = Color3.fromRGB(200, 200, 210)
statusLabel.TextSize = 14
statusLabel.Font = Enum.Font.Gotham
statusLabel.Parent = mainFrame

-- Valid keys
local VALID_KEY_1 = "AgnXKey111"
local VALID_KEY_2 = "burgerbosi123"

-- Loadstring functions
local function executeLoadstring1()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v4.1.o/refs/heads/main/Loader.lua"))()
end

local function executeLoadstring2()
    loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/...l/refs/heads/main/README.md"))()
end

-- Submit function
local function handleKeySubmission()
    local inputKey = keyInput.Text
    local cleanedKey = inputKey:gsub("^%s+", ""):gsub("%s+$", "")
    
    if cleanedKey == VALID_KEY_1 then
        statusLabel.Text = "✅ Success, Loading AgnX v4.o (Free)"
        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
        submitButton.Visible = false
        keyInput.Visible = false
        title.Text = "✅ Loading..."
        
        -- Delete GUI and execute loadstring
        task.wait(0.5)
        screenGui:Destroy()
        executeLoadstring1()
        
    elseif cleanedKey == VALID_KEY_2 then
        statusLabel.Text = "✅ Success, Loading AgnX v4.o (Paid)"
        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
        submitButton.Visible = false
        keyInput.Visible = false
        title.Text = "✅ Loading..."
        
        -- Delete GUI and execute loadstring
        task.wait(0.5)
        screenGui:Destroy()
        executeLoadstring2()
        
    else
        statusLabel.Text = "❌ Invalid key! Please try again."
        statusLabel.TextColor3 = Color3.fromRGB(255, 80, 80)
        keyInput.Text = ""
        keyInput:CaptureFocus()
        
        -- Reset status after 2 seconds
        task.wait(2)
        if not submitButton.Visible then return end
        statusLabel.Text = "Enter your key to continue"
        statusLabel.TextColor3 = Color3.fromRGB(200, 200, 210)
    end
end

-- Button click event
submitButton.MouseButton1Click:Connect(handleKeySubmission)

-- Enter key support
keyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        handleKeySubmission()
    end
end)

-- Auto-focus on input
task.wait(0.5)
keyInput:CaptureFocus()

-- Additional styling for modern look
local titleGradient = Instance.new("UIGradient")
titleGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(100, 150, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(200, 100, 255))
})
titleGradient.Parent = title

-- Subtle glow effect for main frame
local glow = Instance.new("Frame")
glow.Name = "Glow"
glow.Size = UDim2.new(1.1, 0, 1.1, 0)
glow.Position = UDim2.new(-0.05, 0, -0.05, 0)
glow.BackgroundColor3 = Color3.fromRGB(100, 150, 255)
glow.BackgroundTransparency = 0.95
glow.BorderSizePixel = 0
glow.Parent = mainFrame

local glowCorner = Instance.new("UICorner")
glowCorner.CornerRadius = UDim.new(0, 16)
glowCorner.Parent = glow
