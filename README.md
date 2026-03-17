local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UICorner = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local SubTitle = Instance.new("TextLabel")
local Button1 = Instance.new("TextButton") -- V4
local Button2 = Instance.new("TextButton") -- V5 Lightweight
local UIStroke = Instance.new("UIStroke")

-- [ Setup ScreenGui ] --
ScreenGui.Name = "GTL_Ultimate_Hub"
ScreenGui.Parent = game.CoreGui
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- [ Main Frame ] --
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Position = UDim2.new(0.5, -140, 0.4, -110)
MainFrame.Size = UDim2.new(0, 280, 0, 220)
MainFrame.Active = true
MainFrame.Draggable = true 

UICorner.CornerRadius = UDim.new(0, 15)
UICorner.Parent = MainFrame

UIStroke.Color = Color3.fromRGB(0, 255, 150) 
UIStroke.Thickness = 2
UIStroke.Parent = MainFrame

-- [ Title & Header ] --
Title.Name = "Title"
Title.Parent = MainFrame
Title.BackgroundTransparency = 1.0
Title.Position = UDim2.new(0, 0, 0.05, 0)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.Font = Enum.Font.GothamBold
Title.Text = "GTL OPTIMIZE HUB"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18.0

SubTitle.Name = "SubTitle"
SubTitle.Parent = MainFrame
SubTitle.BackgroundTransparency = 1.0
SubTitle.Position = UDim2.new(0, 0, 0.18, 0)
SubTitle.Size = UDim2.new(1, 0, 0, 20)
SubTitle.Font = Enum.Font.Gotham
SubTitle.Text = "ระบบจะปิด UI อัตโนมัติหลังรัน"
SubTitle.TextColor3 = Color3.fromRGB(150, 150, 150)
SubTitle.TextSize = 11.0

-- [ Button Function ] --
local function CreateButton(btn, text, pos, color)
    btn.Parent = MainFrame
    btn.BackgroundColor3 = color
    btn.Position = pos
    btn.Size = UDim2.new(0.9, 0, 0, 45)
    btn.Font = Enum.Font.GothamBold
    btn.Text = text
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.TextSize = 13.0
    
    local bCorner = Instance.new("UICorner")
    bCorner.CornerRadius = UDim.new(0, 10)
    bCorner.Parent = btn
end

CreateButton(Button1, "V4 แก้ลื่นแบบมาตรฐาน (แนะนำ)", UDim2.new(0.05, 0, 0.35, 0), Color3.fromRGB(0, 100, 200))
CreateButton(Button2, "แก้แล็ค V5 ลื่นสุดๆ (Lightweight)", UDim2.new(0.05, 0, 0.62, 0), Color3.fromRGB(180, 0, 40))

-----------------------------------------------------------
-- [ V4 Logic: Standard ] --
-----------------------------------------------------------
Button1.MouseButton1Click:Connect(function()
    local Lighting = game:GetService("Lighting")
    if setfpscap then setfpscap(999) end
    for _, v in pairs(workspace:GetDescendants()) do
        if v:IsA("BasePart") then v.Material = Enum.Material.Plastic v.CastShadow = false end
        if v:IsA("Decal") or v:IsA("Texture") then v:Destroy() end
    end
    
    task.wait(0.1)
    ScreenGui:Destroy()
end)

-----------------------------------------------------------
-- [ V5 Logic: LIGHTWEIGHT OPTIMIZER ] --
-----------------------------------------------------------
Button2.MouseButton1Click:Connect(function()
    -- สคริปต์ V5 ใหม่ที่คุณส่งมา
    local StarterGui = game:GetService("StarterGui")
    local Lighting = game:GetService("Lighting")
    local Terrain = workspace:FindFirstChildOfClass("Terrain")
    local Player = game.Players.LocalPlayer

    -- 1. แจ้งเตือน
    StarterGui:SetCore("SendNotification", {
        Title = "GTL_GamerTH";
        Text = "สคริปต์แก้แลค (ฉบับเน้นลื่น) ทำงานแล้ว!";
        Duration = 5;
    })

    -- 2. ฟังก์ชัน Optimize (รันรอบเดียว)
    task.spawn(function()
        -- ปรับปรุงวัตถุในแมพ
        for _, v in pairs(workspace:GetDescendants()) do
            if v:IsA("BasePart") then
                v.Material = Enum.Material.Plastic
                v.CastShadow = false
                v.Reflectance = 0
                if v:IsA("MeshPart") then
                    v.RenderFidelity = Enum.RenderFidelity.Performance
                    v.CollisionFidelity = Enum.CollisionFidelity.Box
                end
            elseif v:IsA("Decal") or v:IsA("Texture") then
                v:Destroy()
            elseif v:IsA("ParticleEmitter") or v:IsA("Trail") or v:IsA("Fire") or v:IsA("Smoke") or v:IsA("Sparkles") then
                v.Enabled = false
            end
        end

        -- ปรับปรุง Terrain
        if Terrain then
            Terrain.Decoration = false
            Terrain.WaterWaveSize = 0
            Terrain.WaterWaveSpeed = 0
            Terrain.WaterReflectance = 0
            Terrain.WaterTransparency = 0
        end

        -- ลบเครื่องประดับผู้เล่นคนอื่น (รันรอบเดียว)
        for _, otherPlayer in pairs(game.Players:GetPlayers()) do
            if otherPlayer ~= Player and otherPlayer.Character then
                for _, item in pairs(otherPlayer.Character:GetChildren()) do
                    if item:IsA("Accessory") or item:IsA("Shirt") or item:IsA("Pants") then
                        item:Destroy()
                    end
                end
            end
        end
    end)

    -- 3. ปรับแต่งแสง (รันรอบเดียว)
    Lighting.GlobalShadows = false
    Lighting.FogEnd = 200
    Lighting.FogStart = 0
    Lighting.Brightness = 2
    Lighting.ClockTime = 14

    for _, effect in pairs(Lighting:GetChildren()) do
        if effect:IsA("PostProcessEffect") or effect:IsA("BloomEffect") or effect:IsA("SunRaysEffect") or effect:IsA("BlurEffect") then
            effect.Enabled = false
        end
    end

    -- 4. ตั้งค่าระบบภายใน
    settings().Rendering.QualityLevel = 1
    settings().Network.IncomingReplicationLag = -1
    if setfpscap then
        setfpscap(999)
    end

    -- 5. ปิด UI ทันที
    task.wait(0.1)
    ScreenGui:Destroy()
    print("GTL_GamerTH: V5 Lightweight Enabled & UI Closed")
end)
