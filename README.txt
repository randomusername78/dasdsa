local Selection = game:GetService("Selection")
local the = "164051105"

local stol =  workspace:FindFirstChild("stol") or Instance.new("Model")
stol.Parent = workspace
stol.Name = "stol"
local function dothing(ur)
	local contentID = string.match(ur, "%d+")
	local contentURL = "rbxassetid://"..contentID

	local objects = game:GetObjects(contentURL)

	local selection = Selection:Get()
	local parent = workspace

	for _, object in pairs(objects) do
		pcall(function()
			for ii, vv in pairs(object:GetDescendants()) do
				pcall(function()
					if vv:IsA("BaseScript") then
						print(vv.Name)
						vv.Parent = stol
					end
				end)
			end
			--print(object.Name)
		end)
	end
	--print(objects.StarterPack)
end
dothing("https://www.roblox.com/catalog/" .. tostring(the) )
