--ezan zone

Plr = {}
for i,v in pairs(game:GetService("Players"):GetChildren()) do
    table.insert(Plr,v.Name)
end


local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Cave Hub 0.5.0",
    SubTitle = "🥊Ezan Zone Boxing",
    TabWidth = 160,
    Size = UDim2.fromOffset(510, 390),
    Acrylic = false, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})
local Options = Fluent.Options

do
    Fluent:Notify({
        Title = "Notification",
        Content = "Cave Hub NO.1",
        SubContent = "", -- Optional
        Duration = 10 -- Set to nil to make the notification not disappear
    })
end

local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
     Title = "Player",
     Values = Plr,
     Multi = false,
     Default = 1,
 })

Dropdown:SetValue()

Dropdown:OnChanged(function(Value)
     Player = Value
end)


--autoequip

local weapon = {}
local weapon2 = nil


for i,v in pairs(game:GetService("Players").LocalPlayer.Backpack:GetChildren()) do
     table.insert(weapon,v.name)
end


local Dropdown = Tabs.Main:AddDropdown("Dropdown", {
     Title = "Weapon",
     Values = weapon,
     Multi = false,
     Default = 1,
 })

 Dropdown:SetValue("four")

 Dropdown:OnChanged(function(Value)
     weapon = Value
 end)


local Toggle = Tabs.Main:AddToggle("MyToggle", {Title = "Auto Equip Weapon", Default = false })

Toggle:OnChanged(function(Value)
     AutoEquip = Value
end)

Options.MyToggle:SetValue(false)


spawn(function()
     while wait() do
          if AutoEquip then
               pcall(function()
                    game.Players.LocalPlayer.Character.Humanoid:EquipTool(game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(weapon))
               end)
          end
     end
end)




local Toggle = Tabs.Main:AddToggle("MyToggle", {Title = "Auto Kill", Default = false })

Toggle:OnChanged(function(Value)
     _G.AutoKill = Value
     if _G.AutoKill then
     game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-52.4138298034668, 186.89996337890625, 495.84912109375)
     wait(2)
     while _G.AutoKill do wait()
          game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[Player].Character.HumanoidRootPart.CFrame * CFrame.new(-1,1,0.5)
          game:GetService'VirtualUser':Button1Down(Vector2.new(458, 234))
          game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Dodge_Event"):FireServer()
     end
else
     game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-52.4138298034668, 186.89996337890625, 495.84912109375)
     end
end)

Options.MyToggle:SetValue(false)


Tabs.Main:AddButton({
     Title = "Tp To SaftZone",
     Description = "",
     Callback = function()
          game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-52.4138298034668, 186.89996337890625, 495.84912109375)
     end
 })





--setting

Tabs.Settings:AddButton({
     Title = "Rejoin ",
     Description = "",
     Callback = function()
          local ts = game:GetService("TeleportService")

          local p = game:GetService("Players").LocalPlayer          
       
          
          ts:Teleport(game.PlaceId, p)
     end
})


Tabs.Settings:AddButton({
     Title = "Hop To Low Server",
     Description = "",
     Callback = function()
         local Http = game:GetService("HttpService")
         local TPS = game:GetService("TeleportService")
         local Api = "https://games.roblox.com/v1/games/"
         local _place = game.PlaceId
         local _servers = Api.._place.."/servers/Public?sortOrder=Asc&limit=100"
         function ListServers(cursor)
            local Raw = game:HttpGet(_servers .. ((cursor and "&cursor="..cursor) or ""))
            return Http:JSONDecode(Raw)
         end
         local Server, Next; repeat
            local Servers = ListServers(Next)
            Server = Servers.data[1]
            Next = Servers.nextPageCursor
         until Server  
         TPS:TeleportToPlaceInstance(_place,Server.id,game.Players.LocalPlayer)
     end
})

Tabs.Settings:AddButton({
     Title = "FpsBoots🚀",
     Description = "",
     Callback = function()
 
 local decalsyeeted = true -- Leaving this on makes games look shitty but the fps goes up by at least 20.
 local g = game
 local w = g.Workspace
 local l = g.Lighting
 local t = w.Terrain
 sethiddenproperty(l,"Technology",2)
 sethiddenproperty(t,"Decoration",false)
 t.WaterWaveSize = 0
 t.WaterWaveSpeed = 0
 t.WaterReflectance = 0
 t.WaterTransparency = 0
 l.GlobalShadows = 0
 l.FogEnd = 9e9
 l.Brightness = 0
 settings().Rendering.QualityLevel = "Level01"
 for i, v in pairs(w:GetDescendants()) do
     if v:IsA("BasePart") and not v:IsA("MeshPart") then
         v.Material = "Plastic"
         v.Reflectance = 0
     elseif (v:IsA("Decal") or v:IsA("Texture")) and decalsyeeted then
         v.Transparency = 1
     elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
         v.Lifetime = NumberRange.new(0)
     elseif v:IsA("Explosion") then
         v.BlastPressure = 1
         v.BlastRadius = 1
     elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
         v.Enabled = false
     elseif v:IsA("MeshPart") and decalsyeeted then
         v.Material = "Plastic"
         v.Reflectance = 0
         v.TextureID = 10385902758728957
     elseif v:IsA("SpecialMesh") and decalsyeeted  then
         v.TextureId=0
     elseif v:IsA("ShirtGraphic") and decalsyeeted then
         v.Graphic=0
     elseif (v:IsA("Shirt") or v:IsA("Pants")) and decalsyeeted then
         v[v.ClassName.."Template"]=0
     end
 end
 for i = 1,#l:GetChildren() do
     e=l:GetChildren()[i]
     if e:IsA("BlurEffect") or e:IsA("SunRaysEffect") or e:IsA("ColorCorrectionEffect") or e:IsA("BloomEffect") or e:IsA("DepthOfFieldEffect") then
         e.Enabled = false
     end
 end
 w.DescendantAdded:Connect(function(v)
     wait()--prevent errors and shit
    if v:IsA("BasePart") and not v:IsA("MeshPart") then
         v.Material = "Plastic"
         v.Reflectance = 0
     elseif v:IsA("Decal") or v:IsA("Texture") and decalsyeeted then
         v.Transparency = 1
     elseif v:IsA("ParticleEmitter") or v:IsA("Trail") then
         v.Lifetime = NumberRange.new(0)
     elseif v:IsA("Explosion") then
         v.BlastPressure = 1
         v.BlastRadius = 1
     elseif v:IsA("Fire") or v:IsA("SpotLight") or v:IsA("Smoke") or v:IsA("Sparkles") then
         v.Enabled = false
     elseif v:IsA("MeshPart") and decalsyeeted then
         v.Material = "Plastic"
         v.Reflectance = 0
         v.TextureID = 10385902758728957
     elseif v:IsA("SpecialMesh") and decalsyeeted then
         v.TextureId=0
     elseif v:IsA("ShirtGraphic") and decalsyeeted then
         v.ShirtGraphic=0
     elseif (v:IsA("Shirt") or v:IsA("Pants")) and decalsyeeted then
         v[v.ClassName.."Template"]=0
     end
 end)
     end
 })
 
 
 -- Addons:
 -- SaveManager (Allows you to have a configuration system)
 -- InterfaceManager (Allows you to have a interface managment system)
 
 -- Hand the library over to our managers
 SaveManager:SetLibrary(Fluent)
 InterfaceManager:SetLibrary(Fluent)
 
 -- Ignore keys that are used by ThemeManager.
 -- (we dont want configs to save themes, do we?)
 SaveManager:IgnoreThemeSettings()
 
 -- You can add indexes of elements the save manager should ignore
 SaveManager:SetIgnoreIndexes({})
 
 -- use case for doing it this way:
 -- a script hub could have themes in a global folder
 -- and game configs in a separate folder per game
 InterfaceManager:SetFolder("FluentScriptHub")
 SaveManager:SetFolder("FluentScriptHub/specific-game")
 
 InterfaceManager:BuildInterfaceSection(Tabs.Settings)
 
 Window:SelectTab(1)
 
 Fluent:Notify({
     Title = "Notification",
     Content = "The script has been loaded.",
     Duration = 5
 })
 
 -- You can use the SaveManager:LoadAutoloadConfig() to load a config
 -- which has been marked to be one that auto loads!
 SaveManager:LoadAutoloadConfig()


--uitoggle

do
     local ToggleUI = game.CoreGui:FindFirstChild("MyToggle") 
     if ToggleUI then 
     ToggleUI:Destroy() 
     end
 end
 
 local MyToggle = Instance.new("ScreenGui")
 local ImageButton = Instance.new("ImageButton")
 local UICorner = Instance.new("UICorner")
 
 --Properties:
 
 MyToggle.Name = "MyToggle"
 MyToggle.Parent = game.CoreGui
 MyToggle.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
 
 ImageButton.Parent = MyToggle
 ImageButton.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
 ImageButton.BorderColor3 = Color3.fromRGB(0, 0, 0)
 ImageButton.BorderSizePixel = 0
 ImageButton.Position = UDim2.new(0.156000003, 0, -0, 0)
 ImageButton.Size = UDim2.new(0, 50, 0, 50)
 ImageButton.Image = "rbxassetid://16731758728"
 ImageButton.MouseButton1Click:Connect(function()
 game.CoreGui:FindFirstChild("ScreenGui").Enabled = not game.CoreGui:FindFirstChild("ScreenGui").Enabled
 end)
 
 
 UICorner.CornerRadius = UDim.new(0, 10)
 UICorner.Parent = ImageButton



while true do wait()
     pcall(function()
          game.Players.LocalPlayer.Character.Humanoid:EquopTool(game:GetService("Players").LocalPlayer.Backpack)
     end)
end
