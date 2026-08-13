-- Create a ScreenGui
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui")
gui.Parent = player.PlayerGui

-- Main Frame (the textbox)
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 200)
frame.Position = UDim2.new(0.5, -200, 0.5, -100)
frame.BackgroundColor3 = Color3.fromRGB(38, 38, 51)
frame.BorderColor3 = Color3.fromRGB(102, 102, 204)
frame.BorderSizePixel = 2
frame.Parent = gui

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
