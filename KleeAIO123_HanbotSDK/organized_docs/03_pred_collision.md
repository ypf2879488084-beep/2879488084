end
```
####pred.collision.get_prediction(input, pred_result, ign_obj)
Parameters<br>
`table` input<br>
`seg` pred_result<br>
`obj` ign_obj [optional]<br>
Return Values<br>
`table` returns a table of objects that pred_result will collide with or nil if no collision is detected<br>
``` lua 
--this example is based on morgana q
local orb = module.internal('orb')
local ts = module.internal('TS')
local pred = module.internal('pred')

local pred_input = {
  delay = 0.25,
  speed = 1200,
  width = 70,
  boundingRadiusMod = 1,
  range = 1100,
  collision = {
    minion = true, --checks collision for minions
    hero = false, --no need to check for hero collision

    -- checks all collisions: YasuoWall/SamiraWall/BraumWall/PantheonWall/MelWall
    wall = true, 

    -- or checks specific collisions
    -- wall = { yasuo = true, samira = true, braum = false, pantheon = false, mel = false },
  },
}

local function trace_filter(seg, obj, dist)
	if seg.startPos:dist(seg.endPos) > pred_input.range then
		return false
	end
  if pred.trace.newpath(obj, 0.033, 0.500) and dist < 600 then
		return true
  end
  if pred.trace.linear.hardlock(pred_input, seg, obj) then
    return true
  end
  if pred.trace.linear.hardlockmove(pred_input, seg, obj) then
    return true
  end
end

local function target_filter(res, obj, dist)
	if dist > pred_input.range then return false end
	local seg = pred.linear.get_prediction(pred_input, obj)
	if not seg then return false end
	if not trace_filter(seg, obj, dist) then return false end
	--pass obj as third arg, it will then be ignored from collision checks
	if pred.collision.get_prediction(pred_input, seg, obj) then return false end
	
	res.pos = seg.endPos
	return true
end

local function on_tick()
  if player:spellSlot(0).state~=0 then return end

  local res = ts.get_result(target_filter)
  if res.pos then
    player:castSpell('pos', 0, vec3(res.pos.x, mousePos.y, res.pos.y))
    orb.core.set_server_pause()
    return true
  end
end

