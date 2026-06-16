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
