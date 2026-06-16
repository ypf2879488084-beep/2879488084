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

cb.add(cb.tick, on_tick)
```
####pred.circular.get_prediction(input, tar, src)
Parameters<br>
`table` input<br>
`obj` tar<br>
`obj` src [optional]<br>
Return Value<br>
`seg` returns a line segment<br>
``` lua
--this example is based on xerath w
local orb = module.internal('orb')
local ts = module.internal('TS')
local pred = module.internal('pred')

local pred_input = {
	delay = 0.75,
	radius = 275,
	speed = math.huge,
	boundingRadiusMod = 0,
}

local function trace_filter(seg, obj)
	if seg.startPos:dist(seg.endPos) > 950 then return false end

  if pred.trace.circular.hardlock(pred_input, seg, obj) then
    return true
  end
  if pred.trace.circular.hardlockmove(pred_input, seg, obj) then
    return true
  end
  if pred.trace.newpath(obj, 0.033, 0.500) then
    return true
  end
end

local function target_filter(res, obj, dist)
	if dist > 1500 then return false end
	local seg = pred.circular.get_prediction(pred_input, obj)
	if not seg then return false end
	if not trace_filter(seg, obj) then return false end
	
	res.pos = seg.endPos
	return true
end

local function on_tick()
	if player:spellSlot(1).state~=0 then return end

	
	local res = ts.get_result(target_filter)
	if res.pos then
		player:castSpell('pos', 1, vec3(res.pos.x, mousePos.y, res.pos.y))
		orb.core.set_server_pause()
		return true
	end
end

cb.add(cb.tick, on_tick)
```
####pred.present.get_source_pos(obj)
Parameters<br>
`obj` obj<br>
Return Value<br>
`vec2` returns server pos of obj<br>
####pred.present.get_prediction(input, tar, src)
Parameters<br>
`table` input<br>
`obj` tar<br>
`obj` src [optional]<br>
Return Values<br>
`vec2`<br>
``` lua
--this example is based on kindred e
local orb = module.internal('orb')
local ts = module.internal('TS')
local pred = module.internal('pred')

local pred_input = {
  delay = 0,
  radius = player.attackRange,
  dashRadius = 0,
  boundingRadiusModSource = 1,
  boundingRadiusModTarget = 1,
}

local function target_filter(res, obj, dist)
	if dist>800 then return false end
	if not pred.present.get_prediction(pred_input, obj) then return false end
	
	res.obj = obj
	return true
end

local function invoke()
	if player:spellSlot(2).state~=0 then return end
	
	local res = ts.get_result(target_filter)
	if res.obj then
		player:castSpell('obj', 2, res.obj)
		orb.core.set_server_pause()
		return true
  end
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

cb.add(cb.tick, on_tick)
```
###orb

####orb.core.akshan_should_double_attack
Return Value<br>
`boolean`<br>
``` lua
local orb = module.internal('orb')
if xxx then
    orb.core.akshan_should_double_attack = true  -- set it in your AIO logic
end
```

####orb.core.cur_attack_target
Return Value<br>
`obj` readonly, the current attack target<br>

####orb.core.cur_attack_name
Return Value<br>
`string` readonly, the current AA spell name<br>

####orb.core.cur_attack_start_client
Return Value<br>
`number` readonly, the time when current attack started, based on os.clock()<br>

####orb.core.cur_attack_start_server
Return Value<br>
`number` readonly, the server time when current attack started, based on os.clock()<br>

####orb.core.cur_attack_speed_mod
Return Value<br>
`number` readonly, the attack speed mod for current attack<br>

####orb.core.next_attack
Return Value<br>
`number` readonly, time for next attack <br>

####orb.core.next_action
Return Value<br>
`number` readonly, time for next action <br>

####orb.core.next_action
Return Value<br>
`number` readonly, time for next action <br>

####orb.core.reset()
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')
orb.core.reset() --resets the orbwalks attack cooldown
```
####orb.core.can_action()
Return Value<br>
`boolean` returns true if player can move or cast spells<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	print(orb.core.can_action() and 'can action' or 'can not action')
end

cb.add(cb.tick, on_tick)
```
####orb.core.can_move()
Return Value<br>
`boolean` returns true if player can move<br>
####orb.core.can_attack()
Return Value<br>
`boolean` returns true if player can attack<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	print(orb.core.can_attack() and 'can attack' or 'can not attack')
end

cb.add(cb.tick, on_tick)
```
####orb.core.can_cast_spell(spellSlot, ignore_can_action_check)
Return Value<br>
`boolean` returns true if player can cast spell<br>
####orb.core.is_paused()
Return Value<br>
`boolean` returns true if the orb is paused (will not issue any orders)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	print(orb.core.is_paused() and 'is paused' or 'is not paused')
end

cb.add(cb.tick, on_tick)
```
####orb.core.is_move_paused()
Return Value<br>
`boolean` returns true if the orb movement is paused (will not issue move orders)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	print(orb.core.is_move_paused() and 'move is paused' or 'move is not paused')
end

cb.add(cb.tick, on_tick)
```
####orb.core.is_attack_paused()
Return Value<br>
`boolean` returns true if the orb attacks are paused (will not issue attack orders)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	print(orb.core.is_attack_paused() and 'attack is paused' or 'attack is not paused')
end

cb.add(cb.tick, on_tick)
```

####orb.core.is_spell_locked()
Return Value<br>
`boolean` returns true if spells are paused <br>

####orb.core.is_winding_up_attack()
Return Value<br>
`boolean` returns true if winding up <br>

####orb.core.set_pause(t)
Parameters<br>
`number` t<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_process_spell(spell)
	if spell.owner==player and spell.name=='AnnieQ' then
		orb.core.set_pause(0.25)
	end
end

cb.add(cb.spell, on_process_spell)
```
####orb.core.set_pause_move(t)
Parameters<br>
`number` t<br>
Return Value<br>
`void`<br>
####orb.core.set_pause_attack(t)
Parameters<br>
`number` t<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_process_spell(spell)
	if spell.owner==player and spell.name=='XayahR' then
		orb.core.set_pause_attack(1.5)
	end
end

cb.add(cb.spell, on_process_spell)
```
####orb.core.set_server_pause()
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
  if orb.core.is_paused() or not orb.core.can_action() or orb.core.is_move_paused() then return end
	
	if player:spellSlot(0).state~=0 then return end
	player:castSpell('pos', 0, mousePos)
	orb.core.set_server_pause()
end

cb.add(cb.tick, on_tick)
```
####orb.core.set_server_pause_attack()
Return Value<br>
`void`<br>

####orb.core.set_pause_spell_lock()
Return Value<br>
`void`<br>

####orb.core.set_server_pause_spell_lock()
Return Value<br>
`void`<br>

####orb.core.set_pause_strict_limitation(t)
The anti-disconnect feature of orbwalker in CN region is based on facing direction, while during some special spell casting like MelQ, facing direction will be changed very quickly. So we add this API to pause the strict anti-disconnect feature<br> 
But shits anti-cheat in CN will not fix this. <b>You maybe got banned/kicked out from game by pause this feature</b>, and which is also the reason why normal players are banned (like VarusQ).<br> 

Parameters<br>
`number` t<br>
Return Value<br>
`void`<br>

####orb.core.on_after_attack(callback)
Parameters<br>
`function` callabck<br>
Register a callback, which will be triggered once after a attack windup.
####orb.core.on_player_attack(callback)
Parameters<br>
`function` callabck<br>
Register a callback, which will be triggered when a attack is responsed by server
####orb.core.on_advanced_after_attack(callback)
Parameters<br>
`function` callabck<br>
Register a callback, which will be triggered when last attack is finished and could action now (called continuously after windup until attack ready again).
####orb.core.time_to_next_attack()
Return Value<br>
`number` the left seconds to issue next attack<br>
####orb.core.is_waiting_for_server_response(spellSlot)
Return Value<br>
`boolean`<br>
####orb.core.is_waitting_for_cooldown(spellSlot)
Return Value<br>
`boolean`<br>

####orb.combat.is_active()
Return Value<br>
`boolean` returns true if combat mode is active<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
  if orb.combat.is_active() then
		print('combat active')
	end
end

cb.add(cb.tick, on_tick)
```
####orb.combat.target
Return Value<br>
`hero.obj` the current attack hero (valid only for current tick)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
  if orb.combat.is_active() and your_logic() then
    orb.combat.target = your_logic_target()
  end
end

cb.add(cb.tick, on_tick)
```
####orb.combat.pos
Return Value<br>
`hero.obj` the prefer position (valid only for current tick) will orbwalker to<br>

####orb.combat.get_target()

####orb.combat.set_target(t)

####orb.combat.get_pos()

####orb.combat.set_pos(t)

####orb.combat.get_active()

####orb.combat.set_active(t)

####orb.combat.register_f_pre_attack(func)
Parameters<br>
`function` func<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_pre_attack()
  print('will attack', orb.combat.target)
  -- you can set to new target
  -- orb.combat.target = xxxx
end

orb.combat.register_f_pre_attack(on_pre_attack)
```
####orb.combat.register_f_after_attack(func)
Parameters<br>
`function` func<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_after_attack()
  print('attack is on cooldown')
  -- you can return true to block other callbacks (Like callbacks registered by other plugin/module)
  -- return true 
  
  -- [on_after_attack] is called continuously, set bool to false can stop subsequent calls for the current attack.
  -- orb.combat.set_invoke_after_attack(bool) 
end

orb.combat.register_f_after_attack(on_after_attack)
```
####orb.combat.register_f_out_of_range(func)
Parameters<br>
`function` func<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function out_of_range()
  print('there is no target in aa range')
  -- you can return true to block other callbacks
  -- return true 
end

orb.combat.register_f_out_of_range(out_of_range)
```
####orb.combat.register_f_pre_tick(func)
Parameters<br>
`function` func<br>
Return Value<br>
`void`<br>
``` lua
local orb = module.internal('orb')

local function on_tick() --this fucntion is triggered prior to the orbs tick
  -- you can return true to block other callbacks
  -- return true 
end

orb.combat.register_f_pre_tick(on_tick)
```
####orb.combat.set_invoke_after_attack(val)
Parameters<br>
`boolean` val<br>
Return Value<br>
`void`<br>

set to false, then orb will stop triggering \[register_f_after_attack\] events

``` lua
local orb = module.internal('orb')

local function after_attack()
  print('attack is on cooldown')
  orb.combat.set_invoke_after_attack(false)
  -- you can return true to block other callbacks
  -- return true 
end

orb.combat.register_f_after_attack(after_attack)
```

####orb.farm.clear_target
Return Value<br>
`obj` the orbs current lane clear target<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
  if orb.farm.clear_target then
		print(orb.farm.clear_target.charName)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.lane_clear_wait()
Return Value<br>
`boolean` returns true if the orb is currently waiting to attack a minion that is soon to die (or waiting for siege)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
  if orb.farm.lane_clear_wait() then
		print('lane clear is waiting to attack a minion')
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.lane_clear_wait_target
Return Value<br>
`obj` the orbs current lane clear wait target<br>

####orb.farm.predict_hp(obj, time)
Parameters<br>
`minion.obj` obj<br>
`number` time<br>
Return Value<br>
`number` returns the minions health after time (seconds)<br>
``` lua
local orb = module.internal('orb')

local function on_tick()
	for i=0, objManager.minions.size[TEAM_ENEMY]-1 do
		local obj = objManager.minions[TEAM_ENEMY][i]
		if obj.isVisible then
			local hp = orb.farm.predict_hp(obj, 0.25)
			print(obj.charName, obj.health, hp)
		end
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.set_ignore(obj, time)
Parameters<br>
`minion.obj` obj<br>
`number` time<br>
Return Value<br>
`void`<br>
####orb.farm.skill_farm_linear(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on mundo q
local orb = module.internal('orb')
local input = {
	delay = 0.25,
	speed = 2000,
	width = 60,
	boundingRadiusMod = 1,
	range = 1050,
	collision = {
		minion=true,
		walls=true,
		hero=true,
	},
	damage = function(m)
		local q_level = player:spellSlot(0).level
		return math.min(250 + 50*q_level, math.max(30 + 50*q_level, m.health*(.125 + .025*q_level)))
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_farm_linear(input)
	if seg then
		player:castSpell('pos', 0, seg.endPos)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.skill_clear_linear(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on mundo q
local orb = module.internal('orb')
local input = {
	delay = 0.25,
	speed = 2000,
	width = 60,
	boundingRadiusMod = 1,
	range = 1050,
	collision = {
		minion=true,
		walls=true,
		hero=true,
	},
	damage = function(m)
		local q_level = player:spellSlot(0).level
		return math.min(250 + 50*q_level, math.max(30 + 50*q_level, m.health*(.125 + .025*q_level)))
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_clear_linear(input)
	if seg then
		player:castSpell('pos', 0, seg.endPos)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.skill_farm_circular(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on karthus q
local orb = module.internal('orb')
local input = {
	delay = 0.75,
	speed = math.huge,
	radius = 200,
	boundingRadiusMod = 0,
	range = 874,
	damage = function(m)
		return 20*player:spellSlot(0).level + 30 + .3*(player.flatMagicDamageMod*player.percentMagicDamageMod)
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_farm_circular(input)
	if seg then
		player:castSpell('pos', 0, seg.endPos)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.skill_clear_circular(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on karthus q
local orb = module.internal('orb')
local input = {
	delay = 0.75,
	speed = math.huge,
	radius = 200,
	boundingRadiusMod = 0,
	range = 874,
	damage = function(m)
		return 20*player:spellSlot(0).level + 30 + .3*(player.flatMagicDamageMod*player.percentMagicDamageMod)
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_clear_circular(input)
	if seg then
		player:castSpell('pos', 0, seg.endPos)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.skill_farm_target(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on pantheon q (****2019 version****)
local orb = module.internal('orb')
local input = {
	delay = 0.25,
	speed = 1500,
	range = 468,
	damage = function(target)
		return 35 + 40*player:spellSlot(0).level + 1.4*((player.baseAttackDamage + player.flatPhysicalDamageMod)*player.percentPhysicalDamageMod - player.baseAttackDamage)
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_farm_target(input)
	if obj then
		player:castSpell('obj', 0, obj)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.skill_clear_target(input)
Parameters<br>
`table` input<br>
Return Value<br>
`seg` returns a line segment<br>
`minion.obj` returns the minion object<br>
``` lua
--based on pantheon q
local orb = module.internal('orb')
local input = {
	delay = 0.25,
	speed = 1500,
	range = 468,
	damage = function(target)
		return 35 + 40*player:spellSlot(0).level + 1.4*((player.baseAttackDamage + player.flatPhysicalDamageMod)*player.percentPhysicalDamageMod - player.baseAttackDamage)
	end,
}

local function on_tick()
	local seg, obj = orb.farm.skill_clear_target(input)
	if obj then
		player:castSpell('obj', 0, obj)
	end
end

cb.add(cb.tick, on_tick)
```
####orb.farm.set_clear_target(obj)
Parameters<br>
`minion.obj` obj<br>
Return Value<br>
`void`<br>
####orb.utility.get_missile_speed(obj)
Parameters<br>
`obj` obj<br>
Return Value<br>
`number` returns the obj attack missile speed<br>
####orb.utility.get_wind_up_time(obj)
Parameters<br>
`obj` obj<br>
Return Value<br>
`number` returns the obj attacks wind up time<br>
####orb.utility.get_damage_mod(obj)
Parameters<br>
`obj` obj<br>
Return Value<br>
`number` returns the obj damage mod (wards ex)<br>
####orb.utility.get_damage(source, target, add_bonus)
Parameters<br>
`obj` source<br>
`obj` target<br>
`boolean` add_bonus<br>
Return Value<br>
`number` returns attack damage done to target by source<br>
####orb.utility.get_hit_time(source, target)
Parameters<br>
`obj` source<br>
`obj` target<br>
Return Value<br>
`number` returns time in seconds for an attack from source to hit target<br>
####orb.ts
Return Value<br>
`TS` returns the orbs target selector instance<br>
####orb.menu.combat.key:get()
Return Value<br>
`boolean` returns true if combat mode is active<br>
####orb.menu.lane_clear.key:get()
Return Value<br>
`boolean` returns true lane clear mode is active<br>
####orb.menu.last_hit.key:get()
Return Value<br>
`boolean` returns true last hit mode is active<br>
####orb.menu.hybrid.key:get()
Return Value<br>
`boolean` returns true if hybrid mode is active<br>


###evade
use os.clock()<br>
####evade.core.set_server_pause()
Return Value<br>
`void`<br>

this is deprecated, use `evade.core.set_pause` instead

####evade.core.set_pause(t)
Parameters<br>
`number` t<br>
Return Value<br>
`void`<br><br>
pauses evade from issuing movement orders (will still update orbs path)<br>
``` lua
local evade = module.seek('evade')
if evade then
	evade.core.set_pause(3) --pauses the evade from taking action for 3 seconds
end
```
####evade.core.is_paused()
Return Value<br>
`boolean` returns true if evade is currently paused<br>
####evade.core.is_active()
Return Value<br>
`boolean` returns true if evade is currently evading a spell<br><br>
should be checked before casting any movement impairing spells<br>
####evade.core.is_action_safe(v1, speed, delay)
Parameters<br>
`vec2\vec3` v1<br>
`number` speed<br>
`number` delay<br>
Return Value<br>
`boolean` returns true if action is safe<br>
``` lua
--this example is based on vayne q
local evade = module.seek('evade')

local function on_tick()
	if player:spellSlot(0).state~=0 then return end
	
	local pos = player.path.serverPos2D + (mousePos2D - player.path.serverPos2D):norm()*300
	if evade and evade.core.is_action_safe(pos, 500 + player.moveSpeed, 0) then
		player:castSpell('pos', 0, vec3(pos.x, mousePos.y, pos.y))
	end
end

cb.add(cb.tick, on_tick)	
```

####evade.core.get_anchor()
Return Value<br>
`void` returns the anchor for current evading direction<br>

####evade.core.get_pos()
Return Value<br>
`void` returns the target position of current evading<br>

####evade.damage
<br>
``` lua
local ad_damage, ap_damage, true_damage, buff_list = evade.damage.count(player)
--these are reduced/modified by armor/buffs
--buff_list contains an array of all incoming buff types
```

####evade.core.skillshots
<br>
Not recommended, prefer `evade.core.register_on_create_spell`
``` lua
for i=evade.core.skillshots.n, 1, -1 do
  local spell = evade.core.skillshots[i]
  --spell.name
  --spell.start_time -- based on os.clock()
  --spell.end_time -- based on os.clock()
  --spell.owner
  --spell.danger_level
  --spell.start_pos
  --spell.end_pos
  --spell.damage -- totalDamage
  --spell.data -- assorted static data
  --spell:contains(pos2D/obj)
  --spell:get_hit_time(pos2D)
  --spell:get_hit_remaining_time(pos2D)
  --spell:get_damage(target)
  
  local ad_damage,ap_damage,true_damage,buff_list = spell:get_damage(player)
  
  if spell:contains(game.mousePos2D) then
    --mouse is inside of 'spell'
  end
  
  if spell:contains(player) then
    --player is inside of 'spell', this accounts for obj boundingRadius
  end
  
  if spell:intersection(player.pos2D, game.mousePos2D) then
    --line seg player->mousePos intersects 'spell'
  end
end
```

####evade.core.skillshots[i].data
Static metadata object (read-only). Available on `evade.core.skillshots[i].data` and `evade.core.targeted[i].data`.
This attribute is updated to Evade3 [`spelldata.obj`](#objects-spelldataobj-evade3)
``` lua
local d = spell.data
-- d.name : string
-- d.menu_name : string
-- d.slot : integer
-- d.spell_type : string
-- d.missile_names (removed)
-- d.delay : number (seconds)
-- d.length : number
-- d.radius / d.width : number
-- d.speed : number
-- d.fixed_range : boolean
-- d.is_cc : boolean
-- d.update : boolean (can change postion or not, for example the Orianna R)
-- d.applies_on_hit : boolean (is a missile)
-- d.add_bbox_length : boolean (range/length)
-- d.add_bbox_radius : boolean
-- d.add_bbox_width : boolean
-- d.collision : integer (bitmask)
-- function d:damage(source, target) -> ad, ap, true, buff_or_nil
```
Notes:
- `radius` and `width` are aliases for hit width/radius.
- `add_bbox_length`/`add_bbox_radius`/`add_bbox_width` control whether target hitbox is included in distance/width calculations.
- `collision` is a bitmask of collision types.
- The 4th return of `d:damage(source, target)` is the first related buff or `nil`; for a full buff list, use `spell:get_damage`.

####evade.core.targeted
<br>
Not recommended, prefer `evade.core.register_on_create_spell`
``` lua
for i=evade.core.targeted.n, 1, -1 do
  local spell = evade.core.targeted[i]
  --spell.name
  --spell.start_time
  --spell.end_time
  --spell.owner
  --spell.target
  --spell.missile
  --spell.data -- assorted static data
end
```

####evade.core.register_on_create_spell
<br>
``` lua
evade.core.register_on_create_spell(function (skillshot)

  if not skillshot:contains(player) then
    return
  end

  local ad_damage,ap_damage,true_damage,buff_list = skillshot:get_damage(player) -- show damage to self
  print('create skillshot: ', 
    skillshot.name, 
    skillshot.owner and skillshot.owner.charName or "nil", 
    "time: ",
    string.format("%.2f", skillshot.start_time), 
    string.format("%.2f", skillshot.end_time), -- This is only an approximate time
    "target: ",
    skillshot.target and skillshot.target.charName or "nil",
    "damage: ",
    ad_damage,ap_damage,true_damage,#buff_list
  )
  
  -- example for anti ViR:
  if skillshot.name == "ViR" then
    delay_action(skillshot.end_time - os.clock() - 0.1, function() use_zhonya() end)
  end
  
end)
```

####evade.damage.count
``` lua
local ad_damage, ap_damage, true_damage, buff_list = evade.damage.count(player)
```

###damagelib

####damagelib.handlers
Insert your own handlers if internal damagelib is not ok.<br>

``` lua
local damagelib = module.internal('damagelib')
local handlers = damagelib.handlers

local FlashFrost = game.spellhash('FlashFrost')
local TotalPassthroughDamage = game.fnvhash('TotalPassthroughDamage')
local TotalExplosionDamage = game.fnvhash('TotalExplosionDamage')

handlers[FlashFrost] = function (source, target, is_raw_damage, stage)
	print('FlashFrost: lua handlers called')
	local spell_slot = source:spellSlot(0)
	if not spell_slot then
		return damage_result(0, 0, 0)
	end
	local raw_damage = spell_slot:calculate(0, TotalPassthroughDamage) + spell_slot:calculate(0, TotalExplosionDamage)
	if is_raw_damage or not target or not target.valid then
		return damage_result(0, raw_damage, 0)
	end
	
	-- return damage: ad,ap,true
	return damage_result(0, damagelib.calc_magical_damage(source, target, raw_damage), 0)
end


-- print damage
local total_damage, ad_damage, ap_damage, true_damage = damagelib.get_spell_damage('FlashFrost', 0, player, g_target, true, 0)
print(total_damage, ad_damage, ap_damage, true_damage)

```

####damagelib.get_spell_damage(spellName, spellSlot, source, target, isRawDamage, stage)
Parameters<br>
`string` spellName<br>
`number` spellSlot<br>
`obj` source<br>
`obj` target<br>
`boolean` isRawDamage, true = only spell damage, false = include runes/items/buffs/armors/shieds<br>
`number` stage<br>
Return Value<br>
`number`,`number`,`number`,`number` total,ad,ap,true<br>


``` lua
local damagelib = module.internal('damagelib')

-- Briar
print('Passive min', damagelib.get_spell_damage('BriarP', 63, player, g_target, false, 0))
print('Passive max', damagelib.get_spell_damage('BriarP', 63, player, g_target, false, 1))
print('Q', damagelib.get_spell_damage('BriarQ', 0, player, g_target, false, 0))
print('W', damagelib.get_spell_damage('BriarW', 1, player, g_target, false, 0))
print('W2', damagelib.get_spell_damage('BriarWAttackSpell', 1, player, g_target, false, 0)) -- available when W2 ready
print('E', damagelib.get_spell_damage('BriarE', 2, player, g_target, false, 0))
print('R', damagelib.get_spell_damage('BriarR', 3, player, g_target, false, 0))

```

####damagelib.calc_aa_damage(source, target, includeOnHit)
Calc the real damage after shields, etc.<br>
Parameters<br>
`obj` source<br>
`obj` target<br>
`boolean` include `calc_on_hit_damage` or not<br>
Return Value<br>
`number`<br>

####damagelib.calc_physical_damage(source, target, rawDamage)
Calc the real damage after shields, etc.<br>
Parameters<br>
`obj` source<br>
`obj` target<br>
`number` rawDamage<br>
Return Value<br>
`number`<br>

####damagelib.calc_magical_damage(source, target, rawDamage)
Calc the real damage after shields, etc.<br>
Parameters<br>
`obj` source<br>
`obj` target<br>
`number` rawDamage<br>
Return Value<br>
`number`<br>

####damagelib.calc_on_hit_damage(source, target, isAutoAttack)
Calc the extra on hit damage by passive/buffs/items/perks.<br>
Parameters<br>
`obj` source<br>
`obj` target<br>
`boolean` isAutoAttack<br>
Return Value<br>
`number`,`number`,`number`,`number`  total,ad,ap,true<br>

```lua
local total_damage,ad_damage,ap_damage,true_damage = damagelib.calc_on_hit_damage(player, target, true)
```


###TS
####TS.get_result(func, filter, ign_sel, hard)
Parameters<br>
`function` func<br>
`table` filter[optional]<br>
`boolean` ign_sel[optional]<br>
`boolean` hard[optional]<br>
Return Value<br>
`table`<br>
``` lua
--this example is based on annie q
local ts = module.internal('TS')
local pred = module.internal('pred')
local input = {
  delay = 0,
  radius = 505,
  dashRadius = 0,
  boundingRadiusModSource = 1,
  boundingRadiusModTarget = 1,
}

local function ts_filter(res, obj, dist)
	--return false for any objects much too far away
	if dist > 800 then return false end
	
	--pred.present.get_prediction checks that obj is in range for q
	if pred.present.get_prediction(input, obj) then
		--res.obj is arbitrary and could be named anything
		--additionally, anything you like can be added to the res table
		res.obj = obj
		return true
	end
end

local function on_tick()
	--check that q is ready
	if player:spellSlot(0).state~=0 then return end

	--ts.get_result loops through all valid enemies
	--simple usage
	local res = ts.get_result(ts_filter)
	if res.obj then
		player:castSpell('obj', 0, res.obj)
	end
	
	--alternative usages
	local res = ts.get_result(ts_filter, ts.filter_set[2]) --uses filter LESS_CAST_AD_PRIO (overrides menu)
	local res = ts.get_result(ts_filter, nil, true) --ignores ts selected target
	local res = ts.get_result(ts_filter, nil, nil, true) --forces ts selected target to be returned (overrides menu)
end

cb.add(cb.tick, on_tick)
```
####TS.get_active_filter()
Return Value<br>
`table`<br>
``` lua
local ts = module.internal('TS')
print(ts.get_active_filter().name)
```
####TS.loop(func, filter)
Parameters<br>
`function` func<br>
`table` filter[optional]<br>
Return Value<br>
`table`<br>
``` lua
local ts = module.internal('TS')

local function loop_filter(res, obj, dist)
	-- any condition can be set here
	if dist < 800 then
		table.insert(res, obj)
	end
end

local function on_tick()
	local res = ts.loop(loop_filter)
	--res will contain all valid enemies within 800 units
end

cb.add(cb.tick, on_tick)
```
####TS.loop_allies(func, filter)
Parameters<br>
`function` func<br>
`table` filter[optional]<br>
Return Value<br>
`table`<br>
``` lua
local ts = module.internal('TS')

local function loop_filter(res, obj, dist)
	-- any condition can be set here
	if dist < 800 then
		table.insert(res, obj)
	end
end

local function on_tick()
	local res = ts.loop_allies(loop_filter)
	--res will contain all valid allies within 800 units
end

cb.add(cb.tick, on_tick)
```
####TS.filter.new()
Return Value<br>
`table`<br>
``` lua
local ts = module.internal('TS')

local my_filter = ts.filter.new()
my_filter.name = 'LEAST_MANA'
my_filter.rank = {0.33, 0.66, 1.0, 1.33, 1.66} --these correspond to character priorities set in the menu, the lower the ratio the higher priority will be given
my_filter.index = function(obj, rank_val)
	return obj.par
	--alternatively, this will return the target with the least mana adjusted by priority
	-- return obj.par * rank_value
end

local function ts_filter(res, obj, dist)
	if dist < 800 then
		res.obj = obj
		return true
	end
end

local res = ts.get_result(ts_filter, my_filter)
```
####TS.filter_set
Return Value<br>
`table`<br>
``` lua
local ts = module.internal('TS')
for Nebelwolfi=1, #ts.filter_set do
	print(ts.filter_set[Nebelwolfi].name)
end
```
####TS.selected
Return Value<br>
`obj` current selected obj<br>

