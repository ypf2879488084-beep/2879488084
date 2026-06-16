#Examples
###Callbacks
The following callbacks have no arguments:<br>

 * cb.pre_tick
 * cb.tick
 * cb.draw_first
 * cb.draw
 * cb.sprite
 
cb.draw_first is triggered before cb.sprite, while cb.draw is triggered after cb.sprite.

####cb.keydown and cb.keyup
Both have a single arg, key_code:<br>
``` lua
local function on_key_down(k)
	if k==49 then
		print('the 1 key is down')
	end
end

local function on_key_up(k)
	if k==49 then
		print('the 1 key is up')
	end
end

cb.add(cb.keydown, on_key_down)
cb.add(cb.keyup, on_key_up)
```

####cb.spell
Has a single arg, spell.obj:<br>
``` lua
local function on_process_spell(spell)
	print(spell.name, spell.owner.charName)
end

cb.add(cb.spell, on_process_spell)
```

####cb.issueorder
Has three args: order_type, pos, obj:<br>

Note that `cb.issueorder` will only work for hanbot internal request, user's manual movement/attack will not trigger this event.

``` lua
local function on_issue_order(order, pos, obj)
	if order==2 then
		print(('move order issued at %.2f - %.2f'):format(pos.x, pos.z))
	end
	if order==3 then
		print(('attack order issued to %u'):format(obj))
	end
end

cb.add(cb.issueorder, on_issue_order)
```

####cb.issue_order
just a better version of `cb.issueorder`<br>
args: `IssueOrderArgs`:<br>

 * `boolean` args.process
 * `number` args.order
 * `vec3` args.pos
 * `obj` args.target
 * `boolean` args.isShiftPressed
 * `boolean` args.isAltPressed
 * `boolean` args.shouldPlayOrderAcknowledgementSound
 * `boolean` args.isFromUser

<del>Note that `cb.issue_order` will only work for hanbot internal request, user's manual movement/attack will not trigger this event.</del><br>
Now `cb.issue_order` will be triggered for all requests (include manual click).

Warning: <br>
If you want to change the target or pos of `issue_order`, please use `orb.combat.register_f_pre_tick` and `TS.filter`, use `cb.issue_order` is not recommended, it will cause lots logic problems.

``` lua
local function on_issue_order(args)
	if args.order==2 then
		print(('move order issued at %.2f - %.2f'):format(args.pos.x, args.pos.z))
		return
	end
	
	if args.order==3 then
		print(('attack order issued to %u'):format(args.target.ptr))
		return
	end
	
	if SOME_CONDITION_1 then
		args.pos = cursorPos -- you can change any parameters
		return
	end
	
	if SOME_CONDITION_2 then
		args.process = false -- block this issue_order 
		return
	end
end

cb.add(cb.issue_order, on_issue_order)
```

####cb.castspell
Has four args: slot, startpos, endpos, nid:<br>

Note that `cb.cast_spell` will only work for hanbot internal request, user's manual cast will not trigger this event.

``` lua
local function on_cast_spell(slot, startpos, endpos, nid)
	print(('%u, %.2f-%.2f, %.2f-%.2f, %u'):format(slot, startpos.x, startpos.z, endpos.x, endpos.z, nid))
end

cb.add(cb.castspell, on_cast_spell)
```

####cb.cast_spell
just a better version of `cb.castspell` <br>
args: `CastSpellArgs`:<br>

 * `boolean` args.process
 * `number` args.spellSlot
 * `vec3` args.casterPosition
 * `vec3` args.targetPosition
 * `vec3` args.targetEndPosition
 * `obj` args.target

Note that `cb.cast_spell` will only work for hanbot internal request, user's manual cast will not trigger this event.

``` lua
local function on_cast_spell(args)
	print(('spellSlot: %u, target: %u'):format(args.spellSlot, args.target and args.target.ptr or 0))

	if SOME_CONDITION_2 then
		args.process = false -- block this cast_spell 
		return
	end
end

cb.add(cb.cast_spell, on_cast_spell)
```

####cb.attack_cancel
Fired when AA canceled

``` lua
local function on_cancel_attack(obj)
	print(('%s, cancel attack'):format(obj.charName))
end
cb.add(cb.attack_cancel, on_cancel_attack)
```

####cb.cast_finish
Fired when a spell cast is finished.

``` lua
local function on_cast_finish(spell)
	if spell.owner==player then
		print('on_cast_finish: ' .. spell.name)
	end
end
cb.add(cb.cast_finish, on_cast_finish)
```

####cb.play_animation
Fired when a animation (from network only) is begin to play.

``` lua
local function on_play_animation(obj, animation)
	print(('on_play_animation, %s, %s'):format(obj.charName, animation))
end
cb.add(cb.play_animation, on_play_animation)
```

####cb.create_minion and cb.delete_minion
Both have a single arg, minion.obj<br>
``` lua
local function on_create_minion(obj)
	print(obj.name, obj.charName)
end

local function on_delete_minion(obj)
	--obj is invalid within the scope of this function, it is dangerous to check obj properties other than .ptr
	print(obj.ptr)
end

cb.add(cb.create_minion, on_create_minion)
cb.add(cb.delete_minion, on_delete_minion)
```

####cb.create_missile and cb.delete_missile
Both have a single arg, missile.obj<br>
``` lua
local function on_create_missile(obj)
	print(obj.name, obj.speed, obj.spell.name)
end

local function on_delete_missile(obj)
	--obj is invalid within the scope of this function, it is dangerous to check obj properties other than .ptr
	print(obj.ptr)
end

cb.add(cb.create_missile, on_create_missile)
cb.add(cb.delete_missile, on_delete_missile)
```

####cb.create_particle and cb.delete_particle
Both have a single arg, base.obj<br>
``` lua
local function on_create_particle(obj)
	print(obj.name, obj.x, obj.z)
end

local function on_delete_particle(obj)
	--obj is invalid within the scope of this function, it is dangerous to check obj properties other than .ptr
	print(obj.ptr)
end

cb.add(cb.create_particle, on_create_particle)
cb.add(cb.delete_particle, on_delete_particle)
```

####cb.buff_gain and cb.buff_lose
<br>
``` lua
local function on_buff_gain(obj, buff)
	print('[Buff gain]: ', obj.charName, buff.name)
end

local function on_buff_lose(obj, buff)
	print('[Buff lose]: ', obj.charName, buff.name)
end

cb.add(cb.buff_gain, on_buff_gain)
cb.add(cb.buff_lose, on_buff_lose)
```

####cb.set_cursorpos
Don't use this callback, please use `player:castSpell('move')`
<br> 
``` lua

-- Only works for VelkozR / AurelionSolQ / YuumiQ / NunuW / SionR
local function on_cursorpos_change(point)
	print('[on_cursorpos_change]: ', point[0], point[1])
    
    -- set x and y
    local v = graphics.world_to_screen(g_target.pos)
    point[0] = v.x
    point[1] = v.y
end

cb.add(cb.set_cursorpos, on_cursorpos_change)
```

###Creating Shards
Introducing shards, a new way of binding and encrypting your folder into a single file.<br><br>
To build shards, you have to add a shard table to your header.lua, which contains all the names of your files you would use in module.load(id, name).<br>
If you build a libshard, lib = true has to be added additionally.<br>
``` lua

-- this file is also in gbk charset
local isCN = hanbot and hanbot.language == 1
local supported = {
  Ashe = true,
  Lux = true,
}

return {
  id = "some_unique_name",
  name = isCN and "你好" or "Hello",
  author = "aaa",
  description = [[]],
  shard = {
    'main', 
    'spells/q',
  },
  
  -- menu will be loaded by this order: "Champion" / "Orbwalker" / "Evade" / "Utility" / "Other"
  type = "Champion",  -- if this shard is a champion plugin
  
  -- current shard will not be loaded when "load" return failed.
  load = function ()
    return supported[player.charName]
  end
}
```
Additionally you can bind sprites into a shard by adding it's names to a resource table.<br>
The resource is shared between ALL plugins, it is better to have a unique name.<br>

``` lua
return {
  ...
  ...
  shard = {
    'main', 'spells/q',
  },
  resources = {
    'SPRITE_NAME.png', —developer/SHARD_NAME/SPRITE_NAME.png
    'SUB_FOLDER/SPRITE_NAME.png', —developer/SHARD_NAME/SUB_FOLDER/SPRITE_NAME.png
  },
  hprotect = true, -- enable the enhanced protection to protect your source code
  -- lib = true, -- build a libshard
}
```
Note that the sprite name added to the resource folder is the same as when using it ingame.<br>
``` lua
cb.add(cb.sprite, function()
  graphics.draw_sprite('SPRITE_NAME.png', vec2)
  graphics.draw_sprite('SUB_FOLDER/SPRITE_NAME.png', vec2)
end)
```
Shard builder is available in the developer group.<br>
Warning: <br>
There is no error handling for the shard builder. <br>
Make sure your script is working ingame, has a valid header and the folder name is being input correctly.<br>
Do not build shards out of scripts that already use the crypt module.<br><br>

###Avoiding Bugsplats
Variables must be properly purged, attempting to access certain obj properties after the obj has been deleted by the LoL client will result in LoL bugsplatting<br>
``` lua
local ex_obj

local function on_tick()
	if ex_obj and ex_obj.isDead then
		ex_obj = nil
	end
	--continue rest of your code
end

local function on_create_minion(obj)
	if not ex_obj then
		ex_obj = obj
	end
end

local function on_delete_minion(obj)
	if ex_obj and ex_obj.ptr==obj.ptr then
		ex_obj = nil
	end
end

cb.add(cb.tick, on_tick)
cb.add(cb.create_minion, on_create_minion)
cb.add(cb.delete_minion, on_delete_minion)
```
Do not use spell.obj outside of the spell callback.<br>
``` lua
local wrong
local correct

local function on_process_spell(spell)
	if not wrong then
		wrong = spell
	end
	if not correct then
		correct = {
			windUpTime = spell.windUpTime,
			startPos = vec3(spell.startPos),
		}
	end
end

local function on_tick()
	if wrong then
		--DO NOT DO THIS, this is very likely to lead to bugsplats!
		print(wrong.windUpTime)
	end
	
	if correct then
		--Instead, do this
		print(correct.windUpTime)
	end
end

cb.add(cb.spell, on_process_spell)
cb.add(cb.tick, on_tick)
```
Do not attempt to access obj properties other than ptr in cb.delete_minion, cb.delete_particle or cb.delete_missile.<br>
``` lua
local function on_delete_minion(obj)
	--wrong
	if obj.charName=='dontdothis' then
		--this is likely to lead to bugsplats
	end
	
	--correct, only check ptrs here
	if obj.ptr==someobj.ptr then
		someobj = nil
	end
end

local function on_delete_particle(obj)
	--wrong
	if obj.charName=='dontdothis' then
		--this is likely to lead to bugsplats
	end
	
	--correct, only check ptrs here
	if obj.ptr==someobj.ptr then
		someobj = nil
	end
end

local function on_delete_missile(obj)
	--wrong
	if obj.charName=='dontdothis' then
		--this is likely to lead to bugsplats
	end
	
	--correct, only check ptrs here
	if obj.ptr==someobj.ptr then
		someobj = nil
	end
end

cb.add(cb.create_minion, on_create_minion)
cb.add(cb.delete_particlee, on_delete_particle)
cb.add(cb.delete_missile, on_delete_missile)
```
Do not use the buffManager, use obj.buff instead.<br>

