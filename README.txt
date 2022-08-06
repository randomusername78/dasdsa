local last = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.LookVector
game:GetService('RunService').Stepped:connect(function()

	if game.Players.LocalPlayer.Character.Humanoid.RigType == Enum.HumanoidRigType.R6 then
		game.Players.LocalPlayer.Character.Head.CanCollide = false
		game.Players.LocalPlayer.Character.Torso.CanCollide = false
		game.Players.LocalPlayer.Character["Left Leg"].CanCollide = false
		game.Players.LocalPlayer.Character["Right Leg"].CanCollide = false
	else
		if game.Players.LocalPlayer.Character.Humanoid.RigType == Enum.HumanoidRigType.R15 then
			game.Players.LocalPlayer.Character.Head.CanCollide = false
			game.Players.LocalPlayer.Character.UpperTorso.CanCollide = false
			game.Players.LocalPlayer.Character.LowerTorso.CanCollide = false
			game.Players.LocalPlayer.Character.HumanoidRootPart.CanCollide = false
		end
	end

end)
game:GetService('RunService').Heartbeat:connect(function(tim, step)
	if not game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart") then
		script:Destroy()
	end
	local m = game.Players.LocalPlayer.Character.Humanoid.MoveDirection
	if m == Vector3.new(0,0,0) then
		m = last
		
	else
		--print("men")
		--game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame.LookVector*(game.Players.LocalPlayer.Character.Humanoid.WalkSpeed*step)
		last = m
	end
	local l =  game.Players.LocalPlayer.Character.HumanoidRootPart.Position
	game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(l, l+m)  
	--game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = true
end)
for i, v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
	if v:IsA("BasePart") then
		v.CustomPhysicalProperties = PhysicalProperties.new(999, 2, 0, 100, 0)
	end
end
game.Players.LocalPlayer.Character.HumanoidRootPart.Anchored = false
local bambam = Instance.new("BodyAngularVelocity")
bambam.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
bambam.AngularVelocity = Vector3.new(0, 999999999999, 0)
bambam.MaxTorque = Vector3.new(1,1,1)*math.huge
wait(1)
