-- Auto-Harvest para Grow A Garden 2
-- Hospede este conteúdo no GitHub e use o link Raw

local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")
local Player = Players.LocalPlayer
local Character = Player.Character or Player.CharacterAdded:Wait()
local Humanoid = Character:WaitForChild("Humanoid")
local RootPart = Character:WaitForChild("HumanoidRootPart")

local function randomDelay(min, max)
return math.random(min * 100, max * 100) / 100
end

local function walkTo(position)
Humanoid:MoveTo(position)
local startTime = tick()
while (RootPart.Position - position).Magnitude > 3 do
if tick() - startTime > 10 then break end
task.wait(0.1)
end
end

print("🌱 Auto-Harvest Iniciado...")

while true do
task.wait(randomDelay(1, 2))

for _, obj in pairs(Workspace:GetDescendants()) do
if obj:IsA("BasePart") and (obj.Name:lower():find("fruit") or obj.Name:lower():find("plant")) then
if (RootPart.Position - obj.Position).Magnitude < 50 then
walkTo(obj.Position)
local clickDet = obj:FindFirstChildOfClass("ClickDetector")
local proxPrompt = obj:FindFirstChildOfClass("ProximityPrompt")

if clickDet then fireclickdetector(clickDet) end
if proxPrompt then fireproximityprompt(proxPrompt) end
end
end
end
end
