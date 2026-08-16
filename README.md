-- Create the GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Main Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 400, 0, 250)
frame.Position = UDim2.new(0.5, -200, 0.5, -125)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BackgroundTransparency = 0.9
frame.BorderSizePixel = 2
frame.BorderColor3 = Color3.fromRGB(200, 0, 0)
frame.Parent = screenGui

-- Title Label
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 30)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "Dear user,"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.TextScaled = true
title.Font = Enum.Font.SourceSansBold
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = frame

-- Main Message
local message = Instance.new("TextLabel")
message.Size = UDim2.new(1, -20, 0, 90)
message.Position = UDim2.new(0, 10, 0, 45)
message.BackgroundTransparency = 1
message.Text = "This script is outdated and it's disabled by AgnX team.\nPlease contact the owner for the script"
message.TextColor3 = Color3.fromRGB(220, 220, 220)
message.TextScaled = true
message.Font = Enum.Font.SourceSans
message.TextWrapped = true
message.Parent = frame

-- Thank You Label
local thanks = Instance.new("TextLabel")
thanks.Size = UDim2.new(1, -20, 0, 30)
thanks.Position = UDim2.new(0, 10, 0, 140)
thanks.BackgroundTransparency = 1
thanks.Text = "Thank you for listening"
thanks.TextColor3 = Color3.fromRGB(200, 200, 200)
thanks.TextScaled = true
thanks.Font = Enum.Font.SourceSansItalic
thanks.TextXAlignment = Enum.TextXAlignment.Left
thanks.Parent = frame

-- SillyAgnor Label
local signature = Instance.new("TextLabel")
signature.Size = UDim2.new(1, -20, 0, 30)
signature.Position = UDim2.new(0, 10, 0, 175)
signature.BackgroundTransparency = 1
signature.Text = "sillyAgnor"
signature.TextColor3 = Color3.fromRGB(255, 100, 100)
signature.TextScaled = true
signature.Font = Enum.Font.SourceSansBold
signature.TextXAlignment = Enum.TextXAlignment.Left
signature.Parent = frame

-- LEAVE Button
local leaveButton = Instance.new("TextButton")
leaveButton.Size = UDim2.new(0, 120, 0, 40)
leaveButton.Position = UDim2.new(0.5, -60, 1, -50)
leaveButton.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
leaveButton.BorderSizePixel = 0
leaveButton.Text = "LEAVE"
leaveButton.TextColor3 = Color3.fromRGB(255, 255, 255)
leaveButton.TextScaled = true
leaveButton.Font = Enum.Font.SourceSansBold
leaveButton.Parent = frame

-- Hover effect
leaveButton.MouseEnter:Connect(function()
    leaveButton.BackgroundColor3 = Color3.fromRGB(220, 0, 0)
end)

leaveButton.MouseLeave:Connect(function()
    leaveButton.BackgroundColor3 = Color3.fromRGB(180, 0, 0)
end)

-- Leave function
leaveButton.MouseButton1Click:Connect(function()
    game:Shutdown()
end)
