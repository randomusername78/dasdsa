
local Forces = {}
local Player = game.Players.LocalPlayer
local Target = Player.Character.Head
local started = false
function partadd(part)
	if part:IsA("BasePart" or "UnionOperation" or "Model") and part.Anchored == false and not part:IsDescendantOf(Player.Character) and part.Name == "Torso" == false and part.Name == "Head" == false and part.Name == "Right Arm" == false and part.Name == "Left Arm" == false and part.Name == "Right Leg" == false and part.Name == "Left Leg" == false and part.Name == "HumanoidRootPart" == false then
		for i,c in pairs(part:GetChildren()) do
			if c:IsA("BodyPosition") or c:IsA("BodyGyro")  or c:IsA("BodyVelocity") or c:IsA("BodyMover") then
				c:Destroy()
			end
		end
		local ForceInstance = Instance.new("BodyPosition")
		ForceInstance.Parent = part
		ForceInstance.MaxForce = Vector3.new(math.huge, math.huge, math.huge)
		ForceInstance.Position =  Target.Position or part.Position
		ForceInstance.D =800
		table.insert(Forces, ForceInstance)
	end
end

for i, v in pairs(workspace:GetDescendants()) do
	if v:IsA("BasePart") then
		partadd(v)
	end
end

game.Workspace.DescendantAdded:Connect(partadd)

local tool = Instance.new("Tool")

tool.RequiresHandle = false
tool.Name = "Selection"
tool.Parent = Player.Backpack
local selectionbox = Instance.new("SelectionBox")
selectionbox.Parent = Player.PlayerGui
selectionbox.Adornee = nil
local sethidden = sethiddenproperty or set_hidden_property or set_hidden_prop
local gethidden = gethiddenproperty or get_hidden_property or get_hidden_prop
local setsimulation = setsimulationradius or set_simulation_radius
tool.Activated:Connect(function()
	local target = Player:GetMouse().Target
	if target and target.Parent:FindFirstChildOfClass("Humanoid") then
		started = true
		Target = target.Parent.Head
		selectionbox.Adornee = target.Parent
	else
		Target = nil
		selectionbox.Adornee = nil
	end
end)
	simRadLoop = game["Run Service"].Stepped:Connect(function()
		if setsimulation then
			setsimulation(1e308, 1/0)
		elseif sethidden then
			sethidden(Player,"MaximumSimulationRadius",1/0)
			sethidden(Player,"SimulationRadius", 1e308)
		end
	end)
game:GetService("StarterGui"):SetCoreGuiEnabled(Enum.CoreGuiType.Backpack, true)

while Player.Character:FindFirstChild("Humanoid") do
	for i, v in pairs(Forces) do
		if v then
			if Target and started then
				v.Position = Target.Position
			end
		else
			table.remove(Forces, i)
		end
	end
	task.wait(.6)
end
for i, v in pairs(Forces) do
	if v then
		v:Destroy()
	end
end
simRadLoop:Disconnect()
