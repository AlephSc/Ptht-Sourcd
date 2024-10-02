Config = {
  Plant = {
     Delay = 0,
     ID = 0,
   },

  Harvest = {
     Delay = 0,
     ID = 0,
  },
  
  Overall = {
  Mode = "none",
  Loop = 0,
  Jump = 1,
  Repeat = 0,
  },
  
  Position = {
  	x_min = 0,
      x_max = 0,
      
      y_min = 0,
      y_max = 0,
  }

}

--[[
Config :
Mode = {
	"pt"
	"ht"
	"ptht"
	
Loop = {
	0 = infinity
    > 1 = Loop count
	}

]]

--== | Strings | ==--
--== | Str

--== | Int
S_P = 0
S_U = 0
S_H = 0
S_O = 0

--== | Bool

--== | Oth
--C=Shortcut
C_P = Config.Plant
C_H = Config.Harvest
C_O = Config.Overall
C_S = Config.Position
S = Sleep
Pkt = SendPacket
PktR = SendPacketRaw
Var = SendVariant

--== | Functions

local function r(x,y,t,v,o,f)
  s = (o ~= nil and (o ~= "" and o or false) or false)
  if (f ~= nil and f or (f:type() ~= "string" and f or false) or false) == false then
   PktR(false, {type = t, value = v, px = (s and 0 or x), py = (s and 0 or y), x = x, y = y, state = (s and v or (GetLocal().isLeft and 48 or 32))})
  else
   FindPath(x,y)
  end
end

local function l(o,g)
  Var({v1 = "OnConsoleMessage", v2 = (o ~= nil and (o ~= "" and o or "") or "") .. (g ~= nil and (g ~= "" and g or "") or "")})
end

local function GT(x,y)
   if GetWorldName() ~= "EXIT" then
    S(5)
    if GetWorldName() ~= "EXIT" then
     return GetTile(x,y)
   end
 end
 return {fg = -1, bg = -1, x = -1, y = -1, collidabel = false}
end

--== | Main Func

local function Plant()
l("`0","Planting")
 S(1000)
   for x = C_S.x_min, C_S.x_max, (C_S.x_min > C_S.x_max and C_O.Jump - C_O.Jump * 2 or C_O.Jump) do
    for y = C_S.y_min, C_S.y_max, (C_S.y_min > C_S.y_max and -1 or 1) do
     for rep = 1, C_O.Repeat do
      if GT(x,y).fg == 0 and GT(x,y+1).fg ~= 0 and GT(x,y).fg ~= C_P.ID then
      r(x*32,y*32,0,32,true)
      S(C_P.Delay)
      r(x,y,3,C_P.ID)
      S(C_P.Delay)
      end
    end
   end
  end
 S(1000)
 l("`2","Done Planting")
 S_P = S_P + 1
end

local function Uws()
  l("`0","Using UWS")
  S(500)
  Pkt(2, "action|dialog_return\ndialog_name|world_spray\n")
  S(500)
  l("`2", "Done Using UWS")
  S_U = S_U + 1
end

local function Harvest()
l("`0","Harvesting")
 S(1000)
   for x = C_S.x_min, C_S.x_max, (C_S.x_min > C_S.x_max and C_O.Jump - C_O.Jump * 2 or C_O.Jump) do
    for y = C_S.y_min, C_S.y_max, (C_S.y_min > C_S.y_max and -1 or 1) do
     for rep = 1, C_O.Repeat do
      if GT(x,y).fg == C_H.ID and GT(x,y+1).fg ~= 0 then
      r(x*32,y*32,0,32,true)
      S(C_P.Delay)
      r(x,y,3,18)
      S(C_P.Delay)
      end
    end
   end
  end
 S(1000)
 l("`2","Done Harvesting")
 S_H = S_H + 1
end

--== | Main IF


if C_O:lower() == "pt" then
   Plant()
  elseif C_O:lower() == "ht" then
   Harvest()
  elseif C_O:lower() == "ptht" then
   if C_O.Loop == 0 then
      while true do
      Plant()
      Uws()
      Harvest()
      end
   elseif C_O.Loop >= 1 then
      for nuh_uh = 1, C_O.Loop do
      Plant()
      Uws()
      Harvest()
      end
   end
end
