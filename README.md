local Selection = game:GetService("Selection")

local function dothing(ur)
	local contentID = string.match(ur, "%d+")
	local contentURL = "rbxassetid://"..contentID

	local objects = game:GetObjects(contentURL)

	local selection = Selection:Get()
	local parent = workspace

	for _, object in pairs(objects) do
		pcall(function()
			for ii, vv in pairs(object:GetDescendants()) do
				if vv:IsA("BaseScript") then
					vv.Parent = workspace
				end
			end
		end)
	end
end
dothing("https://www.roblox.com/catalog/8096894249/p")
