-- ===== KEY SYSTEM GUI + ANTI-CHEAT BYPASS =====

-- ===== PART 1: ANTI-CHEAT BYPASS =====

local _stbl
_stbl = hookfunction(getrenv().setmetatable, newcclosure(function(tbl, mt)
    if mt and typeof(mt) == "table" and rawget(mt, "__mode") == "kv" then
        local tr = debug.traceback()
        if tr:find("MiscellaneousController") then
            return _stbl({1,2,3}, {})
        end
    end
    return _stbl(tbl, mt)
end))

coroutine.wrap(function()
    pcall(function()
        local function disableScripts(obj)
            pcall(function()
                if obj:IsA("LocalScript") or obj:IsA("ModuleScript") then
                    local success, name = pcall(function() return obj.Name:lower() end)
                    if not success or not name then return end
                    local keywords = {"anticheat","ac","detection","ban","kick","security","moderation"}
                    for i = 1, #keywords do
                        if name:find(keywords[i]) then
                            pcall(function() obj.Disabled = true end)
                            break
                        end
                    end
                end
            end)
        end
        
        pcall(function()
            local descendants = game:GetDescendants()
            for i = 1, #descendants do disableScripts(descendants[i]) end
        end)
        pcall(function() game.DescendantAdded:Connect(disableScripts) end)
    end)
    
    pcall(function()
        local network = game:GetService("NetworkClient")
        if not network then return end
        network.ChildAdded:Connect(function(child)
            pcall(function()
                local success, name = pcall(function() return child.Name:lower() end)
                if success and name then
                    if name:find("anticheat") or name:find("detection") then
                        pcall(function() child:Destroy() end)
                    end
                end
            end)
        end)
    end)
end)()

pcall(function()
    local fakeEvent = Instance.new("RemoteEvent")
    fakeEvent.Name = "ClientAlert"
    fakeEvent.Parent = game.Players.LocalPlayer
end)

pcall(function()
    local replicatedFirst = game:GetService("ReplicatedFirst")
    local targetScript = replicatedFirst:WaitForChild("LocalScript3", 10)
    local gc = getgc(false)
    
    for i = 1, #gc do
        local func = gc[i]
        if type(func) ~= "function" then continue end
        
        local success, env = pcall(getfenv, func)
        if not success or type(env) ~= "table" then continue end
        
        local success2, scriptObj = pcall(function() return rawget(env, "script") end)
        if not success2 or not scriptObj or typeof(scriptObj) ~= "Instance" then continue end
        
        if scriptObj == targetScript then
            local success3, constants = pcall(debug.getconstants, func)
            if not success3 or type(constants) ~= "table" then continue end
            
            for j = 1, #constants do
                local const = constants[j]
                if type(const) == "string" and (const:find("TakeTheL") or const:find("ban") or const:find("kick")) then
                    pcall(function() hookfunction(func, function() end) end)
                    break
                end
            end
        end
    end
end)

task.wait(4)

-- ===== PART 2: KEY SYSTEM GUI =====

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
mainFrame.Active = true
mainFrame.Draggable = true
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

-- Title Gradient
local titleGradient = Instance.new("UIGradient")
titleGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(100, 150, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(200, 100, 255))
})
titleGradient.Parent = title

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

-- ===== VALID KEYS =====
local VALID_KEY_1 = "AgnXKey111"
local VALID_KEY_2 = "pxGGGsarQgstLSUGab"

-- ===== LOADSTRING FUNCTIONS =====
local function executeLoadstring1()
    pcall(function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/AgnX-v4.1.o/refs/heads/main/Loader.lua"))()
    end)
end

local function executeLoadstring2()
    pcall(function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/agnorismajli111-debug/...l/refs/heads/main/README.md"))()
    end)
end

-- ===== SUBMIT FUNCTION =====
local function handleKeySubmission()
    local inputKey = keyInput.Text
    local cleanedKey = inputKey:gsub("^%s+", ""):gsub("%s+$", "")
    
    if cleanedKey == VALID_KEY_1 then
        statusLabel.Text = "✅ Success, Loading AgnX v4.o (Free)"
        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
        submitButton.Visible = false
        keyInput.Visible = false
        title.Text = "✅ Loading..."
        
        task.wait(0.5)
        screenGui:Destroy()
        executeLoadstring1()
        
    elseif cleanedKey == VALID_KEY_2 then
        statusLabel.Text = "✅ Success, Loading AgnX v4.o (Paid)"
        statusLabel.TextColor3 = Color3.fromRGB(0, 255, 100)
        submitButton.Visible = false
        keyInput.Visible = false
        title.Text = "✅ Loading..."
        
        task.wait(0.5)
        screenGui:Destroy()
        executeLoadstring2()
        
    else
        statusLabel.Text = "❌ Invalid key! Please try again."
        statusLabel.TextColor3 = Color3.fromRGB(255, 80, 80)
        keyInput.Text = ""
        keyInput:CaptureFocus()
        
        -- Shake animation effect
        local originalPosition = mainFrame.Position
        for i = 1, 3 do
            mainFrame.Position = UDim2.new(0.5, -200 + (i % 2 == 0 and 10 or -10), 0.5, -125)
            task.wait(0.05)
        end
        mainFrame.Position = originalPosition
        
        -- Reset status after 2 seconds
        task.wait(2)
        if not submitButton.Visible then return end
        statusLabel.Text = "Enter your key to continue"
        statusLabel.TextColor3 = Color3.fromRGB(200, 200, 210)
    end
end

-- ===== BUTTON EVENTS =====
submitButton.MouseButton1Click:Connect(handleKeySubmission)

-- Enter key support
keyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        handleKeySubmission()
    end
end)

-- Button hover effects
submitButton.MouseEnter:Connect(function()
    submitButton.BackgroundColor3 = Color3.fromRGB(90, 150, 255)
end)

submitButton.MouseLeave:Connect(function()
    submitButton.BackgroundColor3 = Color3.fromRGB(70, 120, 200)
end)

-- Auto-focus on input
task.wait(0.5)
keyInput:CaptureFocus()

-- ===== CONSOLE COMMANDS =====
_G.KeySystem = {
    Show = function()
        screenGui.Enabled = true
        print("🔑 Key System GUI opened")
    end,
    Hide = function()
        screenGui.Enabled = false
        print("🔑 Key System GUI hidden")
    end,
    AddKey = function(key, loadFunc)
        if key and loadFunc then
            -- Add custom key functionality
            print("🔑 Custom key added: " .. key)
        end
    end,
    Status = function()
        print("═══════════════════════════════════════════")
        print("🔑 KEY SYSTEM STATUS:")
        print("  GUI Visible: " .. tostring(screenGui.Enabled))
        print("  Valid Keys: " .. VALID_KEY_1 .. ", " .. VALID_KEY_2)
        print("═══════════════════════════════════════════")
    end
}

-- ===== STARTUP MESSAGE =====
print("═══════════════════════════════════════════")
print("✅ KEY SYSTEM GUI + ANTI-CHEAT BYPASS LOADED!")
print("═══════════════════════════════════════════")
print("📌 Anti-Cheat Bypass: ACTIVE")
print("")
print("📌 Valid Keys:")
print("   🔑 " .. VALID_KEY_1 .. " (Free)")
print("   🔑 " .. VALID_KEY_2 .. " (Paid)")
print("")
print("📌 Console Commands:")
print("   _G.KeySystem.Show() - Show GUI")
print("   _G.KeySystem.Hide() - Hide GUI")
print("   _G.KeySystem.Status() - Show status")
print("═══════════════════════════════════════════")
