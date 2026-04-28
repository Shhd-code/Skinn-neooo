-- SH SKIN CHANGER - نسخة الـ RGB الفخمة
if game:GetService("CoreGui"):FindFirstChild("CharSwapper_RGB") then
    game:GetService("CoreGui"):FindFirstChild("CharSwapper_RGB"):Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
local MainFrame = Instance.new("Frame")
local UIStroke = Instance.new("UIStroke")
local UICorner = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local TabFrame = Instance.new("Frame")
local MeTab = Instance.new("TextButton")
local AllTab = Instance.new("TextButton")
local ScrollingFrame = Instance.new("ScrollingFrame")
local UIGridLayout = Instance.new("UIGridLayout")

-- إعدادات اللوحة
ScreenGui.Name = "CharSwapper_RGB"
ScreenGui.Parent = game:GetService("CoreGui")

MainFrame.Parent = ScreenGui
MainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
MainFrame.BackgroundTransparency = 0.2
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -150)
MainFrame.Size = UDim2.new(0, 300, 0, 320)
MainFrame.Active = true
MainFrame.Draggable = true

UICorner.CornerRadius = UDim.new(0, 15)
UICorner.Parent = MainFrame

-- حواف ملونة متغيرة (RGB) للوحة الرئيسية
UIStroke.Thickness = 2.5
UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
UIStroke.Parent = MainFrame

Title.Parent = MainFrame
Title.Size = UDim2.new(1, 0, 0, 45)
Title.Text = "SH SKIN CHANGER"
Title.TextColor3 = Color3.new(1, 1, 1)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
Title.BackgroundTransparency = 1

-- الأزرار العلوية
TabFrame.Parent = MainFrame
TabFrame.Position = UDim2.new(0.05, 0, 0.16, 0)
TabFrame.Size = UDim2.new(0.9, 0, 0, 35)
TabFrame.BackgroundTransparency = 1

local targetMode = "me" 

local function updateTabs()
    if targetMode == "me" then
        MeTab.BackgroundColor3 = Color3.fromRGB(40, 40, 40) -- خلفية داكنة للتبويب
        AllTab.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    else
        AllTab.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
        MeTab.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    end
end

MeTab.Parent = TabFrame
MeTab.Size = UDim2.new(0.48, 0, 1, 0)
MeTab.Text = "لي"
MeTab.Font = Enum.Font.GothamBold
MeTab.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", MeTab).CornerRadius = UDim.new(0, 8)

AllTab.Parent = TabFrame
AllTab.Position = UDim2.new(0.52, 0, 0, 0)
AllTab.Size = UDim2.new(0.48, 0, 1, 0)
AllTab.Text = "الكل"
AllTab.Font = Enum.Font.GothamBold
AllTab.TextColor3 = Color3.new(1, 1, 1)
Instance.new("UICorner", AllTab).CornerRadius = UDim.new(0, 8)

MeTab.MouseButton1Click:Connect(function() targetMode = "me" updateTabs() end)
AllTab.MouseButton1Click:Connect(function() targetMode = "all" updateTabs() end)
updateTabs()

-- التمرير (CanvasSize مصلح)
ScrollingFrame.Parent = MainFrame
ScrollingFrame.Position = UDim2.new(0.05, 0, 0.32, 0)
ScrollingFrame.Size = UDim2.new(0.9, 0, 0.63, 0)
ScrollingFrame.BackgroundTransparency = 1
ScrollingFrame.ScrollBarThickness = 3
ScrollingFrame.CanvasSize = UDim2.new(0, 0, 2.8, 0) 

UIGridLayout.Parent = ScrollingFrame
UIGridLayout.CellSize = UDim2.new(0, 80, 0, 80)
UIGridLayout.CellPadding = UDim2.new(0, 10, 0, 10)

local adminRemote = game:GetService("ReplicatedStorage").HDAdminHDClient.Signals.RequestCommandModification

local skinList = {
    "iipietro_gamery2k", "husen", "Rynoy5", "Im_w7x", "aeonofreason", 
    "hsenhse_8", "c00ldude452311", "Asdfgh92828", "Mariannap014", 
    "mar_gamez725", "marceelditya", "mar498187", "marcosgrand281", 
    "levi_66367", "d7ym12", "Dvhdbhdvhdb", "egoo2929",
    "REROLLINGX25", "T00orobloxYT", "msangela_2nd", "BaconBoyzHehe", 
    "YuZuKiana88", "Azetzy12345", "Ad0b0_rat", "dalandan_1123", 
    "waweck_pogi0", "ghostedhaley"
}

local function applyChar(charName)
    if targetMode == "me" then
        pcall(function() adminRemote:InvokeServer(";char me " .. charName) end)
    else
        for _, p in pairs(game:GetService("Players"):GetPlayers()) do
            pcall(function() adminRemote:InvokeServer(";char " .. p.Name .. " " .. charName) end)
            task.wait(0.8) 
        end
    end
end

for _, name in pairs(skinList) do
    task.spawn(function()
        local success, userId = pcall(function() return game:GetService("Players"):GetUserIdFromNameAsync(name) end)
        if success then
            local imgBtn = Instance.new("ImageButton")
            imgBtn.Parent = ScrollingFrame
            imgBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
            imgBtn.Image = "rbxthumb://type=AvatarHeadShot&id=" .. userId .. "&w=150&h=150"
            Instance.new("UICorner", imgBtn).CornerRadius = UDim.new(0, 10)
            imgBtn.MouseButton1Click:Connect(function() applyChar(name) end)
        end
    end)
end

-- زر الميني (👗) مع حواف RGB
local ToggleBtn = Instance.new("TextButton")
local ToggleCorner = Instance.new("UICorner")
local ToggleStroke = Instance.new("UIStroke")
local DressLabel = Instance.new("TextLabel")

ToggleBtn.Name = "MiniToggle"
ToggleBtn.Parent = ScreenGui
ToggleBtn.Size = UDim2.new(0, 45, 0, 45)
ToggleBtn.Position = UDim2.new(0.05, 0, 0.2, 0)
ToggleBtn.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
ToggleBtn.BackgroundTransparency = 0.1
ToggleBtn.Text = ""
ToggleBtn.Active = true
ToggleBtn.Draggable = true 

ToggleCorner.CornerRadius = UDim.new(1, 0)
ToggleCorner.Parent = ToggleBtn

ToggleStroke.Thickness = 2.5
ToggleStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
ToggleStroke.Parent = ToggleBtn

DressLabel.Parent = ToggleBtn
DressLabel.Size = UDim2.new(1, 0, 1, 0)
DressLabel.BackgroundTransparency = 1
DressLabel.Text = "👗"
DressLabel.TextSize = 22
DressLabel.Font = Enum.Font.GothamBold
DressLabel.TextColor3 = Color3.new(1, 1, 1)

ToggleBtn.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

-- كود تشغيل الـ RGB (تغيير الألوان بسلاسة)
task.spawn(function()
    while true do
        local hue = tick() % 5 / 5 -- يكمل دورة ألوان كل 5 ثواني
        local color = Color3.fromHSV(hue, 0.8, 1)
        UIStroke.Color = color
        ToggleStroke.Color = color
        ScrollingFrame.ScrollBarImageColor3 = color
        task.wait()
    end
end)


-- سكربت حذف إشعارات النظام المزعجة (Anti-UI Notification)
local player = game:GetService("Players").LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- دالة للبحث عن الإشعارات وحذفها
local function hideSystemNotifications(obj)
    -- نبحث عن أي عنصر يحتوي على نص التنبيه المزعج
    if obj:IsA("TextLabel") or obj:IsA("TextBox") then
        if obj.Text:find("Sending commands") or obj.Text:find("CommandLimit") then
            -- الصعود للأب (النافذة السوداء بالكامل) وحذفها
            local notificationFrame = obj.Parent
            if notificationFrame then
                notificationFrame.Visible = false
                notificationFrame:Destroy()
            end
        end
    end
end

-- مراقبة الواجهة بشكل مستمر لأي إشعار جديد
playerGui.DescendantAdded:Connect(function(descendant)
    task.wait(0.01) -- انتظار بسيط لضمان ظهور النص داخل العنصر
    hideSystemNotifications(descendant)
end)

-- تنظيف أي إشعارات موجودة حالياً عند تشغيل السكربت
for _, v in pairs(playerGui:GetDescendants()) do
    hideSystemNotifications(v)
end

print("تم تفعيل حماية الواجهة.. لن تظهر رسائل System بعد الآن.")
