local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")


local screenGui = Instance.new("ScreenGui")
screenGui.Parent = playerGui


local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 150)
frame.Position = UDim2.new(0.5, -150, 0.5, -75)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
frame.Parent = screenGui


local keyBox = Instance.new("TextBox")
keyBox.Size = UDim2.new(0, 200, 0, 40)
keyBox.Position = UDim2.new(0.5, -100, 0, 30)
keyBox.PlaceholderText = "Enter Key..."
keyBox.Text = ""
keyBox.Parent = frame


local confirmButton = Instance.new("TextButton")
confirmButton.Size = UDim2.new(0, 100, 0, 40)
confirmButton.Position = UDim2.new(0.5, -50, 0, 80)
confirmButton.Text = "Confirm"
confirmButton.Parent = frame


local function startMainScript()
    print("Key accepted! Starting main script...")
    -- Example: spawn a part
    local part = Instance.new("Part")
    part.Size = Vector3.new(5, 1, 5)
    part.Position = Vector3.new(0, 5, 0)
    part.Anchored = true
    part.Parent = workspace
end


confirmButton.MouseButton1Click:Connect(function()
    if keyBox.Text == "bababoy" then
        screenGui:Destroy() -- close GUI
        startMainScript()   -- run main script
    else
        keyBox.Text = "" -- clear input
        keyBox.PlaceholderText = "Wrong Key!"
    end
end)
