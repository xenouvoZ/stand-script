# stand-script

local Player = script.Parent.Parent
	local Mouse = Player:GetMouse()
	repeat wait() until Player.Character
	local Character = Player.Character
	local Camera = workspace.CurrentCamera
	local PlayerGui = Player:WaitForChild("PlayerGui")	
	local allmult = 1
	if Player:WaitForChild("Requiem").Value == true then allmult = 1.25 end
	local Humanoid = Character:WaitForChild("Humanoid")
		table.foreach(Humanoid:GetPlayingAnimationTracks(),function(_,v) v:Stop() end)
			if Character:FindFirstChild("Animate") then Character:FindFirstChild("Animate"):Destroy() end
	local Container = Character.Head:WaitForChild("Container")
	local silenced = Character:WaitForChild("silenced")
	local woosh = Character.Torso:WaitForChild("woosh")
	local voiceline = Character.Torso:WaitForChild("voiceline")
	local menacing = Character.Torso:WaitForChild("Menacing")
	local summonstand = Character.Torso:WaitForChild("summonstand")
	local InputService = game:GetService("UserInputService")
	local intextbox = false
	local changestatevent = game:GetService("ReplicatedStorage").Data.changestat
	local jointevent = game:GetService("ReplicatedStorage").Logic.sendjoints
	local updatejointevent = game:GetService("ReplicatedStorage").Logic.receivejoints
	local hitevent = game:GetService("ReplicatedStorage").Logic.hitbox
	local miscevent = game:GetService("ReplicatedStorage").Logic.misc
	local timestopevent = game:GetService("ReplicatedStorage").Specials.timestop
	local knifeevent = game:GetService("ReplicatedStorage").Specials.spawnknife
	
	miscevent:FireServer(5,Humanoid,16)	

	local Stand = Container:WaitForChild("Stand")

	if Player:WaitForChild("IsHamon").Value == true then
		ScreenGui0 = Instance.new("ScreenGui")
		ImageLabel1 = Instance.new("ImageLabel")
		ImageLabel2 = Instance.new("ImageLabel")
		ScreenGui0.Name = "HamonCharge"
		ScreenGui0.Parent = Player.PlayerGui
		ImageLabel1.Name = "BarFront"
		ImageLabel1.Parent = ScreenGui0
		ImageLabel1.Transparency = 1
		ImageLabel1.Size = UDim2.new(0, 0, 0, 20)
		ImageLabel1.Position = UDim2.new(0.449999988, 0, 0.850000024, 0)
		ImageLabel1.BackgroundColor3 = Color3.new(1, 1, 1)
		ImageLabel1.BackgroundTransparency = 1
		ImageLabel1.ZIndex = 2
		ImageLabel1.Image = "rbxassetid://1061605343"
		ImageLabel2.Name = "BarBack"
		ImageLabel2.Parent = ScreenGui0
		ImageLabel2.Size = UDim2.new(0, 200, 0, 20)
		ImageLabel2.Position = UDim2.new(0.449999988, 0, 0.850000024, 0)
		ImageLabel2.BackgroundColor3 = Color3.new(1, 1, 1)
		ImageLabel2.BorderColor3 = Color3.new(0, 0, 0)
		ImageLabel2.BorderSizePixel = 2
		ImageLabel2.Image = "rbxassetid://1061605343"
		ImageLabel2.ImageColor3 = Color3.new(0.27451, 0.27451, 0.27451)
	end		
		
		function addexp(amount)
			local newamount = amount/4
			if newamount > 0 and Player:FindFirstChild("Experience").Value + newamount < Player:FindFirstChild("Level").Value*200 then 
				changestatevent:FireServer("Experience",Player:FindFirstChild("Experience").Value+newamount,"9u21dhqwhd0hashjda0jfj023j0f")
			elseif newamount > 0 and Player:FindFirstChild("Experience").Value + newamount >= Player:FindFirstChild("Level").Value*200 then
				changestatevent:FireServer("Level",Player:FindFirstChild("Level").Value + 1,"9u21dhqwhd0hashjda0jfj023j0f")
				changestatevent:FireServer("Experience",0,"9u21dhqwhd0hashjda0jfj023j0f")
				changestatevent:FireServer("Points",Player:FindFirstChild("Points").Value + 3,"9u21dhqwhd0hashjda0jfj023j0f")
			end
		end

local Joints={
	Character.HumanoidRootPart.RootJoint;
	Character.Torso.Neck;
	Character.Torso['Left Shoulder'];
	Character.Torso['Right Shoulder'];
	Character.Torso['Left Hip'];
	Character.Torso['Right Hip'];
}

local StandJoints;
local StandTorso;
local ora = Stand.Torso:WaitForChild("ora")
local singleora = Stand.Torso:WaitForChild("singleora")
local specialsound = Character.Torso:WaitForChild("specialsound")
local specialsound2 = Character.Torso:WaitForChild("specialsound2")
local specialtable = {}
local specialvar;
local orig1s;
local orig2s;
local orig3s;
local orig4s;
local orig5s;
local random1;
local random2;
local random3;
local random4;
local random5;

	StandJoints={
		Stand:WaitForChild("Torso").Neck;
		Stand:WaitForChild("Torso")['Left Shoulder'];
		Stand:WaitForChild("Torso")['Right Shoulder'];
		Stand:WaitForChild("Torso")['Left Hip'];
		Stand:WaitForChild("Torso")['Right Hip'];
	}
	
	StandTorso = Stand:WaitForChild("Torso")

	orig1s = StandJoints[1].C0
	orig2s = StandJoints[2].C0
	orig3s = StandJoints[3].C0
	orig4s = StandJoints[4].C0
	orig5s = StandJoints[5].C0

local orig1 = CFrame.new(0,0,0,-1,-0,-0,0,0,1,0,1,0)
local orig2 = CFrame.new(0,1,0,-1,-0,-0,0,0,1,0,1,0)
local orig3 = CFrame.new(-1,0.5,0,-0,-0,-1,0,1,0,1,0,0)
local orig4 = CFrame.new(1,0.5,0,0,0,1,0,1,0,-1,-0,-0)
local orig5 = CFrame.new(-1,-1,0,-0,-0,-1,0,1,0,1,0,0)
local orig6 = CFrame.new(1,-1,0,0,0,1,0,1,0,-1,-0,-0)
local timer = 0
local standtimer = 0
local speed = 0.02
local effecttimer = 0
local hit = false
local animation = 0
local keyframe = 0
local attacking = false
local punching = false
local falling = false
local currentbarrage = 0
local canfall = true
local keepmoving = false
local movetimer = 0
local moveframe = 0
local movespeed = 0
local currenttimestop = 0
local summoned = false
local wastimestop = false
local running = false

local ishamon = false
local charginghamon = false
local hamonpower = 0
local glow;
local light;

	if Player:WaitForChild("IsHamon").Value == true then
		light = StandTorso:WaitForChild("Light")
		glow = StandTorso:WaitForChild("Glow")
	end

local cooled1 = true
local cooled2 = true
local cooled3 = false
local waiter = coroutine.wrap(function()
	wait(35)
	cooled3 = true
end)
waiter()
local cooled4 = true
local cooled5 = true
local cooled6 = true
local cooled7 = true
local cooled8 = true
local cooled9 = true
local cooledz = true

function randomangle(restrict)
	local angle;
		if not restrict then angle = math.random(math.rad(-360),math.rad(360)) else angle = math.random(math.rad(-restrict),math.rad(restrict)) end
return angle;
end

function GetAxis(c1,c2)
	local axis = {}
	axis[1] = (c1[2] - c1[1]).unit
	axis[2] = (c1[3] - c1[1]).unit
	axis[3] = (c1[5] - c1[1]).unit
	axis[4] = (c2[2] - c2[1]).unit
	axis[5] = (c2[3] - c2[1]).unit
	axis[6] = (c2[5] - c2[1]).unit
	axis[7] = axis[1]:Cross(axis[4]).unit
	axis[8] = axis[1]:Cross(axis[5]).unit
	axis[9] = axis[1]:Cross(axis[6]).unit
	axis[10] = axis[2]:Cross(axis[4]).unit
	axis[11] = axis[2]:Cross(axis[5]).unit
	axis[12] = axis[2]:Cross(axis[6]).unit
	axis[13] = axis[3]:Cross(axis[4]).unit
	axis[14] = axis[3]:Cross(axis[5]).unit
	axis[15] = axis[3]:Cross(axis[6]).unit
	return axis;
end

function TestAxis(corners1,corners2,axis,surface)
	if axis.Magnitude == 0 or tostring(axis) == "NAN, NAN, NAN" then
	return true;
	end
	local adists, bdists = {},{}
	for i = 1, 8 do
	table.insert(adists, corners1[i]:Dot(axis))
	table.insert(bdists, corners2[i]:Dot(axis))
	end
	local amax, amin = math.max(unpack(adists)), math.min(unpack(adists))
	local bmax, bmin = math.max(unpack(bdists)), math.min(unpack(bdists))
	local longspan = math.max(amax, bmax) - math.min(amin, bmin)
	local sumspan = amax - amin + bmax - bmin
	local pass,mtv
	if surface then
	pass = longspan <= sumspan
	else
	pass = longspan < sumspan
	end
	if pass then
	local overlap = amax > bmax and -(bmax - amin) or (amax - bmin)
	mtv = axis*overlap
	end
	return pass,mtv;
end

function GetCorners(framepos,size)
	local size,corners = size/2,{}
	for x = -1, 1, 2 do
	for y = -1, 1, 2 do
	for z = -1, 1, 2 do
	table.insert(corners,(framepos*CFrame.new(size * Vector3.new(x, y, z))).p)
	end
	end
	end
	return corners;
end

function NewRegion(framepos,size)
	local region = setmetatable({}, {__index = {}})
	region.surfaceCountsAsCollision = true
	region.cframe = framepos
	region.size = size
	region.planes = {}
	region.corners = GetCorners(region.cframe,region.size)
	for _, enum in next, Enum.NormalId:GetEnumItems() do
	local lnormal = Vector3.FromNormalId(enum)
	local wnormal = region.cframe:vectorToWorldSpace(lnormal)
	local distance = (lnormal*region.size/2).magnitude
	local point = region.cframe.p + wnormal * distance
	table.insert(region.planes,{normal = wnormal,point = point})
	end	
	return region;
end

function ShallowCopy(t)
	local nt = {}
	for k, v in next, t do
	nt[k] = v;
	end
	return nt;
end

function CastPart(part,region)
	local corners1 = region.corners;
	local corners2 = GetCorners(part.CFrame, part.Size)
	local axis, mtvs = GetAxis(corners1,corners2),{}
	for i = 1, #axis do
	local intersect, mtv = TestAxis(corners1, corners2, axis[i], region.surfaceCountsAsCollision);
	if not intersect then return false, Vector3.new(); end;
	if mtv then table.insert(mtvs, mtv) end
	end
	table.sort(mtvs, function(a, b) return a.magnitude < b.magnitude; end);
	return true, mtvs[1]
end
 
function CastRegion(ignore,maxParts,region)
	local ignore = type(ignore) == "table" and ignore or {ignore}
	local maxParts = maxParts or 20
	local rmin,rmax = {},{}
	local copy = ShallowCopy(region.corners)
	for _, enum in next, {Enum.NormalId.Right,Enum.NormalId.Top,Enum.NormalId.Back} do
	local lnormal = Vector3.FromNormalId(enum)
	table.sort(copy,function(a, b) return a:Dot(lnormal) > b:Dot(lnormal) end)
	table.insert(rmin,copy[#copy])
	table.insert(rmax,copy[1])
	end
	rmin,rmax = Vector3.new(rmin[1].x, rmin[2].y, rmin[3].z), Vector3.new(rmax[1].x,rmax[2].y,rmax[3].z)
	local realRegion3 = Region3.new(rmin,rmax)
	local parts = game.Workspace:FindPartsInRegion3WithIgnoreList(realRegion3,ignore,maxParts)
	local inRegion = {}
	for _, part in next, parts do
	if CastPart(part,region) then
	table.insert(inRegion,part)
	end
	end
	return inRegion;
end

if workspace.timestopped.Value == true and workspace.timerstopper.Value ~= Player.Name then
	Character.Torso.Anchored = true
end

game:GetService("ReplicatedStorage").Specials.receiveheartattack.OnClientEvent:connect(function(player,part,frame)
	if part then
		part.CFrame = frame
	end
end)

updatejointevent.OnClientEvent:connect(function(player,characterjoints,standjoints,standtorso)
	if player and player ~= Player and player.Character:FindFirstChild("HumanoidRootPart") and player.Character:FindFirstChild("HumanoidRootPart"):FindFirstChild("RootJoint") then
		player.Character.HumanoidRootPart.RootJoint.C0 = characterjoints[1]
		player.Character.Torso.Neck.C0 = characterjoints[2]
		player.Character.Torso['Left Shoulder'].C0 = characterjoints[3]
		player.Character.Torso['Right Shoulder'].C0 = characterjoints[4]
		player.Character.Torso['Left Hip'].C0 = characterjoints[5]
		player.Character.Torso['Right Hip']	.C0 = characterjoints[6]
		if player.Character.Head:FindFirstChild("Container") and player.Character.Head.Container:FindFirstChild("fakearm") and characterjoints[7] then
			player.Character.Head.Container:FindFirstChild("fakearm").CFrame = characterjoints[7]
			player.Character.Head.Container:FindFirstChild("fakearm").Size = characterjoints[8]
		end
		if standjoints and standtorso then
			standtorso.CFrame = standjoints[1]
			standtorso.Neck.C0 = standjoints[2]
			standtorso['Left Shoulder'].C0 = standjoints[3]
			standtorso['Right Shoulder'].C0 = standjoints[4]
			standtorso['Left Hip'].C0 = standjoints[5]
			standtorso['Right Hip'].C0 = standjoints[6]
			if player.Character.Head.Container:FindFirstChild("fakearm") and standjoints[7] then
				player.Character.Head.Container:FindFirstChild("fakearm").CFrame = standjoints[7]
				player.Character.Head.Container:FindFirstChild("fakearm").Size = standjoints[8]
				player.Character.Head.Container:FindFirstChild("fakearmpart").CFrame = standjoints[9]
				player.Character.Head.Container:FindFirstChild("fakearmpart").Size = standjoints[10]
			end
		end
	end
end)

local replicationtimer = 0

game:GetService("RunService").RenderStepped:connect(function()
if workspace.timestopped.Value == false or workspace.timestopper.Value == Player.Name then
	
	if Humanoid.Health > 0 then
	
	replicationtimer = replicationtimer + 1	
	
	if (replicationtimer%5 == 0) then
		jointevent:FireServer({
		Character.HumanoidRootPart.RootJoint.C0;
		Character.Torso.Neck.C0;
		Character.Torso['Left Shoulder'].C0;
		Character.Torso['Right Shoulder'].C0;
		Character.Torso['Left Hip'].C0;
		Character.Torso['Right Hip'].C0;
		},
		{
		Stand:WaitForChild("Torso").CFrame;
		Stand:WaitForChild("Torso").Neck.C0;
		Stand:WaitForChild("Torso")['Left Shoulder'].C0;
		Stand:WaitForChild("Torso")['Right Shoulder'].C0;
		Stand:WaitForChild("Torso")['Left Hip'].C0;
		Stand:WaitForChild("Torso")['Right Hip'].C0;
		},StandTorso)	
	end
	
	if Player:WaitForChild("IsHamon").Value == true then
		if hamonpower > 0 and not charginghamon and workspace.timestopped.Value == false then
			hamonpower = hamonpower - 0.1
			miscevent:FireServer(9,glow,hamonpower/10)
			ImageLabel1.Size = UDim2.new(0,hamonpower*2,0,20)
			if hamonpower <= 0 then hamonpower = 0 ishamon = false miscevent:FireServer(0,light,false) miscevent:FireServer(0,glow,false) end
		elseif charginghamon and hamonpower < 100 then
			hamonpower = hamonpower + 0.125
			miscevent:FireServer(9,glow,hamonpower/10)
			ImageLabel1.Size = UDim2.new(0,hamonpower*2,0,20)
			if hamonpower >= 100 then charginghamon = false end
		end	
	end

	if keepmoving then
		
		movetimer = movetimer + movespeed
		
		if moveframe == 0 then
		 
		   if movetimer >= 0.8 then movetimer = 0 moveframe = 1 end
			
			if not running then
	
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1-math.sin(movetimer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(movetimer*2)/1.5 , (0.1+math.sin(movetimer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1-math.sin(movetimer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(movetimer*2)/1.5 , (0.1+math.sin(movetimer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
			else
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1-math.sin(movetimer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(movetimer*2)/1.15 , (0.1+math.sin(movetimer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1-math.sin(movetimer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(movetimer*2)/1.15 , (0.1+math.sin(movetimer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)

			end
			
		elseif moveframe == 1 then
		 
		  if movetimer >= 0.8 then movetimer = 0 moveframe = 0 end
			
			if not running then
				
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1+math.sin(movetimer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(movetimer*2)/1.5 , (0.1-math.sin(movetimer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1+math.sin(movetimer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(movetimer*2)/1.5 , (0.1-math.sin(movetimer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
				
			else
				
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1+math.sin(movetimer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(movetimer*2)/1.15 , (0.1-math.sin(movetimer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1+math.sin(movetimer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(movetimer*2)/1.15 , (0.1-math.sin(movetimer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , movespeed*1.95)
			
			end
			
		end
		
	end		
	
	timer = timer + speed
	if not attacking or animation == 5 then standtimer = standtimer + 0.02 end
		
		if Character.HumanoidRootPart.Velocity.Y > 5 and not attacking and not falling and canfall then falling = true keepmoving = false speed = 0.02 canfall = false animation = 2 keyframe = 0 if timer >= 0.5 then timer = 0 end end
			if Character.HumanoidRootPart.Velocity.Y < -5 and not attacking and not falling and canfall then falling = true keepmoving = false speed = 0.02 canfall = false animation = 2 keyframe = 1 if timer >= 1 then timer = 0 end end	
		
		if not falling then
			if Humanoid.MoveDirection == Vector3.new(0,0,0) and not attacking and animation ~= 0 then
				animation = 0
				speed = 0.02
				if keyframe > 1 then keyframe = 0 end
				if timer >= 1.5 then timer = 0 end
				keepmoving = false
			elseif Humanoid.MoveDirection ~= Vector3.new(0,0,0) and not attacking and animation ~= 1 then
				animation = 1
				timer = movetimer
				if running then speed = 0.04 else speed = 0.03 end
				if keyframe > 1 then keyframe = 0 end
				if timer >= 0.8 then timer = 0 end
				keepmoving = false
			end
		elseif falling then
			local region = NewRegion(Character.HumanoidRootPart.CFrame*CFrame.new(0,-4.1,0),Vector3.new(2,1,1))
			for _,part in pairs (CastRegion(Character,math.huge,region)) do 
				if part and part.CanCollide then 
					local waiter = coroutine.wrap(function()
						falling = false
						wait(0.15)
						canfall = true
					end)
					waiter()
					break;
				 end
			end
		end
	
	if animation == 0 then
		if keyframe == 0 then
	
		    if timer >= 1.5 then timer = 0 keyframe = 1 end
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.1)*CFrame.Angles(0,0,math.rad(-8)) , speed*1.2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(8),0,math.rad(8)) , speed*1.2)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.5)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(5),0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
				
		elseif keyframe == 1 then
			
		   if timer >= 1.5 then timer = 0 keyframe = 0 end
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(4),0,math.rad(-7)) , speed*1.2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(0,0,math.rad(7)) , speed*1.2)	
				
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-4),math.rad(7),math.rad(-5)) , speed*1.5)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-4),math.rad(-8),math.rad(3)) , speed*1.5)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-8),math.rad(13),math.rad(-8)) , speed*1.2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(7),math.rad(6)) , speed*1.2)
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(5),0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then				
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
					
		end
	elseif animation == 1 then
		if keyframe == 0 then
		 
		   if timer >= 0.8 then timer = 0 keyframe = 1 end
			
			if not running then
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-timer*1.5)/1.5)*CFrame.Angles(math.rad(4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X*3),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-7),0,math.rad(53*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-7),0,math.rad(53*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1-math.sin(timer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(timer*2)/1.5 , (0.1+math.sin(timer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1-math.sin(timer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(timer*2)/1.5 , (0.1+math.sin(timer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
				
			else
			
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-timer*1.5)/1.15)*CFrame.Angles(math.rad(12*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X*7),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-9),0,math.rad(57*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-9),0,math.rad(57*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1-math.sin(timer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(timer*2)/1.15 , (0.1+math.sin(timer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1-math.sin(timer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(timer*2)/1.15 , (0.1+math.sin(timer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(-23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3), math.rad( (-43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) -14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then				
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end		
				
			end
			
		elseif keyframe == 1 then
		 
		  if timer >= 0.8 then timer = 0 keyframe = 0 end
			
			if not running then
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-timer*1.5)/1.5)*CFrame.Angles(math.rad(4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X*3),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-7),0,math.rad(-53*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
		
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-7),0,math.rad(-53*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1+math.sin(timer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(timer*2)/1.5 , (0.1-math.sin(timer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1+math.sin(timer*2)/1.5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(timer*2)/1.5 , (0.1-math.sin(timer*2)/5)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then				
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
				
			else
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-timer*1.5)/1.15)*CFrame.Angles(math.rad(12*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X*7),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-9),0,math.rad(-57*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
		
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-9),0,math.rad(-57*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new((0.1+math.sin(timer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1-math.cos(timer*2)/1.15 , (0.1-math.sin(timer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new((0.1+math.sin(timer*2)/1.15)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z , 0.1+math.cos(timer*2)/1.15 , (0.1-math.sin(timer*2)/4.65)*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X)*CFrame.Angles(math.rad(23*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X) , math.rad(-3) , math.rad( (43*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z) +14*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X )) , speed*1.95)
			
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)	
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
			
			end
			
		end
	elseif animation == 2 then
		if keyframe == 0 then
			
			 if timer >= 0.5 then timer = 0 keyframe = 1 end	
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(3*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-5+(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-11),math.rad(4),0) , speed*1.75)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-11),math.rad(4),0) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new(-0.5,0.2,0)*CFrame.Angles(math.rad(-1.5),0,math.rad(-2)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(0,0,math.rad(-52)) , speed*2)
	
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(-7),0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
					
		elseif keyframe == 1 then 	
	
			 if timer >= 1 then keyframe = 2 end	
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z),math.rad(3*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).X),0) , speed*1.75)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(12+(-4*-Character.HumanoidRootPart.CFrame:vectorToObjectSpace(Humanoid.MoveDirection).Z)),0,0) , speed*1.75)
		
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-11),math.rad(4),0) , speed*1.75)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-11),math.rad(4),0) , speed*1.75)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new(-0.5,0.2,0)*CFrame.Angles(math.rad(-1.5),0,math.rad(-11)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(0,0,math.rad(-59)) , speed*2)
			
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(-7),0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
					end
						
		end
	elseif animation == 3 then
		if keyframe == 0 then
		
			if timer >= 0.75 then timer = 0 keyframe = 1 hit = false random2 = orig2s*CFrame.new(math.random(-55,-35)/30,0,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),math.rad(math.random(-100,3700)/100),math.rad(math.random(-10800,-9700)/100)) end	
				
				effecttimer = effecttimer + 1			
				
				if (effecttimer%3 == 0) then
					if not hit then
						local region = NewRegion(Stand['Right Arm'].CFrame,Stand['Right Arm'].Size)
							local hum;
								for _,v in pairs (CastRegion(Character,math.huge,region)) do
									if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
									if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end
								end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Right Arm'],Stand['Right Arm'].CFrame,0.55*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
					end
					local clone = Stand:WaitForChild("Right Arm"):Clone()
					clone.Parent = Container
					clone:ClearAllChildren()
					clone.Anchored = true
					clone.Transparency = 0.5
						local fader = coroutine.wrap(function()
							for i=1, 10 do
								clone.Transparency = clone.Transparency + 0.05
								wait()
							end
							clone:Remove()
						end)
					fader()
				end
				
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed)	
			
			else
				
				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end	
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
						
			end	
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(-3),0,math.rad(-30)) , speed*2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.new(1.15,0,0)*CFrame.Angles(math.rad(17),math.rad(-5),math.rad(-88)) , speed*2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(random3 , speed*2)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(-3),math.rad(40),0) , speed*4)	
		
		elseif keyframe == 1 then
				
			if timer >= 0.75 then timer = 0 keyframe = 0 hit = false random3 = orig3s*CFrame.new(math.random(35,55)/30,0,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),math.rad(math.random(-100,3700)/100),math.rad(math.random(8600,9400)/100)) end	
				
				effecttimer = effecttimer + 1			
				
				if (effecttimer%3 == 0) then
					if not hit then
						local region = NewRegion(Stand['Left Arm'].CFrame,Stand['Left Arm'].Size)
							local hum;
								for _,v in pairs (CastRegion(Character,math.huge,region)) do
									if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
									if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end
								end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Left Arm'],Stand['Left Arm'].CFrame,0.55*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
					end
					local clone = Stand:WaitForChild("Left Arm"):Clone()
					clone.Parent = Container
					clone:ClearAllChildren()
					clone.Anchored = true
					clone.Transparency = 0.5
						local fader = coroutine.wrap(function()
							for i=1, 10 do
								clone.Transparency = clone.Transparency + 0.05
								wait()
							end
							clone:Remove()
						end)
					fader()
				end
	
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed)	
			
			else
				
				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end	
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
						
			end	
	
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(-3),0,math.rad(30)) , speed*2)
	
					StandJoints[2].C0 = StandJoints[2].C0:lerp(random2 , speed*2)								
					
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.new(-1.15,0,0)*CFrame.Angles(math.rad(17),math.rad(-5),math.rad(88)) , speed*2)
							
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(-3),math.rad(-40),0) , speed*4)	
				
		end
	elseif animation == 4 then
		if keyframe == 0 then
			
			if timer >= 0.75 then keyframe = 1 timer = 0 speed = 0.1*Player:WaitForChild("Speed").Value*allmult random3 = orig3s*CFrame.new(math.random(55,75)/35,0.55,0)*CFrame.Angles(math.rad(math.random(890,910)/10),math.rad(math.random(-700,700)/100),math.rad(math.random(7100,7500)/100)) end
			
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*3)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*3)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*3)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*3)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*3)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*3)	
			
			else
				
				if not keepmoving then
					keepmoving = true
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end

				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*3)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*3)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*3)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*3)
				
			end	
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(-4),0,math.rad(80)) , speed*2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-14),math.rad(7),0) , speed*2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(random3 , speed*2)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(4),math.rad(-80),0) , speed*4)	
		
		elseif keyframe == 1 then
		
			if timer >= 0.75 then
				timer = 0
				attacking = false
					local waiter = coroutine.wrap(function()
						wait(3)								
						cooled2 = true
					end)
				waiter()
				animation = -1
				keyframe = 0
				miscevent:FireServer(7,Humanoid,50)
				speed = 0.02
			end	
				
				effecttimer = effecttimer + 1			
				
				if (effecttimer%2 == 0) then 
					if not hit then
						local region = NewRegion(Stand['Right Arm'].CFrame,Stand['Right Arm'].Size)
							local hum;
								for _,v in pairs (CastRegion(Character,math.huge,region)) do
									if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
									if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end							
								end
							if hum and hum.Health > 0 then
								hit = true
								local results = hitevent:InvokeServer(2,Stand['Right Arm'],Stand['Right Arm'].CFrame,10*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
								if results then  else hit = false end
							end
					end
					local clone = Stand:WaitForChild("Right Arm"):Clone()
					clone.Parent = Container
					clone:ClearAllChildren()
					clone.Anchored = true
					clone.Transparency = 0.5
						local fader = coroutine.wrap(function()
							for i=1, 5 do
								clone.Transparency = clone.Transparency + 0.1
								wait()
							end
							clone:Remove()
						end)
					fader()
				end

			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed)	
					
			else

				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
					
			end
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(7),0,math.rad(-65)) , speed*2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-12),math.rad(5),0) , speed*2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(random3 , speed*2)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(-7),math.rad(65),0) , speed*4)	
		
		end
	elseif animation == 5 then
		if keyframe == 0 then
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(-5),0,math.rad(-57)) , speed*3)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(5),0,math.rad(-37)) , speed*3)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(27),0,math.rad(17)) , speed*3)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(0,math.rad(47),math.rad(137)) , speed*3)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new(0,-0.05,0)*CFrame.Angles(math.rad(-3),math.rad(15),math.rad(9)) , speed*3)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-3),math.rad(-12),math.rad(-9)) , speed*2)		
	
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(5),0,math.rad(-37)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(27),0,math.rad(17)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(0,math.rad(47),math.rad(137)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.05,0)*CFrame.Angles(math.rad(-3),math.rad(15),math.rad(9)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.Angles(math.rad(-3),math.rad(-12),math.rad(-9)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,0,3)*CFrame.Angles(0,math.rad(-57),math.rad(-5)) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.Angles(0,math.rad(-57),math.rad(-5)) , speed*5)
					end
					
		elseif keyframe == 1 then
	
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(-12),0,0) , speed*3)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(12),0,0) , speed*3)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.new(-0.5,0,0.4)*CFrame.Angles(math.rad(-77),math.rad(92),math.rad(-7)) , speed*3)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.new(0.5,0,0.4)*CFrame.Angles(math.rad(-77),math.rad(-92),math.rad(7)) , speed*3)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-3),math.rad(12),math.rad(12)) , speed*3)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-3),math.rad(-12),math.rad(-12)) , speed*2)		
	
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(12),0,0) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.new(-0.5,0,0.4)*CFrame.Angles(math.rad(-77),math.rad(92),math.rad(-7)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.new(0.5,0,0.4)*CFrame.Angles(math.rad(-77),math.rad(-92),math.rad(7)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.Angles(math.rad(-3),math.rad(12),math.rad(12)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.Angles(math.rad(-3),math.rad(-12),math.rad(-12)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,0,3)*CFrame.Angles(math.rad(12),0,0) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.Angles(math.rad(12),0,0) , speed*5)
					end
					
		end
	elseif animation == 6 then
		if keyframe == 0 then
			
			if timer >= 1.75 then 
				timer = 0 
				keyframe = 0 
				attacking = false
				animation = -1
				keyframe = 0
				speed = 0.02
				miscevent:FireServer(7,Humanoid,50)
				if not wastimestop then 
					local waiter = coroutine.wrap(function()
						wait(5)
						cooled4 = true
					end)
					waiter()
				elseif wastimestop then
					local waiter = coroutine.wrap(function()
						wait(0.75)
						cooled6 = true
					end)
					waiter()
				end
			end		
				
			effecttimer = effecttimer + 1
				
					if effecttimer >= 0 or effecttimer <= 0 then
					knifeevent:FireServer(Character['Right Arm'].CFrame*CFrame.new(0,-2,0)*CFrame.Angles(math.rad(185),math.rad(90),math.rad(-5)),7*Player:WaitForChild("Power").Value*allmult,voiceline,ishamon,Player:WaitForChild("IsVampire").Value)
				end
							
				if Humanoid.MoveDirection == Vector3.new(0,0,0) then
						
					keepmoving = false
						
					Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
					
					Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
		
					Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
					
					Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(7),0,math.rad(94)) , speed*2)
				
					Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*2)
				
					Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*2)	
						
				else
	
					if not keepmoving then
						keepmoving = true	
						if running then movespeed = 0.04 else movespeed = 0.03 end
						if moveframe > 1 then moveframe = 0 end
						if movetimer >= 0.8 then movetimer = 0 end
					end
					
					Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
					
					Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
		
					Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
					
					Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(7),0,math.rad(94)) , speed*2)
							
				end		
				
						StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(5),0,math.rad(-3)) , speed*1.2)
						
						StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
				
						StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
						
						StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
					
						StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
						
						if summoned then
							StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,1+math.cos(standtimer)/2,3) , speed*3)
						else
							StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*5)
						end
		end
	elseif animation == 7 then
		if keyframe == 0 then
			
			if timer >= 0.75 then keyframe = 1 timer = 0 speed = 0.05*Player:WaitForChild("Speed").Value*allmult miscevent:FireServer(2,woosh,math.random(110,120)/100) miscevent:FireServer(1,woosh,0) random2 = orig2s*CFrame.new(math.random(15,35)/40,0,0)*CFrame.Angles(math.rad(math.random(-500,-100)/100),math.rad(math.random(-1200,2500)/100),math.rad(math.random(8600,9400)/100)) end

			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
					
				keepmoving = false
					
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*2)	
					
			else

				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
						
			end				
					
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(-2),math.rad(-80),0) , speed*2)
									
						StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(2),0,math.rad(80)) , speed*2)
						
						StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-14),math.rad(7),0) , speed*2)
				
						StandJoints[3].C0 = StandJoints[3].C0:lerp(random3 , speed*2)
						
						StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
					
						StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)

					
		elseif keyframe == 1 then
		
			if timer >= 0.75 then 
				timer = 0 
				keyframe = 0 
				attacking = false
				animation = -1
				keyframe = 0
				speed = 0.02
				miscevent:FireServer(7,Humanoid,50)
				local waiter = coroutine.wrap(function()
					wait(0.2)
					cooled5 = true
				end)
				waiter()
			end			
				
				if not hit then 
					local region = NewRegion(Stand['Right Arm'].CFrame,Stand['Right Arm'].Size)
						local hum;
							for _,v in pairs (CastRegion(Character,math.huge,region)) do
								if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
								if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end
							end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Right Arm'],Stand['Right Arm'].CFrame,2*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
				end
				
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
					
				keepmoving = false
					
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*2)	
					
			else

				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
						
			end
			
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(0,math.rad(40),0) , speed*4)
						
						StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(-30)) , speed*4)
							
						StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-12),math.rad(5),0) , speed*2)
				
						StandJoints[3].C0 = StandJoints[3].C0:lerp(random3 , speed*2)
							
						StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
						
						StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)
					
		end
	elseif animation == 8 then
		if keyframe == 0 then
			
			if timer >= 0.75 then keyframe = 1 timer = 0 speed = 0.05*Player:WaitForChild("Speed").Value*allmult miscevent:FireServer(2,woosh,math.random(110,120)/100) miscevent:FireServer(1,woosh,0) random2 = orig2s*CFrame.new(math.random(-35,-15)/40,0,0)*CFrame.Angles(math.rad(math.random(-500,-100)/100),math.rad(math.random(-1200,2500)/100),math.rad(math.random(-9400,-8600)/100)) end
					
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
					
				keepmoving = false
					
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*2)	
					
			else

				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
						
			end				
					
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(math.rad(-2),math.rad(80),0) , speed*2)
									
						StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(2),0,math.rad(-80)) , speed*2)
						
						StandJoints[2].C0 = StandJoints[2].C0:lerp(random2 , speed*2)
				
						StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-14),math.rad(-7),0) , speed*2)
						
						StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(-4)) , speed*2)
					
						StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(3)) , speed*2)
					
		elseif keyframe == 1 then
				
			if timer >= 0.75 then 
				timer = 0 
				keyframe = 0 
				attacking = false
				animation = -1
				keyframe = 0
				speed = 0.02
				miscevent:FireServer(7,Humanoid,50)
				local waiter = coroutine.wrap(function()
					wait(0.2)
					cooled5 = true
				end)
				waiter()
			end			
				
				if not hit then 
					local region = NewRegion(Stand['Left Arm'].CFrame,Stand['Left Arm'].Size)
						local hum;
							for _,v in pairs (CastRegion(Character,math.huge,region)) do
								if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
								if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end							
							end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Left Arm'],Stand['Left Arm'].CFrame,2*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
				end
					
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
					
				keepmoving = false
					
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed*2)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed*2)	
					
			else

				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed*2)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed*2)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed*2)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed*2)
						
			end
					
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,0,-3.5)*CFrame.Angles(0,math.rad(-40),0), speed*4)
						
						StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(0,0,math.rad(30)) , speed*4)
		
						StandJoints[2].C0 = StandJoints[2].C0:lerp(random2 , speed*2)								
							
						StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-12),math.rad(-5),0) , speed*2)
									
						StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*2)
						
						StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*2)
				
		end	
	elseif animation == 9 then
		if keyframe == 0 then
		
			if timer >= 0.75 then timer = 0 keyframe = 1 hit = false random4 = orig4s*CFrame.new(0,math.random(-55,-35)/40,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),0,math.rad(math.random(500,700)/100)) end	
				
				effecttimer = effecttimer + 1			
				
				if (effecttimer%3 == 0) then
					if not hit then
						local region = NewRegion(Stand['Right Leg'].CFrame,Stand['Right Leg'].Size)
							local hum;
								for _,v in pairs (CastRegion(Character,math.huge,region)) do
									if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
									if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end
								end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Right Leg'],Stand['Right Leg'].CFrame,0.595*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
					end
					local clone = Stand:WaitForChild("Right Leg"):Clone()
					clone.Parent = Container
					clone:ClearAllChildren()
					clone.Anchored = true
					clone.Transparency = 0.5
						local fader = coroutine.wrap(function()
							for i=1, 10 do
								clone.Transparency = clone.Transparency + 0.05
								wait()
							end
							clone:Remove()
						end)
					fader()
				end
				
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed)	
			
			else
				
				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end	
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
						
			end	
				
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(45),0,math.rad(-30)) , speed*2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(32),0,0) , speed*2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(32),0,0) , speed*2)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.Angles(math.rad(-3),0,math.rad(15)) , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(random5 , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,2.5,-5.5)*CFrame.Angles(math.rad(35),math.rad(30),0) , speed*4)	
		
		elseif keyframe == 1 then
				
			if timer >= 0.75 then timer = 0 keyframe = 0 hit = false random5 = orig5s*CFrame.new(0,math.random(-55,-35)/40,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),0,math.rad(math.random(-700,-500)/100)) miscevent:FireServer(2,woosh,math.random(90,110)/100) end	
				
				effecttimer = effecttimer + 1			
				
				if (effecttimer%3 == 0) then
					if not hit then
						local region = NewRegion(Stand['Left Leg'].CFrame,Stand['Left Leg'].Size)
							local hum;
								for _,v in pairs (CastRegion(Character,math.huge,region)) do
									if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and (v.Parent:FindFirstChild("Torso") or v.Parent:FindFirstChild("UpperTorso")) then hum = v.Parent:FindFirstChildOfClass("Humanoid") end end
									if not hum then if v.Parent and v.Parent.Name == "Stand" then hum = v.Parent.Parent.Parent.Parent:FindFirstChildOfClass("Humanoid") end end
								end
						if hum and hum.Health > 0 then
							hit = true
							local results = hitevent:InvokeServer(1,Stand['Left Leg'],Stand['Left Leg'].CFrame,0.595*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,nil,ishamon,Player:WaitForChild("IsVampire").Value) 
							if results then  else hit = false end
						end
					end
					local clone = Stand:WaitForChild("Left Leg"):Clone()
					clone.Parent = Container
					clone:ClearAllChildren()
					clone.Anchored = true
					clone.Transparency = 0.5
						local fader = coroutine.wrap(function()
							for i=1, 10 do
								clone.Transparency = clone.Transparency + 0.05
								wait()
							end
							clone:Remove()
						end)
					fader()
				end
	
			if Humanoid.MoveDirection == Vector3.new(0,0,0) then
				
				keepmoving = false
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
			
				Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-4),math.rad(22),math.rad(-2)) , speed)
			
				Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-4),math.rad(-22),math.rad(2)) , speed)	
			
			else
				
				if not keepmoving then
					keepmoving = true	
					if running then movespeed = 0.04 else movespeed = 0.03 end
					if moveframe > 1 then moveframe = 0 end
					if movetimer >= 0.8 then movetimer = 0 end
				end	
				
				Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.new(0,0,0.4-math.cos(-movetimer*1.5)/1.5)*CFrame.Angles(0,0,math.rad(-3)) , speed)
				
				Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(1),0,math.rad(3)) , speed)
	
				Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(9),math.rad(33),math.rad(23)) , speed)
				
				Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(9),math.rad(-33),math.rad(-23)) , speed)
						
			end	
	
					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(45),0,math.rad(30)) , speed*2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(32),0,0) , speed*2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(32),0,0) , speed*2)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(random4 , speed*2)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.Angles(math.rad(3),0,math.rad(-15)) , speed*2)
					
					StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(0,2.5,-5.5)*CFrame.Angles(math.rad(35),math.rad(-30),0) , speed*4)
				
		end	
	elseif animation == 10 then		
		if keyframe == 0 then
			
			effecttimer = effecttimer + 1
				
					if (effecttimer%15 == 0) then 
						local clone = Character:WaitForChild("Right Arm"):Clone()
						clone.Parent = Container
						clone.Color = Color3.new(1,0,0)
						clone:ClearAllChildren()
						clone.Anchored = true
						clone.Material = "Neon"
						clone.Transparency = 0.5
						local mesh = Instance.new("BlockMesh",clone)
							mesh.Scale = Vector3.new(1,1,1)
							local fader = coroutine.wrap(function()
								for i=1, 10 do
									clone.Transparency = clone.Transparency + 0.05
									mesh.Scale = mesh.Scale + Vector3.new(0.05,0.05,0.05)
									wait()
								end
								clone:Remove()
							end)
						fader()
							local region = NewRegion(Character['Right Arm'].CFrame,Character['Right Arm'].Size)
								local hum;
								local hitpart;
									for _,v in pairs (CastRegion(Player.Character,math.huge,region)) do
										if not hum then if v.Parent and v.Parent:FindFirstChildOfClass("Humanoid") and v.Parent:FindFirstChild("Torso") then hum = v.Parent:FindFirstChildOfClass("Humanoid") hitpart = v end end
									end
								if hum and hum.Health > 0 then
									local results;
										results = hitevent:InvokeServer(0,Character['Right Arm'],Character['Right Arm'].CFrame,1.85*Player:WaitForChild("Power").Value*allmult,voiceline,hum,false,hitpart,false,true,true) 
								end
					end
				
				if Humanoid.MoveDirection == Vector3.new(0,0,0) then
	
					keepmoving = false
	
					Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(3),0,math.rad(52)) , speed*2)
					
					Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-3),0,math.rad(-52)) , speed*2)
						
					Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-12),math.rad(5),0) , speed*2)
				
					Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.new(0.75,0,0)*CFrame.Angles(math.rad(-3),math.rad(-33),math.rad(87)) , speed*2)
						
					Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-8),math.rad(7),math.rad(1)) , speed*2)
					
					Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.new(0,-0.07,0)*CFrame.Angles(math.rad(-3),math.rad(3),math.rad(-2)) , speed*2)
				
				else
					
					if not keepmoving then
						keepmoving = true
						if running then movespeed = 0.04 else movespeed = 0.03 end			
						if moveframe > 1 then moveframe = 0 end
						if movetimer >= 0.8 then movetimer = 0 end
					end
					
					Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(3),0,math.rad(52)) , speed*2)
					
					Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-3),0,math.rad(-52)) , speed*2)				
					
					Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-12),math.rad(5),0) , speed*2)
				
					Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.new(0.75,0,0)*CFrame.Angles(math.rad(-3),math.rad(-33),math.rad(87)) , speed*2)
				
				end

					StandJoints[1].C0 = StandJoints[1].C0:lerp(orig1s*CFrame.Angles(math.rad(5),0,math.rad(-3)) , speed*1.2)
					
					StandJoints[2].C0 = StandJoints[2].C0:lerp(orig2s*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(-3)) , speed*1.2)
			
					StandJoints[3].C0 = StandJoints[3].C0:lerp(orig3s*CFrame.Angles(math.rad(-2),math.rad(-4),math.rad(5)) , speed*1.5)
					
					StandJoints[4].C0 = StandJoints[4].C0:lerp(orig4s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-7),math.rad(12),math.rad(-3)) , speed*1.5)
				
					StandJoints[5].C0 = StandJoints[5].C0:lerp(orig5s*CFrame.new(0,-0.09,0)*CFrame.Angles(math.rad(-5),math.rad(8),math.rad(4)) , speed*1.2)
					
					if summoned then
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame*CFrame.new(-3,0,3) , speed*3)
					else
						StandTorso.CFrame = StandTorso.CFrame:lerp(Character.HumanoidRootPart.CFrame , speed*3)
					end				
				
			end	
	end
	
	end

end
end)

InputService.TextBoxFocused:connect(function()
	intextbox = true
end)

InputService.TextBoxFocusReleased:connect(function()
	intextbox = false
end)

InputService.InputBegan:connect(function(input)
	if workspace.timestopped.Value == false or workspace.timestopper.Value == Player.Name then
		if input.UserInputType == Enum.UserInputType.Keyboard and not intextbox and silenced.Value == false then
			if input.KeyCode == Enum.KeyCode.E --[[and not attacking and not charginghamon and cooled1]] and Humanoid.Health > 0 then
				attacking = true
					if not summoned then
						miscevent:FireServer(2,summonstand,math.random(90,110)/100)
						miscevent:FireServer(1,summonstand,0)
						miscevent:FireServer(3,Stand.Head.face,0)
						for _,v in pairs(Stand:GetChildren()) do
							if v:IsA("BasePart") then
								local fader = coroutine.wrap(function()
									for i=1, 10 do
										miscevent:FireServer(3,v,1-(i/10))
										wait()
									end
								end)
								fader()
							end
						end
						summoned = true
					end
					cooled1 = false
					animation = 3
					keyframe = 0
					timer = 0
					movetimer = timer
					currentbarrage = currentbarrage + 1
					local lastbarrage = currentbarrage
					local duration = coroutine.wrap(function()
						wait(3)
						if currentbarrage == lastbarrage and animation == 3 then
							timer = 0
							attacking = false
								local waiter = coroutine.wrap(function()
									wait(2)								
									cooled1 = true
								end)
							waiter()
							animation = -1
							keyframe = 0
							miscevent:FireServer(1,ora,1)
							miscevent:FireServer(7,Humanoid,50)
							speed = 0.02
						end
					end)
					duration()
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					speed = 0.1*Player:WaitForChild("Speed").Value*allmult
					hit = false
					random3 = orig3s*CFrame.new(math.random(35,55)/30,0,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),math.rad(math.random(-100,3700)/100),math.rad(math.random(9700,10800)/100))
					miscevent:FireServer(2,woosh,math.random(90,110)/100)
					miscevent:FireServer(1,woosh,0)
					miscevent:FireServer(1,ora,0)
			elseif input.KeyCode == Enum.KeyCode.Y --[[and not attacking and not charginghamon and cooled8]] and Humanoid.Health > 0 and Player:FindFirstChild("Requiem").Value == true then
				attacking = true
					if not summoned then
						miscevent:FireServer(2,summonstand,math.random(90,110)/100)
						miscevent:FireServer(1,summonstand,0)
						miscevent:FireServer(3,Stand.Head.face,0)
						for _,v in pairs(Stand:GetChildren()) do
							if v:IsA("BasePart") then
								local fader = coroutine.wrap(function()
									for i=1, 10 do
										miscevent:FireServer(3,v,1-(i/10))
										wait()
									end
								end)
								fader()
							end
						end
						summoned = true
					end
					cooled8 = false
					animation = 9
					keyframe = 0
					timer = 0
					movetimer = timer
					currentbarrage = currentbarrage + 1
					local lastbarrage = currentbarrage
					local duration = coroutine.wrap(function()
						wait(2.5)
						if currentbarrage == lastbarrage and animation == 9 then
							timer = 0
							attacking = false
								local waiter = coroutine.wrap(function()
									wait(5)								
									cooled8 = true
								end)
							waiter()
							animation = -1
							keyframe = 0
							miscevent:FireServer(1,ora,1)
							miscevent:FireServer(7,Humanoid,50)
							speed = 0.02
						end
					end)
					duration()
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					speed = 0.075*Player:WaitForChild("Speed").Value*allmult
					hit = false
					random5 = orig5s*CFrame.new(0,math.random(-55,-35)/40,0)*CFrame.Angles(math.rad(math.random(-300,300)/100),0,math.rad(math.random(-700,-500)/100))
					miscevent:FireServer(2,woosh,math.random(90,110)/100)
					miscevent:FireServer(1,woosh,0)
					miscevent:FireServer(1,ora,0)
			elseif input.KeyCode == Enum.KeyCode.R --[[and not attacking and not charginghamon and cooled2]] and Humanoid.Health > 0 then
				attacking = true
					if not summoned then
						miscevent:FireServer(2,summonstand,math.random(90,110)/100)
						miscevent:FireServer(1,summonstand,0)
						miscevent:FireServer(3,Stand.Head.face,0)
						for _,v in pairs(Stand:GetChildren()) do
							if v:IsA("BasePart") then
								local fader = coroutine.wrap(function()
									for i=1, 10 do
										miscevent:FireServer(3,v,1-(i/10))
										wait()
									end
								end)
								fader()
							end
						end
						summoned = true
					end
					cooled2 = false
					animation = 4
					keyframe = 0
					timer = 0
					movetimer = timer
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					random3 = orig3s*CFrame.new(-math.random(15,20)/40,0,0)*CFrame.Angles(-math.rad(math.random(-800,200)/100),math.rad(math.random(-5100,1200)/100),math.rad(math.random(8600,9400)/100))
					speed = 0.025*Player:WaitForChild("Speed").Value*allmult
					hit = false
					miscevent:FireServer(2,woosh,math.random(90,110)/100)
					miscevent:FireServer(1,woosh,0)
					miscevent:FireServer(1,singleora,0)
			--[[elseif input.KeyCode == Enum.KeyCode.R and animation == 3 and not charginghamon and cooled2 and Humanoid.Health > 0 then
					cooled2 = false
					animation = 4
					keyframe = 0
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					movetimer = timer
					timer = 0
					random3 = orig3s*CFrame.new(-math.random(15,20)/40,0,0)*CFrame.Angles(-math.rad(math.random(-800,200)/100),math.rad(math.random(-5100,1200)/100),math.rad(math.random(8600,9400)/100))
					speed = 0.025*Player:WaitForChild("Speed").Value*allmult
					hit = false
					miscevent:FireServer(1,ora,1)
						local waiter = coroutine.wrap(function()
							wait(2)								
							cooled1 = true
						end)
					waiter()
					miscevent:FireServer(1,singleora,0)]]
			elseif input.KeyCode == Enum.KeyCode.F --[[and not attacking and cooled3 and not charginghamon]] and Humanoid.Health > 0 and Player:WaitForChild("Requiem").Value == true and workspace.timestopped.Value == false then
				cooled3 = false
				
					if not summoned then
						miscevent:FireServer(2,summonstand,math.random(90,110)/100)
						miscevent:FireServer(1,summonstand,0)
						miscevent:FireServer(3,Stand.Head.face,0)
						for _,v in pairs(Stand:GetChildren()) do
							if v:IsA("BasePart") then
								local fader = coroutine.wrap(function()
									for i=1, 10 do
										miscevent:FireServer(3,v,1-(i/10))
										wait()
									end
								end)
								fader()
							end
						end
						summoned = true
					end
				
				timestopevent:FireServer(4*Player:WaitForChild("Special").Value*allmult,Character,specialsound,specialsound2,0,"asdj92udu92hu9uasud9u2df")				
				
				currenttimestop = currenttimestop + 1	
				local thistimestop = currenttimestop			
					local waiter = coroutine.wrap(function()
						wait(35+(4*Player:WaitForChild("Special").Value*allmult))
						if currenttimestop == thistimestop then cooled3 = true end
					end)
					waiter()
			elseif input.KeyCode == Enum.KeyCode.F --[[and not attacking and not charginghamon]] and Humanoid.Health > 0 and workspace.timestopped.Value == true and workspace.timestopper.Value == Player.Name then
				timestopevent:FireServer(4*Player:WaitForChild("Special").Value*allmult,Character,specialsound,specialsound2,1,"asdj92udu92hu9uasud9u2df")
				currenttimestop = currenttimestop + 1
				local waiter = coroutine.wrap(function()
					wait(35)
					cooled3 = true
				end)
				waiter()
			--[[elseif input.KeyCode == Enum.KeyCode.T and not attacking and not charginghamon and cooled4 and workspace.timestopped.Value == false and Humanoid.Health > 0 then
				attacking = true
					cooled4 = false
					animation = 6
					keyframe = 0
					wastimestop = false
					timer = 0
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					speed = 0.095
					hit = false
					miscevent:FireServer(2,woosh,math.random(90,110)/100)
					miscevent:FireServer(1,woosh,0)]]
			elseif input.KeyCode == Enum.KeyCode.T --[[and not attacking and not charginghamon and workspace.timestopped.Value == true and workspace.timestopper.Value == Player.Name and cooled6]] and Humanoid.Health > 0 then
				attacking = true
					cooled6 = false
					animation = 6
					keyframe = 0
					timer = 0
					effecttimer = 0
					wastimestop = true
					miscevent:FireServer(7,Humanoid,0)
					speed = 0.095
					hit = false
					miscevent:FireServer(2,woosh,math.random(100,120)/100)
					miscevent:FireServer(1,woosh,0)
			elseif input.KeyCode == Enum.KeyCode.H --[[and not attacking and cooled9]] and Humanoid.Health > 0 --[[and Player:WaitForChild("IsVampire").Value == true]] then
				attacking = true
					cooled9 = false
					animation = 10
					keyframe = 0
					timer = 0
					currentbarrage = currentbarrage + 1
					local lastbarrage = currentbarrage
					local duration = coroutine.wrap(function()
						wait(4)
						if currentbarrage == lastbarrage and animation == 10 then
							timer = 0
							attacking = false
								local waiter = coroutine.wrap(function()
									wait(5)								
									cooled9 = true
								end)
							waiter()
							animation = -1
							keyframe = 0
							miscevent:FireServer(7,Humanoid,50)
							speed = 0.02
						end
					end)
					duration()
					movetimer = timer
					effecttimer = 0
					miscevent:FireServer(7,Humanoid,0)
					speed = 0.095*Player:WaitForChild("Speed").Value*allmult
					hit = false
					miscevent:FireServer(1,woosh,0)
			elseif input.KeyCode == Enum.KeyCode.Z --[[and not attacking and not charginghamon and cooledz]] and Humanoid.Health > 0 --[[Player:WaitForChild("Power").Value >= 100]] then
				cooledz = false
				
					if not summoned then
						miscevent:FireServer(2,summonstand,math.random(90,110)/100)
						miscevent:FireServer(1,summonstand,0)
						miscevent:FireServer(3,Stand.Head.face,0)
						for _,v in pairs(Stand:GetChildren()) do
							if v:IsA("BasePart") then
								local fader = coroutine.wrap(function()
									for i=1, 10 do
										miscevent:FireServer(3,v,1-(i/10))
										wait()
									end
								end)
								fader()
							end
						end
						summoned = true
					end
				
				local lookvector = Character.HumanoidRootPart.CFrame.lookVector
				local jumppower = Player:WaitForChild("Power").Value
					if jumppower > 200 then jumppower = 200 end
				miscevent:FireServer(16,Character.HumanoidRootPart,Vector3.new(lookvector.X*(30+(jumppower/2)),50+(jumppower/2),lookvector.Z*(30+(jumppower/2))))
				
				local waiter = coroutine.wrap(function()
					wait(5)
					cooledz = true
				end)
				waiter()
			elseif input.KeyCode == Enum.KeyCode.Q and (not attacking or animation == 5) and Humanoid.Health > 0 then
				if not summoned and Stand['Torso'].Transparency == 1 then
					miscevent:FireServer(2,summonstand,math.random(90,110)/100)
					miscevent:FireServer(1,summonstand,0)
					miscevent:FireServer(3,Stand.Head.face,0)
					for _,v in pairs(Stand:GetChildren()) do
						if v:IsA("BasePart") then
							local fader = coroutine.wrap(function()
								for i=1, 10 do
									miscevent:FireServer(3,v,1-(i/10))
									wait()
								end
							end)
							fader()
						end
					end
					summoned = true
				elseif summoned and Stand['Torso'].Transparency == 0 then
					miscevent:FireServer(3,Stand.Head.face,1)
					for _,v in pairs(Stand:GetChildren()) do
						if v:IsA("BasePart") then
							local fader = coroutine.wrap(function()
								for i=1, 10 do
									miscevent:FireServer(3,v,(i/10))
									wait()
								end
							end)
							fader()
						end
					end
					summoned = false
				end
			elseif input.KeyCode == Enum.KeyCode.G and not attacking and Humanoid.Health > 0 then
				attacking = true
				timer = 0
				speed = 0.04
				keepmoving = false
				miscevent:FireServer(0,menacing,true)
				miscevent:FireServer(5,Humanoid,0)
				miscevent:FireServer(7,Humanoid,0)
				animation = 5
				keyframe = math.random(0,1)
			elseif input.KeyCode == Enum.KeyCode.G and animation == 5 and Humanoid.Health > 0 then
				animation = -1
				keyframe = 0
				attacking = false
				miscevent:FireServer(0,menacing,false)
				if running then miscevent:FireServer(5,Humanoid,20) else miscevent:FireServer(5,Humanoid,16) end
				miscevent:FireServer(7,Humanoid,50)
			elseif input.KeyCode == Enum.KeyCode.X and not attacking and Humanoid.Health > 0 and not charginghamon and hamonpower == 0 and cooled7 and Player:WaitForChild("IsHamon").Value == true then
				if not summoned then
					miscevent:FireServer(2,summonstand,math.random(90,110)/100)
					miscevent:FireServer(1,summonstand,0)
					miscevent:FireServer(3,Stand.Head.face,0)
					for _,v in pairs(Stand:GetChildren()) do
						if v:IsA("BasePart") then
							local fader = coroutine.wrap(function()
								for i=1, 10 do
									miscevent:FireServer(3,v,1-(i/10))
									wait()
								end
							end)
							fader()
						end
					end
					summoned = true
				end
				charginghamon = true
				ishamon = true
				cooled7 = false
				miscevent:FireServer(0,light,true)
				miscevent:FireServer(0,glow,true)
				local waiter = coroutine.wrap(function()
					wait(15)
					cooled7 = true
				end)
				waiter()
			elseif input.KeyCode == Enum.KeyCode.LeftControl and not attacking and Humanoid.Health > 0 then
				if running then running = false miscevent:FireServer(5,Humanoid,16) if animation == 1 then speed = 0.03 end else running = true miscevent:FireServer(5,Humanoid,20) if animation == 1 then speed = 0.04 end end
			end
		elseif input.UserInputType == Enum.UserInputType.MouseButton1 and not intextbox and PlayerGui:WaitForChild("statUI"):FindFirstChild("background").Position ~= UDim2.new(0.7,0,0.06,0) then
			if --[[cooled5 and not attacking and]] Humanoid.Health > 0 --[[and not charginghamon]] then
				if not summoned then
					miscevent:FireServer(2,summonstand,math.random(90,110)/100)
					miscevent:FireServer(1,summonstand,0)
					miscevent:FireServer(3,Stand.Head.face,0)
					for _,v in pairs(Stand:GetChildren()) do
						if v:IsA("BasePart") then
							local fader = coroutine.wrap(function()
								for i=1, 10 do
									miscevent:FireServer(3,v,1-(i/10))
									wait()
								end
							end)
							fader()
						end
					end
					summoned = true
				end
				local either = math.random(0,1)
				if either == 0 then
					attacking = true
						cooled5 = false
						animation = 7
						keyframe = 0
						timer = 0
						miscevent:FireServer(7,Humanoid,0)
						effecttimer = 0
						movetimer = timer
						speed = 0.025*Player:WaitForChild("Speed").Value*allmult
						hit = false
						random3 = orig3s*CFrame.new(math.random(15,35)/70,0,0)*CFrame.Angles(math.rad(math.random(-500,-100)/100),math.rad(math.random(-3100,1200)/100),math.rad(math.random(8600,9400)/100))
				elseif either == 1 then
					attacking = true
						cooled5 = false
						animation = 8
						keyframe = 0
						timer = 0
						miscevent:FireServer(7,Humanoid,0)
						effecttimer = 0
						movetimer = timer
						speed = 0.025*Player:WaitForChild("Speed").Value*allmult
						hit = false
						random2 = orig2s*CFrame.new(math.random(-35,-15)/70,0,0)*CFrame.Angles(math.rad(math.random(-500,-100)/100),math.rad(math.random(1200,3100)/100),math.rad(math.random(-9400,-8600)/100))
				end		
			end	
		end
	end
end)

InputService.InputEnded:connect(function(input)
	if input.UserInputType == Enum.UserInputType.Keyboard then
		if input.KeyCode == Enum.KeyCode.E and animation == 3 then
			timer = 0
			attacking = false
				local waiter = coroutine.wrap(function()
					wait(2)								
					cooled1 = true
				end)
			waiter()
			miscevent:FireServer(1,ora,1)
			animation = -1
			keyframe = 0
			miscevent:FireServer(7,Humanoid,50)
			speed = 0.02
		elseif input.KeyCode == Enum.KeyCode.Y and animation == 9 then
			timer = 0
			attacking = false
				local waiter = coroutine.wrap(function()
					wait(5)
					cooled8 = true
				end)
			waiter()
			miscevent:FireServer(1,ora,1)
			animation = -1
			keyframe = 0
			miscevent:FireServer(7,Humanoid,50)
			speed = 0.02
		elseif input.KeyCode == Enum.KeyCode.H and animation == 10 then
			timer = 0
			attacking = false
				local waiter = coroutine.wrap(function()
					wait(5)								
					cooled9 = true
				end)
			waiter()
			animation = -1
			keyframe = 0
			miscevent:FireServer(7,Humanoid,50)
			speed = 0.02
		elseif input.KeyCode == Enum.KeyCode.X and not attacking and Humanoid.Health > 0 and charginghamon then	
			charginghamon = false
		end
	end
end)

Humanoid.Died:connect(function()
	if summoned then
		miscevent:FireServer(3,Stand.Head.face,1)
		for _,v in pairs(Stand:GetChildren()) do
			if v:IsA("BasePart") then
				local fader = coroutine.wrap(function()
					for i=1, 10 do
						miscevent:FireServer(3,v,(i/10))
						wait()
					end
				end)
				fader()
			end
		end
	end
end)

local cooledoof = true
local prevhealth = Humanoid.Health
Humanoid.HealthChanged:connect(function(value)
	if value < prevhealth and cooledoof then
		cooledoof = false
		local impactvar = (prevhealth - value)/Humanoid.MaxHealth
		prevhealth = value		
		
		local random = math.random(0,1)		
		
		if random == 0 then
			
			Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(22),0,math.rad(-8)) , impactvar*2)
				
			Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(5),math.rad(-2),math.rad(5)) , impactvar*2)
	
			Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(22),math.rad(5),math.rad(-32)) , impactvar*2)
		
			Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(21),math.rad(5),math.rad(33)) , impactvar*2)
		
			Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(-2),math.rad(2),math.rad(22)) , impactvar*2)
		
			Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(-2),math.rad(-2),math.rad(-22)) , impactvar*2)
				
		elseif random == 1 then
			
			Joints[1].C0 = Joints[1].C0:lerp(orig1*CFrame.Angles(math.rad(-22),0,math.rad(8)) , impactvar*2)
				
			Joints[2].C0 = Joints[2].C0:lerp(orig2*CFrame.Angles(math.rad(-5),math.rad(2),math.rad(-5)) , impactvar*2)
	
			Joints[3].C0 = Joints[3].C0:lerp(orig3*CFrame.Angles(math.rad(-22),math.rad(-5),math.rad(32)) , impactvar*2)
		
			Joints[4].C0 = Joints[4].C0:lerp(orig4*CFrame.Angles(math.rad(-21),math.rad(-5),math.rad(-33)) , impactvar*2)
		
			Joints[5].C0 = Joints[5].C0:lerp(orig5*CFrame.Angles(math.rad(2),math.rad(-2),math.rad(-22)) , impactvar*2)
		
			Joints[6].C0 = Joints[6].C0:lerp(orig6*CFrame.Angles(math.rad(2),math.rad(2),math.rad(22))	 , impactvar*2)		
			
		end
		
		wait(0.5)
		cooledoof = true
	end
end)

workspace.timestopped.Changed:connect(function(value)
	wait()
	if workspace.timestopper.Value ~= Player.Name then
		if value == true then
			Character.Torso.Anchored = true
			if woosh.IsPlaying then miscevent:FireServer(1,woosh,2) end
			if ora.IsPlaying then miscevent:FireServer(1,ora,2) end
			if singleora.IsPlaying then miscevent:FireServer(1,singleora,2) end
			if voiceline.IsPlaying then miscevent:FireServer(1,voiceline,2) end
		elseif value == false then
			Character.Torso.Anchored = false
			if woosh.IsPaused and woosh.TimePosition > 0 then miscevent:FireServer(1,woosh,3) end
			if ora.IsPaused and ora.TimePosition > 0 then miscevent:FireServer(1,ora,3) end
			if singleora.IsPaused and singleora.TimePosition > 0 then miscevent:FireServer(1,singleora,3) end
			if voiceline.IsPaused and voiceline.TimePosition > 0 then miscevent:FireServer(1,voiceline,3) end
		end
	end
end)

Player:WaitForChild("Endurance").Changed:connect(function(value)
	miscevent:FireServer(8,Humanoid,50*value*allmult)
end)

Character:WaitForChild("weakened").Changed:connect(function(value)
	if value == true then
		allmult = 0.5
	elseif value == false then
		if Player:WaitForChild("Requiem").Value == true then allmult = 1.25 else allmult = 1 end
	end
end)
