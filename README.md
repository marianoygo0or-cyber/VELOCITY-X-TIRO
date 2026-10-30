-- VELOCITY X V16 - CARTOLA UI
print("Carregando Velocity X...")
local P = game:GetService("Players")
local U = game:GetService("UserInputService")
local T = game:GetService("TweenService")
local R = game:GetService("RunService")
local VU = game:GetService("VirtualUser")
local lp = P.LocalPlayer
local pg = lp:WaitForChild("PlayerGui")

if pg:FindFirstChild("VX16") then pg.VX16:Destroy() end

local sg = Instance.new("ScreenGui")
sg.Name = "VX16"
sg.ResetOnSpawn = false
sg.DisplayOrder = 999
sg.Parent = pg

local function C(c,p,f) local o=Instance.new(c); for k,v in pairs(p) do o[k]=v end; o.Parent=f; return o end
local Re,Da,Pa,Ca,CaH,Tx,Su=Color3.fromRGB(255,40,60),Color3.fromRGB(12,12,15),Color3.fromRGB(18,18,22),Color3.fromRGB(26,26,32),Color3.fromRGB(35,35,45),Color3.fromRGB(255,255,255),Color3.fromRGB(140,140,150)

local CF={Speed=16,Noclip=false,ESP=false,FOV=100,Triggerbot=false,Aimbot=false,AntiLag1=false,AntiLag2=false,AntiFling=false,AntiSit=false,InfJump=false}
local lastShot,espCache=0,{}
local sPP,sMP=UDim2.new(.5,-210,.5,-130),UDim2.new(.5,-95,.1,0) -- Centralizado

-- ==========================================
-- INTERFACE PRINCIPAL
-- ==========================================
local mf=C("Frame",{Size=UDim2.fromOffset(420,260),Position=sPP,BackgroundColor3=Da,BackgroundTransparency=.05},sg)
C("UICorner",{CornerRadius=UDim.new(0,14)},mf)
C("UIStroke",{Color=Re,Thickness=1.5,Transparency=.5},mf)

local tb=C("Frame",{Size=UDim2.new(1,0,0,40),BackgroundColor3=Pa},mf)
C("UICorner",{CornerRadius=UDim.new(0,14)},tb)
C("Frame",{Size=UDim2.new(1,0,0,10),Position=UDim2.new(0,0,1,-10),BackgroundColor3=Pa},tb)
C("TextLabel",{Size=UDim2.fromOffset(150,40),Position=UDim2.fromOffset(15,0),BackgroundTransparency=1,Text="VELOCITY X",TextColor3=Re,Font=Enum.Font.GothamBlack,TextSize=18,TextXAlignment=Enum.TextXAlignment.Left},tb)
local mBtn=C("TextButton",{Size=UDim2.fromOffset(35,35),Position=UDim2.new(1,-75,0,2.5),BackgroundTransparency=1,Text="-",TextColor3=Tx,Font=Enum.Font.GothamBold,TextSize=24},tb)
local cBtn=C("TextButton",{Size=UDim2.fromOffset(35,35),Position=UDim2.new(1,-40,0,2.5),BackgroundTransparency=1,Text="X",TextColor3=Re,Font=Enum.Font.GothamBold,TextSize=20},tb)

local sb=C("Frame",{Size=UDim2.new(0,110,1,-55),Position=UDim2.fromOffset(10,50),BackgroundColor3=Pa,BackgroundTransparency=.4},mf)
C("UICorner",{CornerRadius=UDim.new(0,10)},sb)
local ti=C("Frame",{Size=UDim2.fromOffset(4,18),Position=UDim2.fromOffset(5,14),BackgroundColor3=Re},sb)
C("UICorner",{CornerRadius=UDim.new(1,0)},ti)
local ca=C("Frame",{Size=UDim2.new(1,-130,1,-55),Position=UDim2.fromOffset(125,50),BackgroundColor3=Pa,BackgroundTransparency=.3,ClipsDescendants=true},mf)
C("UICorner",{CornerRadius=UDim.new(0,10)},ca)

local tabBtns,tw={},{}
local function MkTab(t,y)
    local b=C("TextButton",{Size=UDim2.new(1,-15,0,26),Position=UDim2.fromOffset(12,y),BackgroundTransparency=1,Text=t,TextColor3=Su,Font=Enum.Font.GothamBold,TextSize=11},sb)
    table.insert(tabBtns,{btn=b,y=y}); return b
end
local t0,t1,t2,t3,t4=MkTab("PRINCIPAL",8),MkTab("COMBATE",38),MkTab("VISUAL",68),MkTab("BYPASS",98),MkTab("ANTI-XIT",128)

local function SetT(act,y)
    for _,v in ipairs(tabBtns) do
        if tw[v.btn] then tw[v.btn]:Cancel() end
        tw[v.btn]=T:Create(v.btn,TweenInfo.new(.2),{TextColor3=(v.btn==act) and Tx or Su}); tw[v.btn]:Play()
    end
    T:Create(ti,TweenInfo.new(.3,Enum.EasingStyle.Quart),{Position=UDim2.fromOffset(5,y+5)}):Play()
end

local aS=nil
U.InputChanged:Connect(function(i) if aS and (i.UserInputType==Enum.UserInputType.MouseMovement or i.UserInputType==Enum.UserInputType.Touch) then local sx=math.clamp((i.Position.X-aS.b.AbsolutePosition.X)/aS.b.AbsoluteSize.X,0,1); aS.f.Size=UDim2.new(sx,0,1,0); local v=math.floor(aS.m+(aS.x-aS.m)*sx); aS.l.Text=aS.t..": "..v; aS.c(v) end end)
U.InputEnded:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then aS=nil end end)

local function Toggle(p,t,desc,y,cb,def)
    local f=C("Frame",{Size=UDim2.new(1,-10,0,44),Position=UDim2.fromOffset(5,y),BackgroundColor3=Ca,BackgroundTransparency=.1},p)
    C("UICorner",{CornerRadius=UDim.new(0,8)},f)
    C("UIStroke",{Color=Color3.fromRGB(50,50,60),Thickness=1,Transparency=.5},f)
    C("TextLabel",{Size=UDim2.new(1,-50,0,18),Position=UDim2.fromOffset(10,5),BackgroundTransparency=1,Text=t,TextColor3=Tx,Font=Enum.Font.GothamBold,TextSize=12,TextXAlignment=Enum.TextXAlignment.Left},f)
    C("TextLabel",{Size=UDim2.new(1,-50,0,14),Position=UDim2.fromOffset(10,22),BackgroundTransparency=1,Text=desc,TextColor3=Su,Font=Enum.Font.Gotham,TextSize=9,TextXAlignment=Enum.TextXAlignment.Left},f)
    local s=C("TextButton",{Size=UDim2.fromOffset(36,18),Position=UDim2.new(1,-46,.5,-9),BackgroundColor3=Color3.fromRGB(45,45,50),Text=""},f)
    C("UICorner",{CornerRadius=UDim.new(1,0)},s)
    local c=C("Frame",{Size=UDim2.fromOffset(14,14),Position=UDim2.new(0,2,.5,-7),BackgroundColor3=Tx},s)
    C("UICorner",{CornerRadius=UDim.new(1,0)},c)
    local o=def or false
    if o then s.BackgroundColor3=Re; c.Position=UDim2.new(1,-16,.5,-7) end
    cb(o)
    s.MouseButton1Click:Connect(function()
        o=not o
        T:Create(s,TweenInfo.new(.2),{BackgroundColor3=o and Re or Color3.fromRGB(45,45,50)}):Play()
        T:Create(c,TweenInfo.new(.2,Enum.EasingStyle.Back),{Position=o and UDim2.new(1,-16,.5,-7) or UDim2.new(0,2,.5,-7)}):Play()
        cb(o)
    end)
end

local function Slider(p,t,y,mn,mx,df,cb)
    local f=C("Frame",{Size=UDim2.new(1,-10,0,44),Position=UDim2.fromOffset(5,y),BackgroundColor3=Ca,BackgroundTransparency=.1},p)
    C("UICorner",{CornerRadius=UDim.new(0,8)},f)
    C("UIStroke",{Color=Color3.fromRGB(50,50,60),Thickness=1,Transparency=.5},f)
    local l=C("TextLabel",{Size=UDim2.new(1,0,0,18),Position=UDim2.fromOffset(10,5),BackgroundTransparency=1,Text=t..": "..df,TextColor3=Tx,Font=Enum.Font.GothamBold,TextSize=12,TextXAlignment=Enum.TextXAlignment.Left},f)
    local b=C("Frame",{Size=UDim2.new(1,-20,0,4),Position=UDim2.fromOffset(10,28),BackgroundColor3=Color3.fromRGB(45,45,50),ClipsDescendants=true},f)
    C("UICorner",{CornerRadius=UDim.new(1,0)},b)
    local fl=C("Frame",{Size=UDim2.new((df-mn)/(mx-mn),0,1,0),BackgroundColor3=Re},b)
    C("UICorner",{CornerRadius=UDim.new(1,0)},fl)
    b.InputBegan:Connect(function(i) if i.UserInputType==Enum.UserInputType.MouseButton1 or i.UserInputType==Enum.UserInputType.Touch then aS={b=b,f=fl,l=l,m=mn,x=mx,t=t,c=cb}; local sx=math.clamp((i.Position.X-b.AbsolutePosition.X)/b.AbsoluteSize.X,0,1); fl.Size=UDim2.new(sx,0,1,0); local v=math.floor(mn+(mx-mn)*sx); l.Text=t..": "..v; cb(v) end end)
end

local function Panel(vis) return C("ScrollingFrame",{Size=UDim2.new(1,0,1,0),BackgroundTransparency=1,Visible=vis,ScrollBarThickness=2,CanvasSize=UDim2.fromOffset(0,300)},ca) end
local p0,p1,p2,p3,p4=Panel(true),Panel(false),Panel(false),Panel(false),Panel(false)

local lagThread
local function ToggleAntiLag1(s)
    CF.AntiLag1=s
    if s then if not lagThread then lagThread=task.spawn(function() while CF.AntiLag1 do for _,v in pairs(workspace:GetDescendants()) do if (v:IsA("ParticleEmitter") or v:IsA("Fire") or v:IsA("Smoke")) and v.Enabled then v.Enabled=false end end task.wait(1) end end) end
    else if lagThread then task.cancel(lagThread); lagThread=nil end end
end

Slider(p0,"VELOCIDADE",5,16,40,16,function(v) CF.Speed=v end)
Toggle(p0,"NOCLIP","Atravessa paredes",55,function(v) CF.Noclip=v; if not v and lp.Character then for _,p in pairs(lp.Character:GetDescendants()) do if p:IsA("BasePart") then p.CanCollide=true end end end end)
Toggle(p0,"ANTI-LAG V1 (FX)","Remove partículas",105,ToggleAntiLag1)
Toggle(p0,"ANTI-LAG V2 (LIGHT)","Desliga sombras",155,function(v) CF.AntiLag2=v; if v then pcall(function() settings().Rendering.QualityLevel=1 end); game.Lighting.GlobalShadows=false; game.Lighting.FogEnd=1e5 else pcall(function() settings().Rendering.QualityLevel=21 end); game.Lighting.GlobalShadows=true; game.Lighting.FogEnd=1e4 end end)

Toggle(p1,"TRIGGERBOT","Atira automaticamente",5,function(v) CF.Triggerbot=v end)
Toggle(p1,"AIMBOT (BALANCED)","Mira equilibrada dt*8",55,function(v) CF.Aimbot=v end)
Slider(p1,"FOV (Raio de Mira)",105,70,150,100,function(v) CF.FOV=v end)

Toggle(p2,"ESP PLAYERS","Destaca jogadores",5,function(v) CF.ESP=v end)

Toggle(p3,"ANTI-AFK","Evita kick",5,function(v) end,true)
Toggle(p3,"ESCONDER AO MORRER","Some ao morrer",55,function(v) end,true)
Toggle(p3,"PULO INFINITO","Pula infinitamente",105,function(v) CF.InfJump=v end)
Toggle(p3,"FPS UNLOCKER","Remove limite de FPS",155,function(v) if v then pcall(function() setfpscap(240) end) else pcall(function() setfpscap(60) end) end end)

Toggle(p4,"ANTI FLING","Não é jogado pro céu",5,function(v) CF.AntiFling=v end)
Toggle(p4,"ANTI SIT","Não senta forçado",55,function(v) CF.AntiSit=v end)

local panels={p0,p1,p2,p3,p4}
local tabs={t0,t1,t2,t3,t4}
for i,t in ipairs(tabs) do t.MouseButton1Click:Connect(function() SetT(t,8+30*(i-1)); for j,p in ipairs(panels) do p.Visible=(i==j) end end) end
SetT(t0,8)

local cG=C("Frame",{Size=UDim2.fromOffset(250,140),Position=UDim2.new(.5,-125,.5,-70),BackgroundColor3=Da,Visible=false},sg)
C("UICorner",{CornerRadius=UDim.new(0,12)},cG)
C("UIStroke",{Color=Re,Thickness=1},cG)
C("TextLabel",{Size=UDim2.new(1,-20,0,50),Position=UDim2.fromOffset(10,10),BackgroundTransparency=1,Text="FECHAR O VELOCITY X?",TextColor3=Tx,Font=Enum.Font.GothamBold,TextSize=13,TextWrapped=true,TextXAlignment=Enum.TextXAlignment.Center},cG)
local yB=C("TextButton",{Size=UDim2.fromOffset(90,30),Position=UDim2.new(0,15,1,-40),BackgroundTransparency=1,Text="SIM",TextColor3=Re,Font=Enum.Font.GothamBold,TextSize=14},cG)
local nB=C("TextButton",{Size=UDim2.fromOffset(90,30),Position=UDim2.new(1,-105,1,-40),BackgroundTransparency=1,Text="NÃO",TextColor3=Tx,Font=Enum.Font.GothamBold,TextSize=14},cG)
cBtn.MouseButton1Click:Connect(function() cG.Visible=true end)
nB.MouseButton1Click:Connect(function() cG.Visible=false end)
yB.MouseButton1Click:Connect(function() sg:Destroy() end)

-- ==========================================
-- MINIBAR REPAGINADA (Estilo Cartola Hub)
-- ==========================================
local mb = C("TextButton", {
    Size = UDim2.fromOffset(190, 40), 
    Position = UDim2.new(.5, -95, .1, 0), 
    BackgroundColor3 = Color3.fromRGB(15,15,20), 
    BackgroundTransparency = 0.1, 
    Text = "", 
    AutoButtonColor = false, 
    Visible = false
}, sg)

-- Formato de pílula e Borda
C("UICorner", {CornerRadius = UDim.new(1, 0)}, mb)
C("UIStroke", {Color = Re, Thickness = 1.5, Transparency = 0.2}, mb)
C("UIGradient", {Color = ColorSequence.new(Color3.fromRGB(30,30,40), Color3.fromRGB(15,15,20)), Rotation = 90}, mb)

-- Texto "VELOCITY X" alinhado à esquerda
C("TextLabel", {
    Size = UDim2.new(1, -50, 1, 0), 
    Position = UDim2.fromOffset(15, 0), 
    BackgroundTransparency = 1, 
    Text = "VELOCITY X", 
    TextColor3 = Tx, 
    Font = Enum.Font.GothamBlack, 
    TextSize = 14, 
    TextXAlignment = Enum.TextXAlignment.Left
}, mb)

-- Ícone "+" alinhado à direita
C("TextLabel", {
    Size = UDim2.fromOffset(40, 40), 
    Position = UDim2.new(1, -45, 0, 0), 
    BackgroundTransparency = 1, 
    Text = "+", 
    TextColor3 = Re, 
    Font = Enum.Font.GothamBlack, 
    TextSize = 20, 
    TextXAlignment = Enum.TextXAlignment.Center
}, mb)

-- Animação Minimizar
mBtn.MouseButton1Click:Connect(function()
    sPP=mf.Position
    T:Create(mf,TweenInfo.new(.4,Enum.EasingStyle.Quart,Enum.EasingDirection.In),{Position=UDim2.new(sPP.X.Scale,sPP.X.Offset,1.5,0)}):Play()
    task.wait(.4)
    mf.Visible=false
    mb.Position=UDim2.new(sMP.X.Scale,sMP.X.Offset,-.5,0); mb.Visible=true
    T:Create(mb,TweenInfo.new(.4,Enum.EasingStyle.Back,Enum.EasingDirection.Out),{Position=sMP}):Play()
end)

-- Lógica Anti-Toque Acidental na MiniBar
local miniDragStart, miniDragging = nil, false
mb.InputBegan:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseButton1 or inp.UserInputType==Enum.UserInputType.Touch then miniDragStart = inp.Position; miniDragging = false end end)
U.InputChanged:Connect(function(inp) if miniDragStart and (inp.UserInputType==Enum.UserInputType.MouseMovement or inp.UserInputType==Enum.UserInputType.Touch) then if (inp.Position - miniDragStart).Magnitude > 5 then miniDragging = true end end end)
U.InputEnded:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseButton1 or inp.UserInputType==Enum.UserInputType.Touch then task.wait(0.1); miniDragStart = nil end end)

mb.MouseButton1Click:Connect(function()
    if miniDragging then miniDragging = false return end
    mb.Visible=false
    mf.Position=UDim2.new(sPP.X.Scale,sPP.X.Offset,1.5,0); mf.Visible=true
    T:Create(mf,TweenInfo.new(.6,Enum.EasingStyle.Bounce,Enum.EasingDirection.Out),{Position=sPP}):Play()
end)

-- Drag
local function Drag(f,area,isMini)
    local d,i,s,p=false,nil,nil,nil
    area.InputBegan:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseButton1 or inp.UserInputType==Enum.UserInputType.Touch then d=true; s=inp.Position; p=f.Position end end)
    area.InputChanged:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseMovement or inp.UserInputType==Enum.UserInputType.Touch then i=inp end end)
    U.InputChanged:Connect(function(inp) if inp==i and d then local dl=inp.Position-s; local np=UDim2.new(p.X.Scale,p.X.Offset+dl.X,p.Y.Scale,p.Y.Offset+dl.Y); f.Position=np; if isMini then sMP=np else sPP=np end end end)
    U.InputEnded:Connect(function(inp) if inp.UserInputType==Enum.UserInputType.MouseButton1 or inp.UserInputType==Enum.UserInputType.Touch then d=false end end)
end
Drag(mf,tb,false); Drag(mb,mb,true)

-- ==========================================
-- LOOPS
-- ==========================================
lp.Idled:Connect(function() pcall(function() VU:CaptureController(); VU:ClickButton2(Vector2.new()) end) end)
U.JumpRequest:Connect(function() if CF.InfJump then pcall(function() local h=lp.Character and lp.Character:FindFirstChildOfClass("Humanoid"); if h and h.Health>0 then h:ChangeState(Enum.HumanoidStateType.Jumping) end end) end end)

R.Stepped:Connect(function()
    if not mf.Parent then return end
    pcall(function()
        local c=lp.Character; if not c then return end
        if CF.Noclip then
            local h=c:FindFirstChildOfClass("Humanoid")
            local cc=h and h.MoveDirection.Magnitude>0
            for _,v in pairs(c:GetDescendants()) do if v:IsA("BasePart") then v.CanCollide=not cc end end
        end
    end)
end)

R.Heartbeat:Connect(function()
    if not mf.Parent then return end
    pcall(function()
        local c=lp.Character; local h=c and c:FindFirstChild("Humanoid"); if not c or not h then return end
        if h.Health>0 then h.WalkSpeed=CF.Speed; h.JumpPower=50 end
        if CF.AntiFling then local hrp=c:FindFirstChild("HumanoidRootPart"); if hrp and (hrp.AssemblyAngularVelocity.Magnitude>10 or hrp.AssemblyLinearVelocity.Magnitude>100) then hrp.AssemblyAngularVelocity=Vector3.new(0,0,0); hrp.AssemblyLinearVelocity=Vector3.new(0,hrp.AssemblyLinearVelocity.Y,0) end end
        if h.WalkSpeed>40 then h.WalkSpeed=40 end
    end)
end)

local rp=RaycastParams.new()
pcall(function() rp.FilterType=Enum.RaycastFilterType.Exclude end)
pcall(function() rp.FilterType=Enum.RaycastFilterType.Blacklist end)

R.RenderStepped:Connect(function(dt)
    if not mf.Parent then return end
    pcall(function()
        local c=lp.Character; if not c or not c:FindFirstChild("Head") then return end
        local cam=workspace.CurrentCamera; if not cam then return end
        rp.FilterDescendantsInstances={c}
        if CF.FOV~=cam.FieldOfView then cam.FieldOfView=CF.FOV end
        local bt,ld=nil,CF.FOV
        for _,p in pairs(P:GetPlayers()) do
            if p~=lp and p.Character then
                local h=p.Character:FindFirstChild("Humanoid"); local hp=p.Character:FindFirstChild("Head")
                if h and h.Health>0 and hp then
                    local pos,on=cam:WorldToViewportPoint(hp.Position)
                    if on then
                        local d=(Vector2.new(pos.X,pos.Y)-Vector2.new(cam.ViewportSize.X/2,cam.ViewportSize.Y/2)).Magnitude
                        if d<ld then
                            local rh=workspace:Raycast(cam.CFrame.Position,(hp.Position-cam.CFrame.Position).Unit*1000,rp)
                            if rh and (rh.Instance:IsDescendantOf(p.Character) or rh.Instance.Parent==p.Character) then ld=d; bt=p end
                        end
                    end
                end
            end
        end
        if CF.Aimbot and bt and bt.Character then
            local hp=bt.Character:FindFirstChild("Head")
            if hp then cam.CFrame=cam.CFrame:Lerp(CFrame.new(cam.CFrame.Position,hp.Position),math.clamp(dt*8,0,1)) end
        end
        if CF.Triggerbot and bt and ld<60 and (os.clock()-lastShot>.15) then
            pcall(function() VU:CaptureController(); VU:ClickButton1(Vector2.new()) end)
            lastShot=os.clock()
        end
    end)
end)

task.spawn(function()
    while mf.Parent and task.wait(.2) do
        pcall(function()
            for _,p in pairs(P:GetPlayers()) do
                if p~=lp and p.Character then
                    local ph=p.Character:FindFirstChild("Head")
                    if ph and p.Character:FindFirstChild("Humanoid") then
                        if CF.ESP then
                            if not espCache[p.Name] or espCache[p.Name].Adornee~=p.Character then
                                if espCache[p.Name] then espCache[p.Name]:Destroy() end
                                local hl=Instance.new("Highlight",p.Character); hl.Adornee=p.Character; hl.FillColor=Re; hl.DepthMode=Enum.HighlightDepthMode.AlwaysOnTop; espCache[p.Name]=hl
                            end
                        elseif espCache[p.Name] then espCache[p.Name]:Destroy(); espCache[p.Name]=nil end
                    end
                end
            end
            for n,hl in pairs(espCache) do if not P:FindFirstChild(n) then hl:Destroy(); espCache[n]=nil end end
        end)
    end
end)

-- Animação de Entrada Suave (Agora sim, no painel)
mf.Position = UDim2.new(sPP.X.Scale, sPP.X.Offset, 1.5, 0)
T:Create(mf, TweenInfo.new(0.8, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {Position=sPP}):Play()

print("Velocity X V16 Carregado com Sucesso!")
