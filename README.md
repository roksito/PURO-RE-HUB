local function press(a)
    game:GetService("VirtualInputManager"):SendKeyEvent(true, tostring(a), false, game)
end
local player = game.Players.LocalPlayer
local shop = game:GetService("Workspace").Properties[player.Name].Builds
local job
_G.autofarm = false;
_G.restock = false;
_G.cashier = false;


getgenv().Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/RTrade/Voidz/main/API/Networks/swordhook-network.lua"))() --you can go into the github link and copy all of it and modify it for yourself.
getgenv().Window = getgenv().Library:CreateWindow('Roville', Vector2.new(550, 627), Enum.KeyCode.LeftShift) 

local Test = Window:CreateTab("main")
local Test2 = Test:CreateSector("Section","left")



Test2:AddToggle("farming blox cashier job",false,function(state)
getgenv().cashier = state
while getgenv().cashier do
wait(0.05)

-- Get Cashiers
local cashiers = {}
local stuff = workspace:GetDescendants()
for i = 1, #stuff do local v = stuff[i]
    if v.Name == "Cashier" then
        table.insert(cashiers, v)
    end
end

-- Get Customers
    for _ = 1, 3 do
        for i,v in pairs(cashiers[_].Customers:GetChildren()) do
            if v:FindFirstChild("ChoiceShow") then
                if string.find(v.ChoiceShow.TextLabel.Text, "Fries") then
                    player.Character.Humanoid:MoveTo(cashiers[_].QSpot.Position)
                    wait(player:DistanceFromCharacter(cashiers[_].QSpot.Position)/player.Character.Humanoid.WalkSpeed+0.3)
                    fireclickdetector(cashiers[_].Choices["Bloxy Fries"].ClickDetector, 1)
                elseif string.find(v.ChoiceShow.TextLabel.Text, "Cola") then
                    player.Character.Humanoid:MoveTo(cashiers[_].QSpot.Position)
                    wait(player:DistanceFromCharacter(cashiers[_].QSpot.Position)/player.Character.Humanoid.WalkSpeed+0.3)
                    fireclickdetector(cashiers[_].Choices["Bloxy Cola"].ClickDetector, 1)
                elseif string.find(v.ChoiceShow.TextLabel.Text, "Burger") then
                    player.Character.Humanoid:MoveTo(cashiers[_].QSpot.Position)
                    wait(player:DistanceFromCharacter(cashiers[_].QSpot.Position)/player.Character.Humanoid.WalkSpeed+0.3)
                    fireclickdetector(cashiers[_].Choices["Bloxy Burger"].ClickDetector, 1)
                end
            end
        end
    end
   end
   end)



Test2:AddToggle("auto restock",false,function(state)
getgenv().restock = state
while getgenv().restock do
wait(0.05)
for _,object in ipairs(shop:GetChildren()) do
   if object:FindFirstChild("Products") then
     if object:FindFirstChild("ActionEvent") then
       local A_1 = object
       local Event = game:GetService("ReplicatedStorage").ActionEvents[object.ActionEvent.ActionName.Value]
       Event:FireServer(A_1)
     end
   end
 end
end
end)


Test2:AddToggle("farming banker job",false,function(state)
getgenv().autofarm = state
while getgenv().autofarm do
wait(0.05)

for i,v in pairs(workspace.Bank.BankerJob:GetChildren()) do
   if v:IsA("Model") and player:DistanceFromCharacter(v.Amm.Position) < 6 then
       job = v
   end
end

for i,v in pairs(job.Customers:GetChildren()) do
       if pcall(function() return v.ChoiceShow.TextLabel.Text end) then
local choice = v.ChoiceShow
           local amount = string.split(choice.TextLabel.Text, "$")[2]
           local mm = tick()
           repeat
               pcall(function()
                   fireclickdetector(job.Nums[amount].ClickDetector, 1)
               end)
               wait(.25)
           until job.Amm.SurfaceGui.TextLabel.Text == "$"..amount or tick() - mm > 2
if string.find(choice.TextLabel.Text:lower(), "deposit") then
               fireclickdetector(job.Choices.Deposit.CD, 1)
           else
               fireclickdetector(job.Choices.Withdraw.CD, 1)
           end
           wait(.7)
       end
   end


-- Get Desk


-- Get Customers
   
end
end)
