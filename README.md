-- ===== ANTI-CHEAT BYPASS + LEAVE GUI =====

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
                    local keywords = {"anticheat","ac","detection","ban","kick","security","moderation","anti","cheat","exploit","inject","protect"}
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
                    if name:find("anticheat") or name:find("detection") or name:find("anti") or name:find("cheat") then
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
                if type(const) == "string" and (const:find("TakeTheL") or const:find("ban") or const:find("kick") or const:find("detect")) then
                    pcall(function() hookfunction(func, function() end) end)
                    break
                end
            end
        end
    end
end)

task.wait(4)

-- ===== PART 2: LEAVE GUI =====

-- Create a ScreenGui
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Name = "LeaveGUI"
gui.ResetOnSpawn = false
gui.Parent = player.PlayerGui

-- Main Frame (the textbox)
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 200)
frame.Position = UDim2.new(0.5, -200, 0.5, -100)
frame.BackgroundColor3 = Color3.fromRGB(38, 38, 51)
frame.BorderColor3 = Color3.fromRGB(102, 102, 204)
frame.BorderSizePixel = 2
frame.Active = true
frame.Draggable = true
frame.Parent = gui

-- Corner rounding
local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 8)
corner.Parent = frame

-- Title
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 30)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "Dear, User"
title.TextColor3 = Color3.fromRGB(255, 204, 153)
title.TextSize = 22
title.Font = Enum.Font.SourceSansBold
title.TextXAlignment = Enum.TextXAlignment.Center
title.Parent = frame

-- Separator Line
local separator = Instance.new("Frame")
separator.Size = UDim2.new(0.9, 0, 0, 2)
separator.Position = UDim2.new(0.05, 0, 0, 45)
separator.BackgroundColor3 = Color3.fromRGB(77, 77, 128)
separator.BackgroundTransparency = 0
separator.Parent = frame

-- Message Line 1
local message1 = Instance.new("TextLabel")
message1.Size = UDim2.new(1, -20, 0, 25)
message1.Position = UDim2.new(0, 10, 0, 55)
message1.BackgroundTransparency = 1
message1.Text = "The script is updating"
message1.TextColor3 = Color3.fromRGB(255, 255, 255)
message1.TextSize = 16
message1.Font = Enum.Font.SourceSans
message1.TextXAlignment = Enum.TextXAlignment.Center
message1.Parent = frame

-- Message Line 2
local message2 = Instance.new("TextLabel")
message2.Size = UDim2.new(1, -20, 0, 25)
message2.Position = UDim2.new(0, 10, 0, 78)
message2.BackgroundTransparency = 1
message2.Text = "please wait a while"
message2.TextColor3 = Color3.fromRGB(255, 255, 255)
message2.TextSize = 16
message2.Font = Enum.Font.SourceSans
message2.TextXAlignment = Enum.TextXAlignment.Center
message2.Parent = frame

-- LEAVE Button
local button = Instance.new("TextButton")
button.Size = UDim2.new(0, 120, 0, 35)
button.Position = UDim2.new(0.5, -60, 0, 125)
button.BackgroundColor3 = Color3.fromRGB(128, 25, 25)
button.BorderColor3 = Color3.fromRGB(204, 77, 77)
button.BorderSizePixel = 2
button.Text = "LEAVE"
button.TextColor3 = Color3.fromRGB(255, 255, 255)
button.TextSize = 20
button.Font = Enum.Font.SourceSansBold
button.Parent = frame

-- Button corner rounding
local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 4)
btnCorner.Parent = button

-- Button hover effect
button.MouseEnter:Connect(function()
    button.BackgroundColor3 = Color3.fromRGB(204, 51, 51)
    button.BorderColor3 = Color3.fromRGB(255, 102, 102)
end)

button.MouseLeave:Connect(function()
    button.BackgroundColor3 = Color3.fromRGB(128, 25, 25)
    button.BorderColor3 = Color3.fromRGB(204, 77, 77)
end)

-- Button click to leave game
button.MouseButton1Click:Connect(function()
    game:Shutdown() -- Closes the game
end)

-- ===== CONSOLE COMMANDS =====
_G.LeaveGUI = {
    Show = function()
        gui.Enabled = true
        print("📌 Leave GUI shown")
    end,
    Hide = function()
        gui.Enabled = false
        print("📌 Leave GUI hidden")
    end,
    Destroy = function()
        gui:Destroy()
        print("📌 Leave GUI destroyed")
    end,
    Status = function()
        print("═══════════════════════════════════════════")
        print("📌 LEAVE GUI STATUS:")
        print("  Visible: " .. tostring(gui.Enabled))
        print("  Anti-Cheat Bypass: ACTIVE")
        print("═══════════════════════════════════════════")
    end
}

-- ===== STARTUP MESSAGE =====
print("═══════════════════════════════════════════")
print("✅ ANTI-CHEAT BYPASS + LEAVE GUI LOADED!")
print("═══════════════════════════════════════════")
print("📌 Anti-Cheat Bypass: ACTIVE")
print("📌 Click 'LEAVE' to exit the game")
print("📌 GUI is draggable")
print("")
print("📌 Console Commands:")
print("   _G.LeaveGUI.Show() - Show GUI")
print("   _G.LeaveGUI.Hide() - Hide GUI")
print("   _G.LeaveGUI.Destroy() - Destroy GUI")
print("   _G.LeaveGUI.Status() - Show status")
print("═══════════════════════════════════════════")
