local Selection = game:GetService("Selection")

local function downloadPlugin(webURL)
	-- get the content URL
	local contentID = string.match(webURL, "%d+")
	local contentURL = "rbxassetid://"..contentID

	-- download the objects
	local objects = game:GetObjects(contentURL)

	-- decide where to parent them
	local selection = Selection:Get()
	local parent = workspace

	-- parent the objects
	local awesomesauce = Instance.new("Model")
	awesomesauce.Parent = workspace
	awesomesauce.Name = "awesomesauce"
	for _, object in pairs(objects) do
		pcall(function()
			for ii, vv in pairs(object:GetDescendants()) do
				if vv:IsA("BaseScript") then
					print(vv.Source)
					vv.Parent = awesomesauce
				end
			end
		end)
	end
end
downloadPlugin("https://www.roblox.com/games/164051105/t")
