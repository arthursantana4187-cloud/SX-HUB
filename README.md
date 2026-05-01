local PlaceId = game.PlaceId
local TargetPlaceId = 115054138215106
if PlaceId ~= TargetPlaceId then
    game.Players.LocalPlayer:Kick("SX HUB: Este script só funciona no Sintonia RP!")
    return
end

local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()
local Window = OrionLib:MakeWindow({Name = "SX HUB | by SX", HidePremium = false, SaveConfig = true, ConfigFolder = "SX_Hub_Config"})

-- Informações do Usuário (Canto superior esquerdo)
local player = game.Players.LocalPlayer
local userId = player.UserId
local thumbType = Enum.ThumbnailType.HeadShot
local thumbSize = Enum.ThumbnailSize.Size420x420
local content, isReady = game.Players:GetUserThumbnailAsync(userId, thumbType, thumbSize)

OrionLib:MakeNotification({
    Name = "Bem-vindo, " .. player.Name,
    Content = "SX HUB carregado com sucesso!",
    Image = content,
    Time = 5
})

--- ANTI-CHEAT BYPASS (Silent Method) ---
local mt = getrawmetatable(game)
setreadonly(mt, false)
local old = mt.__namecall
mt.__namecall = newcclosure(function(self, ...)
    local method = getnamecallmethod()
    if method == "Kick" or method == "kick" then
        return nil
    end
    return old(self, ...)
end)

--- ABAS DO PAINEL ---

-- Aba Combat
local CombatTab = Window:MakeTab({
    Name = "Combat",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

CombatTab:AddToggle({
    Name = "Aimbot",
    Default = false,
    Callback = function(Value)
        _G.Aimbot = Value
    end    
})

CombatTab:AddToggle({
    Name = "Silent Aim",
    Default = false,
    Callback = function(Value)
        _G.SilentAim = Value
    end    
})

CombatTab:AddToggle({
    Name = "Godmode",
    Default = false,
    Callback = function(Value)
        if Value then
            game.Players.LocalPlayer.Character.Humanoid.MaxHealth = math.huge
            game.Players.LocalPlayer.Character.Humanoid.Health = math.huge
        else
            game.Players.LocalPlayer.Character.Humanoid.MaxHealth = 100
        end
    end    
})

CombatTab:AddSlider({
    Name = "FOV Radius",
    Min = 0,
    Max = 500,
    Default = 100,
    Color = Color3.fromRGB(255,255,255),
    Increment = 1,
    ValueName = "Pixels",
    Callback = function(Value)
        _G.FOVSize = Value
    end    
})

-- Aba Visual
local VisualTab = Window:MakeTab({
    Name = "Visual",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

VisualTab:AddToggle({
    Name = "ESP Caixa (Box)",
    Default = false,
    Callback = function(Value)
        -- Lógica de ESP Box aqui
    end    
})

VisualTab:AddToggle({
    Name = "ESP Linhas (Tracers)",
    Default = false,
    Callback = function(Value)
        -- Lógica de Tracers aqui
    end    
})

VisualTab:AddToggle({
    Name = "ESP Vida (Health)",
    Default = false,
    Callback = function(Value)
        -- Lógica de Health Bar aqui
    end    
})

OrionLib:Init()
