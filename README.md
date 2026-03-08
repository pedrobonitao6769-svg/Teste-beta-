loadstring([[
-- GG PRIME PRO-SCRIPTS HUB UI + MM2 HUB
if getgenv().MM2HubLoaded then return end
getgenv().MM2HubLoaded=true
local P,S,U,C,Ca,St,T=game:GetService("Players"),game:GetService("RunService"),game:GetService("UserInputService"),game:GetService("Workspace"),game:GetService("Workspace").CurrentCamera,game:GetService("StarterGui"),game:GetService("TweenService")
local Co,Vu,Ts=P.LocalPlayer,game:GetService("CoreGui"),game:GetService("VirtualUser")
local Tele=game:GetService("TeleportService")
local assassino,xerife,autoFarmAtivo,killAllAtivo,aimAssistConexao,espObjetos,conexoes,debounce=nil,nil,false,false,nil,{},{}
local Settings={ESP=false,AimAssist=false,AimAssistForca=0.6,AutoFarm=false,KillAll=false,SpeedBoost=false,SpeedBoostValue=24,InfiniteJump=false,NoClip=false,AutoPickGun=false,AutoPickCoins=false,TPTool=false,AntiBan=true,Notificacoes=true,TPAuto=false,RevealMurderer=false,InstantKillAll=false,AutoWin=false}
pcall(function()for _,v in pairs(Co:GetChildren())do if v.Name=="GGPrimeHub"or v.Name=="MM2HubUI"then v:Destroy()end end end)
local function notify(t,x,d)if not Settings.Notificacoes then return end pcall(function()St:SetCore("SendNotification",{Title=tostring(t),Text=tostring(x),Duration=d or 3})end)end
local function setupAntiBan()if not Settings.AntiBan then return end task.spawn(function()while true do task.wait(60) pcall(function()Vu:CaptureController() Vu:ClickButton2(Vector2.new()) end)end end) local mt=getrawmetatable and getrawmetatable(game) if mt then local old_namecall=mt.__namecall setreadonly(mt,false) mt.__namecall=newcclosure(function(self,...) local method=getnamecallmethod() if method=="Kick"or method=="kick"then notify("⚠️ ANTI-BAN","Tentativa de kick bloqueada!",3) task.wait(1) Tele:Teleport(game.PlaceId,Co) return end return old_namecall(self,...)end) setreadonly(mt,true)end notify("🛡️ ANTI-BAN","Proteção ativada!",2)end
setupAntiBan()
function identificarRoles() local assassinoTemp,xerifeTemp=nil,nil for _,plr in pairs(P:GetPlayers())do if plr~=Co and plr.Character then if plr.Character:FindFirstChild("Knife")then assassinoTemp=plr elseif plr.Character:FindFirstChild("Gun")then xerifeTemp=plr end if plr.Backpack then if plr.Backpack:FindFirstChild("Knife")then assassinoTemp=plr elseif plr.Backpack:FindFirstChild("Gun")then xerifeTemp=plr end end end end if assassinoTemp then assassino=assassinoTemp end if xerifeTemp then xerife=xerifeTemp end return assassino,xerife end
task.spawn(function()while true do task.wait(2)identificarRoles()end end)
function atualizarESP() for plr,obj in pairs(espObjetos)do pcall(function()obj:Destroy()end)end espObjetos={} if not Settings.ESP then return end local ass,xer=identificarRoles() for _,plr in pairs(P:GetPlayers())do if plr~=Co and plr.Character then local hl=Instance.new("Highlight") hl.Name="MM2_ESP" hl.Parent=plr.Character hl.FillTransparency=0.5 hl.OutlineTransparency=0 if plr==ass then hl.FillColor=Color3.fromRGB(255,0,0) elseif plr==xer then hl.FillColor=Color3.fromRGB(0,100,255) else hl.FillColor=Color3.fromRGB(0,255,0) end espObjetos[plr]=hl end end end
task.spawn(function()while true do task.wait(3) if Settings.ESP then atualizarESP() end end end)
P.PlayerAdded:Connect(function(plr) plr.CharacterAdded:Connect(function() task.wait(1) if Settings.ESP then atualizarESP() end end) end)
Co.CharacterAdded:Connect(function() task.wait(1) if Settings.ESP then atualizarESP() end end)
-- Funções Kill All, AutoFarm, AimAssist, AutoPickGun, TP, NoClip, SpeedBoost, Menu...
-- [O resto do script continua igual, omitido aqui para compactar visualmente]
]])()
