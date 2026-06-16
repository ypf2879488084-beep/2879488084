
#Modules
###pred
####pred.trace.linear.hardlock(input, seg, obj)
Parameters<br>
`table` input<br>
`seg` seg<br>
`obj` obj<br>
Return Value<br>
`boolean` returns true if obj is hard crowd controlled<br>
``` lua


```
####pred.trace.linear.hardlockmove(input, seg, obj)
Parameters<br>
`table` input<br>
`seg` seg<br>
`obj` obj<br>
Return Value<br>
`boolean` returns true if obj is hard crowd controlled by taunts, fears or charms<br>
``` lua

```
####pred.trace.circular.hardlock(input, seg, obj)
Parameters<br>
`table` input<br>
`seg` seg<br>
`obj` obj<br>
Return Value<br>
`boolean` returns true if obj is hard crowd controlled<br>
``` lua

```
####pred.trace.circular.hardlockmove(input, seg, obj)
Parameters<br>
`table` input<br>
`seg` seg<br>
`obj` obj<br>
Return Value<br>
`boolean` returns true if obj is hard crowd controlled by taunts, fears or charms<br>
``` lua

```
####pred.trace.newpath(obj, t1, t2)
Parameters<br>
`obj` obj<br>
`number` t1<br>
`number` t2<br>
Return Value<br>
`boolean` returns true if obj path has updated <t1 seconds ago or >t2 seconds ago<br>
``` lua

```
####pred.core.lerp(path, delay, speed)
Parameters<br>
`path.obj` path<br>
`number` delay<br>
`number` speed<br>
Return Value<br>
`vec2` returns interpolated position along path<br>
`number` returns path index of vec2<br>
`boolean` returns true if vec2 is the end of path<br>
``` lua
local pred = module.internal('pred')

local function on_tick()
	if player.path.active and player.path.count>0 then
		local res, res_i, res_b = pred.core.lerp(player.path, 0.5, player.moveSpeed)
		print(('%.2f-%.2f on index %u'):format(res.x, res.y, res_i), res_b)
	end
end

cb.add(cb.tick, on_tick)
```
####pred.core.project(pos, path, delay, projectileSpeed, pathSpeed)
Parameters<br>
`vec2` pos<br>
`path.obj` path<br>
`number` delay<br>
`number` projectileSpeed<br>
`number` pathSpeed<br>
Return Value<br>
`vec2` returns projected position along path<br>
`number` returns path index of vec2<br>
`boolean` returns true if vec2 is the end of path<br>
``` lua
local pred = module.internal('pred')

local function on_tick()
	if player.path.active and player.path.count>0 then
		local res, res_i, res_b = pred.core.project(mousePos2D, player.path, 0.5, 1200, player.moveSpeed)
		print(('%.2f-%.2f on index %u'):format(res.x, res.y, res_i), res_b)
	end
end

cb.add(cb.tick, on_tick)
```
####pred.core.project_off(pos, path, delay, projectileSpeed, pathSpeed, offset)
Parameters<br>
`vec2` pos<br>
`path.obj` path<br>
`number` delay<br>
`number` projectileSpeed<br>
`number` pathSpeed<br>
`vec2` offset<br>
Return Value<br>
`vec2` returns projected position along path<br>
`number` returns path index of vec2<br>
`boolean` returns true if vec2 is the end of path<br>
``` lua
local pred = module.internal('pred')

local function on_tick()
	if player.path.active and player.path.count>0 then
		--same as core.project, but the path is offset
		local res, res_i, res_b = pred.core.project_off(mousePos2D, player.path, 0.5, 1200, player.moveSpeed, vec2(0,100))
		print(('%.2f-%.2f on index %u'):format(res.x, res.y, res_i), res_b)
	end
end

cb.add(cb.tick, on_tick)
```
####pred.core.get_pos_after_time(obj, time)
Parameters<br>
`obj` obj<br>
`number` time<br>
Return Value<br>
`vec2` returns position of obj after time<br>
``` lua
local pred = module.internal('pred')

local function on_tick()
	local res = pred.core.get_pos_after_time(player, 0.5)
	print(('%.2f-%.2f'):format(res.x, res.y))
end

cb.add(cb.tick, on_tick)
```
####pred.linear.get_prediction(input, tar, src)
Parameters<br>
`table` input<br>
`obj` tar<br>
`obj` src [optional]<br>
Return Value<br>
`seg` returns a line segment<br>
``` lua
--this example is based on caitlyn q
local orb = module.internal('orb')
local ts = module.internal('TS')
local pred = module.internal('pred')

local pred_input = {
  delay = 0.625,
  speed = 2200,
  width = 60,
  range = 1150,
  boundingRadiusMod = 1,
  collision = {
    wall = true,
  },
}

local function trace_filter(seg, obj)
	if seg.startPos:dist(seg.endPos) > pred_input.range then return false end

  if pred.trace.linear.hardlock(pred_input, seg, obj) then
    return true
  end
  if pred.trace.linear.hardlockmove(pred_input, seg, obj) then
    return true
  end
  if pred.trace.newpath(obj, 0.033, 0.500) then
    return true
  end
end

local function target_filter(res, obj, dist)
	if dist > 1500 then return false end
	local seg = pred.linear.get_prediction(pred_input, obj)
	if not seg then return false end
	if not trace_filter(seg, obj) then return false end
	
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
