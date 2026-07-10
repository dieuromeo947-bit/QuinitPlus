# Quinit

Quinit is an easy to use module loader for Roblox Luau. It allows you to cache and require modules on the server and client, as well as link up various helpful default functions to prevent calling multiple of the same connections.

### What changes fork?

**Simpler and better setup** _(Server or Client script)_
```
-- .SetSettings set settings for quinit
Quinit.SetSettings({
	deepSearch = 2,
	--data = ...
})

--[[
	Now you can pass containers into Quinit
	deepSearch will go through the modules to the desired parent
]]
Quinit._Init({
	script.Services -- Folder
})

Quinit._Start()
```

**Inside module**
```
local TestService = {}

-- Priority inside modulescript overrides priority set in Quinit
TestService.Priority = 1

--[[
	Now Quinit pass self into _Start arguments
	
	Example:
]]
function TestService._Start(self: Service)
	self.Variable = 1
	
	print('o')
	
	self:PrintVariable()
end

function TestService.PrintVariable(self: Service)
	print(self.Variable)
end

type Service = typeof(TestService) & {
	Variable: number
}

return TestService
```

**Template Module**
```
local Service = {}

function Service._Start()
end

function Service._OnPlayerAdded(player: Player)
end

function Service._OnCharacterAdded(character: Model, player: Player)
end

function Service._OnPlayerRemoving(player: Player)
end

function Service._OnHeartbeat()
end

return Service
```
