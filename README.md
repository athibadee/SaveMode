--// Credits to Mercury creator, script by Maplell

local Mercury = loadstring(game:HttpGet("https://raw.githubusercontent.com/deeeity/mercury-lib/master/src.lua"))()
local plr = game:GetService("Players").LocalPlayer
local char = plr.Character
local HissatsuSelected = ""
local HissatsuSequence = ""

local GUI = Mercury:Create{
    Name = "Mercury",
    Size = UDim2.fromOffset(600, 400),
    Theme = Mercury.Themes.Dark,
    Link = "https://github.com/deeeity/mercury-lib"
}

local FarmTab = GUI:Tab{
	Name = "Farm Features",
	Icon = "rbxassetid://8569322835"
}

local SpinTab = GUI:Tab{
	Name = "Spin Hissatsu Features",
	Icon = "rbxassetid://8569322835"
}

--// Spins

local HissatsuDropdown = SpinTab:Dropdown{
	Name = "Hissatsu Select",
	StartingText = "Please Select..",
	Description = "This need to be selected before Add hissatsu.",
	Items = {
		"DragBall",
        "KazaanaDrive",
        "SparkEdge",
        "GhostLock",
        "ShootPocket",
        "ArtemisRing",
        "Aurora",
        "HolyZone",
        "DiamondRay",
        "DisasterBreak",
        "SonicShot",
        "DoubleJaw",
        "DeathDrop",
        "EternalBlizzard",
        "Einsatz",
        "SpiralDraw",
        "TheWall",
        "HuntersNet"
	},
	Callback = function(item) 
        HissatsuSelected = item
        print(HissatsuSelected)
    end
}

local HissatsuPosition = SpinTab:Dropdown{
	Name = "Select Sequence",
	StartingText = "Please Select..",
	Description = "Please select the sequence to add.",
	Items = {
		"FirstHissatsuSpin",
        "SecondHissatsuSpin"
	},
	Callback = function(item) 
        HissatsuSequence = item
        print(HissatsuSequence)
    end
}

SpinTab:Button{
	Name = "Add Hissatsu",
	Description = "Add Selected Hissatsu ( Need to open the spin gui first )",
	Callback = function()
        if HissatsuSelected == "" or HissatsuSequence == "" then GUI:Notification{
            Title = "Alert",
            Text = "Please select the hissatsu nor the sequence first!",
            Duration = 3,
            Callback = function() end
        }
        end

        plr.PlayerGui.HissatsuSpin.Frame.Spins:FindFirstChild(HissatsuSequence).LocalScript.RemoteEvent:FireServer(HissatsuSelected)
    end
}

SpinTab:Button{
	Name = "Reset",
	Description = "Reset the character",
	Callback = function()
        char:WaitForChild("Head"):Destroy()
    end
}

--// Farms

FarmTab:Toggle{
	Name = "Icecream Farm",
	StartingState = false,
	Description = "Icecream Auto-farm ( Pretty Buggy )",
	Callback = function(State)
        _G.TempState = State
        while _G.TempState == true do
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(807,271,-270)
            wait(0.1)
            fireproximityprompt(game:GetService("Workspace").IceCreamGuy:WaitForChild("ExpMoneyQuest").ProximityPrompt, 0)
            wait(0.1)
            game:GetService("Players").LocalPlayer.PlayerGui:WaitForChild("MoneyAndEXPQuest").MainFrame.Frame.Agree.Visible = true
            wait(0.1)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").GettingBoxPart.CFrame * CFrame.new(0,0,0)
            wait(0.01)
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(807,281,-270)
            wait(0.1)
        end
    end
}

FarmTab:Button{
	Name = "Instant Dribble Quest",
	Description = "Please accept the quest before using this.",
	Callback = function()
        char.HumanoidRootPart.CFrame = workspace.Map.SnowyArea.DRIBLLETOUCHPART.CFrame
    end
}

FarmTab:Button{
	Name = "Add Speed Speed Quest",
	Description = "Please accept the quest before using this.",
	Callback = function()
        char.Humanoid.WalkSpeed = 125
    end
}

FarmTab:Button{
	Name = "Reset",
	Description = "Reset the character",
	Callback = function()
        char:WaitForChild("Head"):Destroy()
    end
}

GUI:Credit{
	Name = "Maplell",
	Description = "All features by me",
	V3rm = "R1CarD0",
	Discord = "ZVacia#1916"
}
