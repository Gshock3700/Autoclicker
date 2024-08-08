local gui = Instance.new("ScreenGui")
gui.Name = "ShockHub"
gui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 200, 0, 160)
mainFrame.Position = UDim2.new(0.5, -100, 0.5, -80)
mainFrame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = gui

local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 10)
uiCorner.Parent = mainFrame

local title = Instance.new("TextLabel")
title.Text = "ShockHub"
title.Font = Enum.Font.GothamBold
title.TextSize = 24
title.TextColor3 = Color3.new(1, 1, 1)
title.Size = UDim2.new(1, 0, 0, 30)
title.BackgroundTransparency = 1
title.Parent = mainFrame

local autoclickerToggle = Instance.new("TextButton")
autoclickerToggle.Text = "Toggle Autoclicker"
autoclickerToggle.Font = Enum.Font.Gotham
autoclickerToggle.TextSize = 14
autoclickerToggle.TextColor3 = Color3.new(1, 1, 1)
autoclickerToggle.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
autoclickerToggle.Size = UDim2.new(0.9, 0, 0, 30)
autoclickerToggle.Position = UDim2.new(0.05, 0, 0, 40)
autoclickerToggle.Parent = mainFrame

local autoclickerCircle = Instance.new("Frame")
autoclickerCircle.Size = UDim2.new(0, 20, 0, 20)
autoclickerCircle.Position = UDim2.new(1, -25, 0.5, -10)
autoclickerCircle.BackgroundColor3 = Color3.new(1, 0, 0)
autoclickerCircle.Parent = autoclickerToggle

local circleCorner = Instance.new("UICorner")
circleCorner.CornerRadius = UDim.new(1, 0)
circleCorner.Parent = autoclickerCircle

local areaToClickButton = Instance.new("TextButton")
areaToClickButton.Text = "Set Click Area"
areaToClickButton.Font = Enum.Font.Gotham
areaToClickButton.TextSize = 14
areaToClickButton.TextColor3 = Color3.new(1, 1, 1)
areaToClickButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
areaToClickButton.Size = UDim2.new(0.9, 0, 0, 30)
areaToClickButton.Position = UDim2.new(0.05, 0, 0, 80)
areaToClickButton.Parent = mainFrame

local clicksPerSecondTextBox = Instance.new("TextBox")
clicksPerSecondTextBox.PlaceholderText = "Clicks per second"
clicksPerSecondTextBox.Font = Enum.Font.Gotham
clicksPerSecondTextBox.TextSize = 14
clicksPerSecondTextBox.TextColor3 = Color3.new(1, 1, 1)
clicksPerSecondTextBox.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
clicksPerSecondTextBox.Size = UDim2.new(0.9, 0, 0, 30)
clicksPerSecondTextBox.Position = UDim2.new(0.05, 0, 0, 120)
clicksPerSecondTextBox.Parent = mainFrame

local autoclickerEnabled = false
local areaToClick = Vector2.new(0, 0)
local clicksPerSecond = 1

local function toggleAutoclicker()
    autoclickerEnabled = not autoclickerEnabled
    autoclickerCircle.BackgroundColor3 = autoclickerEnabled and Color3.new(0, 1, 0) or Color3.new(1, 0, 0)
    autoclickerToggle.Text = "Toggle Autoclicker (" .. (autoclickerEnabled and "ON" or "OFF") .. ")"
end

local function setAreaToClick()
    areaToClickButton.Text = "Click anywhere..."
    local connection
    connection = game:GetService("UserInputService").InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            areaToClick = input.Position
            areaToClickButton.Text = "Set Click Area"
            connection:Disconnect()
        end
    end)
end

local function startAutoclicker()
    while autoclickerEnabled do
        wait(1 / clicksPerSecond)
        game:GetService("VirtualUser"):Button1Down(areaToClick)
        game:GetService("VirtualUser"):Button1Up(areaToClick)
    end
end

autoclickerToggle.MouseButton1Click:Connect(toggleAutoclicker)
areaToClickButton.MouseButton1Click:Connect(setAreaToClick)

clicksPerSecondTextBox.FocusLost:Connect(function()
    local newValue = tonumber(clicksPerSecondTextBox.Text)
    if newValue and newValue > 0 then
        clicksPerSecond = newValue
    else
        clicksPerSecondTextBox.Text = tostring(clicksPerSecond)
    end
end)

spawn(startAutoclicker)
