
local Player = game.Players.LocalPlayer
task.wait(1)
function rm()
	local Character = Player.Character
	for i,v in pairs(Character:GetDescendants()) do
		if v:IsA("BasePart") then
			if v.Name == "Handle" or v.Name == "Head" then
				if Character.Head:FindFirstChild("OriginalSize") then
					Character.Head.OriginalSize:Destroy()
				end
			else
				for i,cav in pairs(v:GetDescendants()) do
					if cav:IsA("Attachment") then
						if cav:FindFirstChild("OriginalPosition") then
							cav.OriginalPosition:Destroy()  
						end
					end
				end
				if v:FindFirstChild("OriginalSize") then
					v:FindFirstChild("OriginalSize"):Destroy()
					if v:FindFirstChild("AvatarPartScaleType") then
						v:FindFirstChild("AvatarPartScaleType"):Destroy()
					end
				end
			end
		end
	end
end
local sizers ={}
local Config = {
	DemeshTools = false,
	RemoveTouchInterest = false,
	CustomRightGripWeld = true
}

function GodMode()
	local Players = game:GetService("Players")

	local Player = Players.LocalPlayer
	local Character = Player.Character


	local ch = Player.Character
	local prt=Instance.new("Model")
	prt.Parent = Player.Character
	local z1 = Instance.new("Part")
	z1.Name="Torso"
	z1.CanCollide = false
	z1.Anchored = true
	local z2 = Instance.new("Part")
	z2.Name="Head"
	z2.Parent = prt
	z2.Anchored = true
	z2.CanCollide = false
	local z3 =Instance.new("Humanoid")
	z3.Name="Humanoid"
	z3.Parent = prt
	z1.Position = Vector3.new(0,9999,0)
	Player.Character=prt
	wait(3)
	Player.Character=ch
	wait(2)
	local Hum = Instance.new("Humanoid")

	Hum.Parent = Player.Character
	local root =  Player.Character.HumanoidRootPart
	for i,v in pairs(Character:GetChildren()) do
		if v:IsA("Humanoid") then
			v:SetStateEnabled(Enum.HumanoidStateType.Dead, false)
			v.BreakJointsOnDeath = false
		end
	end
	wait(1)
	Hum:Destroy()
end
--GodMode()
local Player = game.Players.LocalPlayer
local Character = Player.Character
local Humanoid = Character:FindFirstChildOfClass("Humanoid")

Humanoid:UnequipTools()
local RightArm = Character:FindFirstChild("Right Arm") or Character:FindFirstChild("RightHand")

local Humanoid = Character:FindFirstChildWhichIsA("Humanoid")
local Tool = Character:FindFirstChildWhichIsA("Tool") or Player.Backpack:FindFirstChildWhichIsA("Tool")
local FinalPath = Tool -- can change this to humanoid watever
local LocalPlayer = game:GetService("Players").LocalPlayer
local Character = LocalPlayer.Character
local Humanoid = Character:FindFirstChildOfClass("Humanoid")
local CreateCustomRightGrip = function(Tool2, CF)
	local Handle = Tool2:FindFirstChild("Handle")

	task.spawn(function()
		for _, x in next, Tool:GetDescendants() do
			if x:IsA("Mesh") or x:IsA("SpecialMesh") or x:IsA("MeshPart") then
				x:Destroy()
			end
		end
		local Speed = 1
		local Radius = 3
		local RightGrip = Instance.new("Weld")
		RightGrip.Name = "RightGrip"
		RightGrip.Part0 = RightArm
		RightGrip.Part1 = Handle
		RightGrip.C0 = CF
		RightGrip.Parent = RightArm
		Tool2.Parent = Tool
		local Attacking= false
		local Got = false
		local killthem = nil
		local saved = Character.HumanoidRootPart.CFrame
		Tool2.AncestryChanged:Connect(function(child,parent)
			if child == Tool2 and not Got then
				Got = true
				if RightGrip then
					RightGrip:Destroy()
				end
				saved = Character.HumanoidRootPart.CFrame
				killthem = parent
			end
		end)
		Tool.Activated:Connect(function()
			if not Attacking then
				Attacking= true
				task.wait(4)
				Attacking= true
			end
		end)
		RightGrip = Instance.new("Weld")
		RightGrip.Name = "RightGrip"
		RightGrip.Part0 = RightArm
		RightGrip.Part1 = Handle
		RightGrip.C0 = CF
		RightGrip.Parent = RightArm
		RightGrip.C0 = RightArm.CFrame:ToObjectSpace(CFrame.new(Character.HumanoidRootPart.Position))
		while not Got do
			Handle.Massless = true
			Handle.CanCollide = false
			if Player:GetMouse() then
				
			end
			local cf = CFrame.new(math.sin(workspace.DistributedGameTime*Speed)*Radius,math.sin(workspace.DistributedGameTime*3)*1,  math.cos(workspace.DistributedGameTime*Speed)*Radius)
			local root = Character.HumanoidRootPart
			--[[if not Attacking then
				--root.Anchored = false
				RightGrip.C0 = RightArm.CFrame:ToObjectSpace(CFrame.new(root.Position)*cf)]]
			if Attacking then
				--root.Anchored = true
				RightGrip.C0 = RightArm.CFrame:ToObjectSpace(Player:GetMouse().Hit)
				
			end
			task.wait(.2)
			RightGrip:Destroy()
			RightGrip = Instance.new("Weld")
			RightGrip.Name = "RightGrip"
			RightGrip.Part0 = RightArm
			RightGrip.Part1 = Handle
			RightGrip.C0 = CF
			RightGrip.Parent = RightArm
			RightGrip.C0 = RightArm.CFrame:ToObjectSpace(CFrame.new(Character.HumanoidRootPart.Position))

		end
		local start = workspace.DistributedGameTime
		local root = Character.HumanoidRootPart
		local theirstart = killthem:FindFirstChild("HumanoidRootPart").Position
		Character.Archivable = true
		--local fakecharacter = Character:Clone()
		--fakecharacter.PrimaryPart.Anchored = true
		--[[for i, v in pairs(fakecharacter:GetDescendants()) do
			if v:IsA("BasePart") then
				v.Anchored = true
			end
		end]]
		--fakecharacter:BreakJoints()
		--workspace.CurrentCamera.CameraSubject = fakecharacter.Humanoid
		--fakecharacter.Parent = workspace
		Character.Archivable = false
		while root and  	(theirstart- killthem:FindFirstChild("HumanoidRootPart").Position).Magnitude <= 650   and workspace.DistributedGameTime-start < 2 do
			task.wait()
			--fakecharacter:BreakJoints()
			root.RotVelocity = Vector3.new(1,1,1)*19e10
			
			--root.CFrame = CFrame.new(19e2, 19e2, 19e2)
		end
		
		print("thej")
		task.wait(.5)
		Humanoid:UnequipTools()
		root.Anchored = true
		local start = workspace.DistributedGameTime
		--fakecharacter:Destroy()
		while root and workspace.DistributedGameTime-start < .2 do
			task.wait()
			for i,v in pairs(RightArm:GetChildren()) do
				if v.Name == "RightGrip" then
					v:Destroy()
				end
			end
			root.CFrame = saved
			root.RotVelocity = Vector3.new(0,0,0)
			root.Velocity = Vector3.new()
		end
		workspace.CurrentCamera.CameraSubject = Character.Humanoid
		Humanoid:ChangeState(Enum.HumanoidStateType.GettingUp)
		root.Anchored = false
	end)
end

local Demesh = function(Tool)
	for _, x in next, Tool:GetDescendants() do
		if x:IsA("Mesh") or x:IsA("SpecialMesh") or x:IsA("MeshPart") then
			x:Destroy()
		end
	end
end

for _, x in next, Player.Backpack:GetChildren() do
	if _ > 0 and x ~= Tool then
		x.Parent = Character
		x.Parent = Tool
		x.Parent = Player.Backpack
		x.Parent = FinalPath
		if Config.CustomRightGripWeld then
			CreateCustomRightGrip(x, CFrame.new(0, -_ + 54, 0) * CFrame.Angles(math.rad(90), math.rad(90), 0))
		end
	end
end

if Config.DemeshTools then
	for _, x in next, Tool:GetChildren() do
		if x:IsA("Tool") then
			local Mesh = x:FindFirstChildWhichIsA("Mesh", true) or x:FindFirstChildWhichIsA("SpecialMesh", true) or x:FindFirstChildWhichIsA("MeshPart", true)
			if Mesh then
				Mesh:Destroy()
			end
		end
	end
end

if Config.RemoveTouchInterest then
	for _, x in next, Tool:GetChildren() do
		if x:IsA("Tool") then
			local Touch = x:FindFirstChildWhichIsA("TouchTransmitter", true)
			if Touch then
				Touch:Destroy()
			end
		end
	end
end
--Humanoid:EquipTool(Tool)
--[[for i, v in pairs(Character:GetChildren()) do
	if v:IsA("BasePart") then
		v:Destroy()
	end
end]]
--[[Tool.Parent = Character
Tool.Parent = Player.Backpack
Tool.Parent = Character]]
--[[local delaying = 0.5
rm()
wait(delaying)
local bps = Humanoid:FindFirstChild("BodyProportionScale")
bps.Parent =nil
table.insert(sizers, bps)
wait(delaying)

rm()
wait(delaying)
local bhs = Humanoid:FindFirstChild("BodyHeightScale")
bhs.Parent =nil
table.insert(sizers, bhs)
wait(delaying)

rm()
wait(delaying)
local bws = Humanoid:FindFirstChild("BodyWidthScale")
bws.Parent =nil
table.insert(sizers, bws)
wait(delaying)

rm()
wait(delaying)
local depthscale = Humanoid:FindFirstChild("BodyDepthScale")
depthscale.Parent = nil
table.insert(sizers, depthscale)
wait(delaying)

rm()
wait(delaying)
local hs = Humanoid:FindFirstChild("HeadScale")
hs.Parent = nil
table.insert(sizers, hs)
wait(delaying)]]
--[[for i, v in pairs(sizers) do
	if v then
		v.Parent = Humanoid
	end
end]]
