#Libraries
###hanbot
####hanbot.path
Return Value<br>
`string` returns hanbots working directory
####hanbot.luapath
Return Value<br>
`string` returns directory of non-shard scripts
####hanbot.libpath
Return Value<br>
`string` returns directory of community libraries
####hanbot.shardpath
Return Value<br>
`string` returns directory of shards
####hanbot.hwid
Return Value<br>
`string` returns current users hwid
####hanbot.user
Return Value<br>
`string` returns current users id
####hanbot.language
Return Value<br>
`number` returns language id
###cb
Enums:<br>

 * cb.draw_first  (cb.draw2)
 * cb.sprite      (cb.draw_sprite)
 * cb.draw
 * cb.draw_world
 * cb.draw_under_hud
 * cb.tick
 * cb.pre_tick
 * cb.spell
 * cb.keyup
 * cb.keydown
 * cb.issueorder
 * cb.issue_order
 * cb.castspell
 * cb.cast_spell
 * cb.attack_cancel
 * cb.cast_finish
 * cb.play_animation
 * cb.delete_minion
 * cb.create_minion
 * cb.delete_particle
 * cb.create_particle
 * cb.delete_missile
 * cb.create_missile
 * cb.buff_gain
 * cb.buff_lose
 * cb.path
 * cb.set_cursorpos
 * cb.error


#### drawing order:
cb.draw_world (game pipeline) -> <br>
cb.draw_mouse_overs (game pipeline) -> <br>
cb.draw_under_hud (game pipeline) -> <br>
cb.draw_first (hanbot pipeline) -> <br>
cb.draw_sprite (hanbot pipeline) -> <br>
cb.draw (hanbot pipeline)

* ALWAYS prepare your drawings in cb.tick, DONT do too much calculations in drawing callback
* The `draw_world`/`draw_mouse_overs`/`draw_under_hud` pipelines will be combined to hanbot pipeline if `obs_bypass` is enabled in core menu.
 
####cb.add(t, f)
Parameters<br>
`number` t<br>
`function` f<br>
Return Value<br>
`void`
``` lua
local tick_n = 0
local function on_tick()
	tick_n = tick_n + 1
	print(tick_n)
end

cb.add(cb.tick, on_tick)
```

####cb.remove(f)
Parameters<br>
`function` f<br>
Return Value<br>
`void`
``` lua
local tick_n = 0
local function on_tick()
	tick_n = tick_n + 1
	if tick_n == 10 then
		print('removed')
		cb.remove(on_tick)
	end
end

cb.add(cb.tick, on_tick)
```

###chat
####chat.isOpened
Return Value<br>
`boolean` returns true if chat is open
####chat.size
Return Value<br>
`number` returns number in chat history
####chat.clear()
Clear the send buffer<br>
Parameters<br>
Return Value<br>
`void`<br>
####chat.add(str, style)
Parameters<br>
`string` str in UTF8<br>
`table` style <br>
Return Value<br>
`void`<br>
####chat.send(str)
Parameters<br>
`string` str in UTF8<br>
Return Value<br>
`void`<br>

```lua
chat.clear()
chat.add("hello", {bold = false, italic = false, color = 'ffffffff'})
chat.add("world", {bold = true, italic = true, color = '99999999'})
chat.print()
```

####chat.print(str)
Parameters<br>
`string` str in UTF8<br>
Return Value<br>
`void`<br>

```lua
chat.print("hello world")
```

####chat.message(index)
Parameters<br>
`number` index<br>
Return Value<br>
`string`<br>

```lua
for i=0,chat.size-1 do
    print(chat.message(i))
end
```
###console
####console.set_color(c)
Parameters<br>
`number` c<br>
Return Value<br>
`void`<br>
####console.printx(str, c)
Parameters<br>
`string` str<br>
`number` c<br>
Return Value<br>
`void`<br>
###minimap
####minimap.x
Return Value<br>
`number` returns the screen x pos of the upper left corner of the minimap<br>
####minimap.y
Return Value<br>
`number` returns the screen y pos of the upper left corner of the minimap<br>
####minimap.width
Return Value<br>
`number` returns the screen width of the minimap<br>
####minimap.height
Return Value<br>
`number` returns the screen height of the minimap<br>
####minimap.bounds
Return Value<br>
`vec2` returns the maximum map boundaries<br>
####minimap.world_to_map(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`vec2` returns the screen pos of v1 on the minimap<br>
``` lua
local v1 = player.pos
local a = minimap.world_to_map(v1)
a:print()
```
####minimap.on_map(v1)
Parameters<br>
`vec2` v1<br>
Return Value<br>
`boolean` returns true if v1 is hovering the minimap<br>
``` lua
local v1 = game.cursorPos
local a = minimap.on_map(v1)
print(a)
```
####minimap.on_map_xy(x, y)
Parameters<br>
`number` x<br>
`number` y<br>
Return Value<br>
`boolean` returns true if (x, y) is hovering the minimap<br>
``` lua
local x = game.cursorPos.x
local y = game.cursorPos.y
local a = minimap.on_map_xy(x, y)
print(a)
```
####minimap.draw_circle(v1, r, w, c, n)
Parameters<br>
`vec3` v1<br>
`number` r<br>
`number` w<br>
`number` c<br>
`number` n<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	local v1 = player.pos
	local radius = 1000
	local line_width = 1
	local color = 0xFFFFFFFF
	local points_n = 16
	minimap.draw_circle(v1, radius, line_width, color, points_n)
end

cb.add(cb.draw, on_draw)
```
###ping
Enums:<br>

 * ping.ALERT
 * ping.DANGER
 * ping.MISSING_ENEMY
 * ping.ON_MY_WAY
 * ping.RETREAT
 * ping.ASSIST_ME
 * ping.AREA_IS_WARDED
 
####ping.send(vec3 pos [, number ping_type [, obj target]])
Parameters<br>
`vec3` pos<br>
`number` ping_type<br>
`game.obj` obj<br>
Return Value<br>
`void` <br>
####ping.recv(vec3 pos [, number ping_type [, obj target]])
Parameters<br>
`vec3` pos<br>
`number` ping_type<br>
`game.obj` obj<br>
Return Value<br>
`void` <br>

###navmesh
####navmesh.getTerrainHeight(x, z)
Parameters<br>
`number` x coordinate<br>
`number` z coordinate<br>
Return Value<br>
`number` returns terrain height at x,z<br>

####navmesh.isGrass(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`boolean` returns true if v1 is in grass<br>

####navmesh.isWater(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`boolean` returns true if v1 is in water<br>

####navmesh.isWall(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`boolean` returns true if v1 is a wall<br>

####navmesh.isStructure(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`boolean` returns true if v1 is a structure<br>

####navmesh.isInFoW(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`boolean` returns true if v1 is in fog of war<br>

####navmesh.getNearstPassable(v1)
deprecated, please use `player:getPassablePos` instead<br>
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`vec2` returns the nearst passable position (the cell start) vec2(x,z) to v1(x, z)<br>
`bool` returns the nearst passable is grass or not<br>

```lua
local drop_pos = navmesh.getNearstPassable(mousePos) -- return type is vec2
graphics.draw_circle(vec3(drop_pos.x + 25, 0, drop_pos.y + 25), 4, 2, 0xFFFFFF00, 3)
```

####navmesh.calcPos(obj, targetPos, strips)
Parameters<br>
`obj` hero/minion <br>
`vec3` destination <br>
`table` strips (shape of obstacle area) <br>
Return Value<br>
`vec3[]` returns array of paths<br>
`number` returns array length<br>

```lua

local g_strips = {}

function check_spell_area()
	local collision_size = 4
	local collision_array = vec3.array(collision_size)
	
	-- push areas, and please note that the minimum unit for collision checking is cell.
	-- You need to round up points to cell boundings in real situations.
	collision_array[0] = vec3(1000, 0, 1000)
	collision_array[1] = vec3(1000, 0, 2000)
	collision_array[2] = vec3(2000, 0, 2000)
	collision_array[3] = vec3(2000, 0, 1000)
	
	table.insert(g_strips, {vec = collision_array, n = collision_size})
end

cb.add(cb.draw, function()

  g_strips = {}
  check_spell_area()

  -- draw a opening shape
  for i = 1, #g_strips do
    local strip = g_strips[i]
    local vec = strip.vec
    for j = 0, strip.n - 2 do
      graphics.draw_line(vec[j], vec[j + 1], 2, 0xffff0000)
    end
  end
  
  -- draw the path finding
  local paths,size = navmesh.calcPos(player, mousePos, g_strips)
  graphics.draw_line_strip(paths, 2, 0xFF00FF00, size)
end)

```


###game
####game.mousePos
Return Value<br>
`vec3` returns the current position of the mouse<br>
####game.mousePos2D
Return Value<br>
`vec2` returns the current position of the mouse<br>
####game.cameraPos
Return Value<br>
`vec3` returns the current position of the camera<br>
####game.cameraLocked
Return Value<br>
`boolean` returns true if the camera is locked<br>
####game.setCameraLock(bool)
Parameters<br>
`boolean` bool<br>
Return Value<br>
`void` <br>
####game.cameraY
Return Value<br>
`number` returns the current camera zoom<br>
####game.cursorPos
Return Value<br>
`vec2` returns the current cursor position<br>
####game.time
Return Value<br>
`number` returns the current game time<br>
####game.version
Return Value<br>
`string` returns the current game version<br>
*You cant lock your shard to specific game version, this is a forbidden.*<br>
####game.selectedTarget
Return Value<br>
`obj` returns the current selected game object<br>
####game.hoveredTarget
Return Value<br>
`obj` returns the current hovered game object<br>
####game.mapID
Return Value<br>
`number` returns the current map ID<br>
####game.mode
Return Value<br>
`string` returns the current game mode<br>
####game.type
Return Value<br>
`string` returns the current game type<br>
####game.modeRoundIndex
Return Value<br>
`string` returns the current round index (2v2v2v2v2) <br>
####game.modePhaseIndex
Return Value<br>
`string` returns the current phase index (2v2v2v2v2) <br>
####game.shopOpen
Return Value<br>
`boolean` check if shop available<br>
####game.isWindowFocused
Return Value<br>
`boolean` returns true if LoL is focused<br>
####game.getHoveredTarget(int, int)
Parameters<br>
`int` mouse X<br>
`int` mouse Y<br>
Return Value<br>
`obj` returns the current hovered game object by position<br><br>
####game.sendEmote(emoteId)
Parameters<br>
`int` emoteId <br>
Return Value<br>
`void` <br>
```c
EMOTE_DANCE = 0
EMOTE_TAUNT = 1
EMOTE_LAUGH = 2
EMOTE_JOKE = 3
EMOTE_TOGGLE = 4
```
```lua
game.sendEmote(0) -- dance
```
####game.sendRadialEmote(index)
Parameters<br>
`int` index <br>
Return Value<br>
`void` <br>

```lua
game.sendRadialEmote(8) -- centre emote
```
####game.displayMasteryBadge()
Parameters<br>
Return Value<br>
`void` <br>
####game.fnvhash(str)
Parameters<br>
`string` input string<br>
Return Value<br>
`unsigned int` returns the fnvhash of input string<br>

####game.spellhash(str)
Parameters<br>
`string` input string<br>
Return Value<br>
`unsigned int` returns the spell hash of input string<br>

####game.hashSDBM(str)
Parameters<br>
`string` input string<br>
Return Value<br>
`unsigned int` returns the SDBM hash of input string<br>

###graphics
####graphics.width
Return Value<br>
`number` returns screen width<br>
####graphics.height
Return Value<br>
`number` returns screen height<br>
####graphics.res
Return Value<br>
`vec2` returns screen resolution<br>
####graphics.draw_text_2D(str, size, x, y, color)
Parameters<br>
`string` str<br>
`number` size<br>
`number` x<br>
`number` y<br>
`number` color<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_text_2D('foo', 14, game.cursorPos.x, game.cursorPos.y, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_outlined_text_2D(str, size, x, y, color, outline_color)
Parameters<br>
`string` str<br>
`number` size<br>
`number` x<br>
`number` y<br>
`number` color<br>
`number` outline_color<br>
Return Value<br>
`void`<br>
####graphics.text_area(str, size, n)
Parameters<br>
`string` str<br>
`number` size<br>
`number` n<br>
Return Value<br>
`number` returns str width<br>
`number` returns str height<br>
``` lua
local str = 'foo'
local font_size = 14
local x, y = graphics.text_area(str, font_size)
print(x, y)
```
####graphics.get_font()
Return Value<br>
`string` returns current font name<br>
####graphics.argb(a, r, g, b)
Parameters<br>
`number` a<br>
`number` r<br>
`number` g<br>
`number` b<br>
Return Value<br>
`number` returns color<br>
``` lua
local color = graphics.argb(255, 25, 185, 90)
local function on_draw()
	graphics.draw_text_2D('foo', 14, game.cursorPos.x, game.cursorPos.y, color)
end

cb.add(cb.draw, on_draw)
```
####graphics.world_to_screen(v1)
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec2` returns screen position from world position<br>
``` lua
local function on_draw()
	local v = graphics.world_to_screen(player.pos)
	graphics.draw_text_2D('foo', 14, v.x, v.y, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```
####graphics.world_to_screen_xyz(x, y, z)
Parameters<br>
`number` x<br>
`number` y<br>
`number` z<br>
Return Value<br>
`vec2` returns screen position from world position<br>
``` lua
local function on_draw()
	local v = graphics.world_to_screen_xyz(player.x, player.y, player.z)
	graphics.draw_text_2D('foo', 14, v.x, v.y, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_line_2D(x1, y1, x2, y2, width, color)
Parameters<br>
`number` x1<br>
`number` y1<br>
`number` x2<br>
`number` y2<br>
`number` width<br>
`number` color<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_line_2D(0, 0, game.cursorPos.x, game.cursorPos.y, 2, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_line(v1, v2, width, color)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
`number` width<br>
`number` color<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_line(mousePos, player.pos, 2, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```

####graphics.draw_triangle_2D(p1, p2, p3, width, color, is_filled, rounding)
Parameters<br>
`vec2` p1<br>
`vec2` p2<br>
`vec2` p3<br>
`number` width<br>
`number` color<br>
`boolean` is_filled, default: false<br>
`number` rounding, default: 0<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_triangle_2D(vec2(10, 10),vec2(10, 50),vec2(50, 10), 2, 0xFFFFFFFF, true)
end

cb.add(cb.draw, on_draw)
```

####graphics.draw_rectangle_2D(x, y, dx, dy, width, color, is_filled)
Parameters<br>
`number` x<br>
`number` y<br>
`number` dx<br>
`number` dy<br>
`number` width<br>
`number` color<br>
`boolean` is_filled: default: false<br>
`number` rounding: default: 0<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_rectangle_2D(game.cursorPos.x, game.cursorPos.y, 90, 20, 2, 0xFFFFFFFF)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_line_strip(pts, width, color, pts_n)
Parameters<br>
`vec3[]` pts<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	if player.path.active then
		graphics.draw_line_strip(player.path.point, 2, 0xFFFFFFFF, player.path.count+1)
	end
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_line_strip_2D(pts, width, color, pts_n)
Parameters<br>
`vec2[]` pts<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
Return Value<br>
`void`<br>
``` lua
local v = vec2.array(4)
v[0].x = 200
v[0].y = 200
v[1].x = 400
v[1].y = 200
v[2].x = 400
v[2].y = 400
v[3].x = 200
v[3].y = 400
local function on_draw()
	graphics.draw_line_strip_2D(v, 2, 0xFFFFFFFF, 4)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_circle(v1, radius, width, color, pts_n)
Parameters<br>
`vec3` v1<br>
`number` radius<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_circle(player.pos, player.attackRange, 2, 0xFFFFFFFF, 32)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_circle_2D(x, y, radius, width, color, pts_n)
Parameters<br>
`number` x<br>
`number` y<br>
`number` radius<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_circle_2D(game.cursorPos.x, game.cursorPos.y, 120, 2, 0xFFFFFFFF, 32)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_circle_xyz(x, y, z, radius, width, color, pts_n)
Parameters<br>
`number` x<br>
`number` y<br>
`number` z<br>
`number` radius<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_circle_xyz(player.x, player.y, player.z, player.attackRange, 2, 0xFFFFFFFF, 32)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_arc(v1, radius, width, color, pts_n, r1, r2)
Parameters<br>
`vec3` v1<br>
`number` radius<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
`number` r1<br>
`number` r2<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_arc(player.pos, player.attackRange, 2, 0xFFFFFFFF, 32, 0, math.pi/2)
end

cb.add(cb.draw, on_draw)
```
####graphics.draw_arc_2D(x, y, radius, width, color, pts_n, r1, r2)
Parameters<br>
`number` x<br>
`number` y<br>
`number` radius<br>
`number` width<br>
`number` color<br>
`number` pts_n<br>
`number` r1<br>
`number` r2<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw()
	graphics.draw_arc(player.pos, player.attackRange, 2, 0xFFFFFFFF, 32, 0, math.pi/2)
end

cb.add(cb.draw, on_draw)
```
####graphics.create_effect(type)
Create a shadereffect instance by type<br>
Parameters<br>
`number` type<br>
Return Value<br>
`shadereffect.obj`<br>
``` lua
-- create once, show always, with best performance
local circle_unchanged = graphics.create_effect(graphics.CIRCLE_RAINBOW)
circle_unchanged:update_circle(player.pos, 1200, 2, 0xFFFF0000)
circle_unchanged:attach(player)
circle_unchanged:show()
```
``` lua
-- update effect in on_draw
local circle_aa = graphics.create_effect(graphics.CIRCLE_RAINBOW)
local function on_draw()
	circle_aa:update_circle(player.pos, player.attackRange, 2, 0xff123456)
end
cb.add(cb.draw, on_draw)
```
####graphics.CIRCLE_GLOW
Return Value<br>
`number` simple glow circle<br>
####graphics.CIRCLE_GLOW_RAINBOW
Return Value<br>
`number` glow circle with rainbow<br>
####graphics.CIRCLE_GLOW_LIGHT
Return Value<br>
`number` another glow circle<br>
####graphics.CIRCLE_GLOW_BOLD
Return Value<br>
`number` another glow circle 2<br>
####graphics.CIRCLE_FIRE
Return Value<br>
`number` fire circle<br>
####graphics.CIRCLE_RAINBOW
Return Value<br>
`number` colorful rainbow circle<br>
####graphics.CIRCLE_RAINBOW_BOLD
Return Value<br>
`number` colorful another rainbow circle<br>
####graphics.CIRCLE_FILL
Return Value<br>
`number` filled circle<br>

####graphics.sprite(name)
Parameters<br>
`string` name<br>
`vec2` the screen position<br>
`number` scale<br>
`number` color<br>
Return Value<br>
`texture.obj`<br>
``` lua
local myIcon = graphics.sprite('XXX/menu_icon.png')
if myIcon then 
	-- In some PC it will failed load PNG, so need check this
	myMenu:set('icon', myIcon)
end
```

####graphics.game_sprite(name)
Parameters<br>
`string` name<br>
`vec2` the screen position<br>
`number` scale<br>
`number` color<br>
Return Value<br>
`texture.obj`<br>
``` lua
-- example: https://raw.communitydragon.org/14.1/game/assets/characters/sru_blue/hud/bluesentinel_circle.png
local icon = graphics.game_sprite('ASSETS/Characters/SRU_Blue/HUD/BlueSentinel_Circle.dds')
local icon_ashe = graphics.game_sprite('ASSETS/Characters/Ashe/HUD/Ashe_Circle.dds')
```
####graphics.draw_sprite(name, v1, scale, color)
Parameters<br>
`string|texture.obj` name<br>
`vec2` the screen position<br>
`number` scale<br>
`number` color<br>
Return Value<br>
`void`<br>
``` lua
local function on_draw_sprite()
	--sprite files must be placed in your shard directory
	graphics.draw_sprite("sprite_name.png", vec2(p.x, p.y), 1.5, 0x66FFFFFF)
end

cb.add(cb.sprite, on_draw_sprite)
```


####graphics.spawn_fake_click(color, v1)
Parameters<br>
`string` color: "red" or "green"<br>
`vec3` v1: world_pos<br>
Return Value<br>
`void`<br>
``` lua
local function on_key_down(k)
	if k==49 then --1
		graphics.spawn_fake_click("green", mousePos)
	end
end

cb.add(cb.keydown, on_key_down)
```

####graphics.set_draw(enabled)
Parameters<br>
`boolean` enabled<br>
Return Value<br>
`void`<br>

####graphics.get_draw()
Parameters<br>
Return Value<br>
`boolean` enabled<br>

####graphics.set_draw_menu(enabled)
Parameters<br>
`boolean` enabled<br>
Return Value<br>
`void`<br>

###shadereffect
####shadereffect.construct(effect_description, is_3D)
Parameters<br>
`string` effect_description<br>
`boolean` is_3D<br>
Return Value<br>
`shadereffect` shadereffect<br>

####shadereffect.begin(shadereffect, height, is_3D)
Parameters<br>
`shadereffect` shadereffect<br>
`number` hieght<br>
`boolean` is_3D<br>
Return Value<br>
`void`<br>

####shadereffect.set_float(shadereffect, varname, var)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`number` var<br>
Return Value<br>
`void`<br>

####shadereffect.set_vec2(shadereffect, varname, var)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`vec2` var<br>
Return Value<br>
`void`<br>

####shadereffect.set_vec3(shadereffect, varname, var)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`vec3` var<br>
Return Value<br>
`void`<br>

####shadereffect.set_vec4(shadereffect, varname, var)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`vec4` var<br>
Return Value<br>
`void`<br>

####shadereffect.set_float_array(shadereffect, varname, var, size)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`array` var<br>
`number` size<br>
Return Value<br>
`void`<br>

####shadereffect.set_color(shadereffect, varname, color)
Parameters<br>
`shadereffect` shadereffect<br>
`string` varname<br>
`color` var<br>
Return Value<br>
`void`<br>

###objManager
####objManager.player
Return Value<br>
`hero.obj` returns player object<br>
``` lua
print(player.charName)
```

####objManager.maxObjects
Return Value<br>
`number` returns max object count<br>

####objManager.get(i)
Return Value<br>
`obj` returns game object<br>
``` lua
for i=0, objManager.maxObjects-1 do
	local obj = objManager.get(i)
	if obj and obj.type==TYPE_HERO then
		print(obj.charName)
	end
end
```

####objManager.enemies_n
Return Value<br>
`number` returns enemy hero count<br>

####objManager.enemies
Return Value<br>
`hero.obj[]` returns array of enemy heroes<br>
``` lua
for i=0, objManager.enemies_n-1 do
	local obj = objManager.enemies[i]
	print(obj.charName)
end
```
####objManager.allies_n
Return Value<br>
`number` returns ally hero count<br>

####objManager.allies
Return Value<br>
`hero.obj[]` returns array of ally heroes<br>
``` lua
for i=0, objManager.allies_n-1 do
	local obj = objManager.allies[i]
	print(obj.charName)
end
```

####objManager.minions.size[team]
Parameters<br>
`team` can be any of these: `TEAM_ALLY`/`TEAM_ENEMY`/`TEAM_NEUTRAL` / "plants" / "others" / "farm" / "farm" / "lane_ally" / "lane_enemy" / "pets_ally" / "pets_enemy" / "barrels"<br>
Return Value<br>
`number` returns minion count of respective team<br>

``` lua
local enemyMinionCount = objManager.minions.size[TEAM_ENEMY]
```

####objManager.minions[team][i]
Parameters<br>
`team` can be any of these: `TEAM_ALLY`/`TEAM_ENEMY`/`TEAM_NEUTRAL` / "plants" / "others" / "farm" / "lane_ally" / "lane_enemy" / "pets_ally" / "pets_enemy" / "barrels"<br>
Return Value<br>
`minion.obj` returns minion object<br>
``` lua

local enemy_minion_size = objManager.minions.size[TEAM_ENEMY]
local enemy_minion_arr = objManager.minions[TEAM_ENEMY]
for i=0, enemy_minion_size-1 do
	local obj = enemy_minion_arr[i]
	print(obj.charName)
end

-- spell farm minions
local farm_minion_size = objManager.minions.size['farm']
local farm_minion_size = objManager.minions.size['farm']
local farm_minion_arr = objManager.minions['farm']
for i=0, farm_minion_size-1 do
	local obj = farm_minion_arr[i]
	print(obj.charName)
end

```

####objManager.turrets.size[team]
Return Value<br>
`number` returns turret count of respective team<br>

####objManager.turrets[team][i]
Return Value<br>
`turret.obj` returns turret object<br>
``` lua
for i=0, objManager.turrets.size[TEAM_ALLY]-1 do
	local obj = objManager.turrets[TEAM_ALLY][i]
	print(obj.charName)
end
```

####objManager.inhibs.size[team]
Return Value<br>
`number` returns inhib count of respective team<br>

####objManager.inhibs[team][i]
Return Value<br>
`inhib.obj` returns inhib object<br>
``` lua
for i=0, objManager.inhibs.size[TEAM_ALLY]-1 do
	local obj = objManager.inhibs[TEAM_ALLY][i]
	print(obj.health)
end
```

####objManager.nexus[team]
Return Value<br>
`nexus.obj` returns nexus object<br>
``` lua
print(objManager.nexus[TEAM_ENEMY].health)
```

####objManager.allObjects[i]
Return Value<br>
`base.obj` returns GameObject<br>

####objManager.allAttackableUnits[i]
Return Value<br>
`base.obj` returns AttackableUnit<br>

####objManager.allHeros[i]
Return Value<br>
`hero.obj` returns hero object<br>

``` lua
for i=0, objManager.allHeros.size-1 do
	local obj = objManager.allHeros[i]
	print(obj.handle)
end
```

####objManager.allMinions[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.minionsAlly[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.minionsEnemy[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.minionsNeutral[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.minionsOther[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.petsAlly[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.petsEnemy[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.barrels[i]
Return Value<br>
`minion.obj` returns minion object<br>

####objManager.missiles[i]
Return Value<br>
`missile.obj` returns missile object<br>

####objManager.particles[i]
Return Value<br>
`particle.obj` returns particle object<br>

####objManager.wardsAlly[i]
Return Value<br>
`minion.obj` returns ally ward object<br>


####objManager.loop(f)
Parameters<br>
`function` f<br>
Return Value<br>
`void`<br>
``` lua
local function foo(obj)
	if obj.type==TYPE_HERO then
		print(obj.charName)
	end
end

objManager.loop(foo)
```

###core
####core.tick
Return Value<br>
`number` returns current core_tick<br>

####core.fps
Return Value<br>
`number` returns current fps<br>

####core.block_input()

Only works in `cb.issueorder` and `cb.castspell`, will block current operation.

Return Value<br>
`void`<br>
``` lua
local function on_issue_order(order, pos, target_ptr)
	if order==3 then
		--blocks this attack
		--this only works for orders issued by hanbot
		core.block_input()
	end
end

cb.add(cb.issueorder, on_issue_order)
```
####core.reload()
Return Value<br>
`void`<br>


###sound

####sound.play(name)
Parameters<br>
`string` name<br>

``` lua
-- while resource is shared between all plugins, it is better to have a unique name (path)
sound.play('demo_aio_resources/load.wav')
```

####sound.play_from_file(file_path)
Parameters<br>
`string` file_path<br>

####sound.disable(is_disabled)
Parameters<br>
`boolean` is_disabled<br>



###shop

####shop.canShop
Return Value<br>
`bool` <br>

####shop.isOpened
Return Value<br>
`bool` <br>

####shop.augmentSelectionOpen
Return Value<br>
`bool` <br>

####shop.augmentSelectionIds
Return Value<br>
`table` See AugmentId<br>
```
enum class AugmentId: std::uint32_t
{
	Oathsworn = 0x1F273AC,// buff_hash( "Oathsworn" )
	ShrinkRay = 0x302DB74,// buff_hash( "ShrinkRay" )
	UltimateRevolution = 0x4A9BDC5,// buff_hash( "UltimateRevolution" )
	StackosaurusRex = 0x55E5BD2,// buff_hash( "StackosaurusRex" )
	OrbitalLaser = 0x5E9FD41,// buff_hash( "OrbitalLaser" )
	ApexInventor = 0x93D7848,// buff_hash( "ApexInventor" )
	escAPADe = 0xB24AB25,// buff_hash( "escAPADe" )
	WarmupRoutine = 0xB731243,// buff_hash( "WarmupRoutine" )
	HeavyHitter = 0x109C1530,// buff_hash( "HeavyHitter" )
	SummonersRoulette = 0x13BDA632,// buff_hash( "SummonersRoulette" )
	EtherealWeapon = 0x13E8C4A7,// buff_hash( "EtherealWeapon" )
	TheBrutalizer = 0x16EA7954,// buff_hash( "TheBrutalizer" )
	ItsKillingTime = 0x17A308CA,// buff_hash( "ItsKillingTime" )
	GiantSlayer = 0x1950C668,// buff_hash( "GiantSlayer" )
	SearingDawn = 0x199AA2C8,// buff_hash( "SearingDawn" )
	CannonFodder = 0x1A9B0060,// buff_hash( "CannonFodder" )
	Quest_WoogletsWitchcap = 0x1BC0CAC1,// buff_hash( "Quest_WoogletsWitchcap" )
	SpinToWin = 0x209762E6,// buff_hash( "SpinToWin" )
	Executioner = 0x23F1EBC6,// buff_hash( "Executioner" )
	NowYouSeeMe = 0x26433BAB,// buff_hash( "NowYouSeeMe" )
	FeeltheBurn = 0x2D24DA51,// buff_hash( "FeeltheBurn" )
	ItsCritical = 0x2E4815CC,// buff_hash( "ItsCritical" )
	GambaAnvil = 0x2EFA5F6D,// buff_hash( "GambaAnvil" )
	MadScientist = 0x301C4AB9,// buff_hash( "MadScientist" )
	DontBlink = 0x361E81B4,// buff_hash( "DontBlink" )
	GuiltyPleasure = 0x38A48C10,// buff_hash( "GuiltyPleasure" )
	SkilledSniper = 0x3A3FB8AC,// buff_hash( "SkilledSniper" )
	OutlawsGrit = 0x3AFCE102,// buff_hash( "OutlawsGrit" )
	Clothesline = 0x3D187ED1,// buff_hash( "Clothesline" )
	BannerofCommand = 0x3F13BB13,// buff_hash( "BannerofCommand" )
	TwiceThrice = 0x42346B02,// buff_hash( "TwiceThrice" )
	SoulSiphon = 0x4293CD3B,// buff_hash( "SoulSiphon" )
	OmniSoul = 0x44031317,// buff_hash( "OmniSoul" )
	Chauffeur = 0x4474F5D0,// buff_hash( "Chauffeur" )
	ServeBeyondDeath = 0x4589990F,// buff_hash( "ServeBeyondDeath" )
	Quest_UrfsChampion = 0x4716448D,// buff_hash( "Quest_UrfsChampion" )
	CelestialBody = 0x47330DB1,// buff_hash( "CelestialBody" )
	IceCold = 0x48B5BDCA,// buff_hash( "IceCold" )
	FromBeginningToEnd = 0x48DC2006,// buff_hash( "FromBeginningToEnd" )
	DawnbringersResolve = 0x4B303285,// buff_hash( "DawnbringersResolve" )
	WillingSacrifice = 0x4B43BF6C,// buff_hash( "WillingSacrifice" )
	JuiceBox = 0x4D27E960,// buff_hash( "JuiceBox" )
	DontChase = 0x4DBF5E70,// buff_hash( "DontChase" )
	BreadAndCheese = 0x4E28F2C3,// buff_hash( "BreadAndCheese" )
	FrostWraith = 0x4F7D128E,// buff_hash( "FrostWraith" )
	FeyMagic = 0x52022D72,// buff_hash( "FeyMagic" )
	DrawYourSword = 0x522572E9,// buff_hash( "DrawYourSword" )
	InfernalSoul = 0x55780831,// buff_hash( "InfernalSoul" )
	QuantumComputing = 0x55EF3A40,// buff_hash( "QuantumComputing" )
	OkBoomerang = 0x58FEA611,// buff_hash( "OkBoomerang" )
	Eureka = 0x59B3AFC2,// buff_hash( "Eureka" )
	Dematerialize = 0x5C8D739F,// buff_hash( "Dematerialize" )
	BigBrain = 0x5F479857,// buff_hash( "BigBrain" )
	MysticPunch = 0x610EB7B4,// buff_hash( "MysticPunch" )
	HolyFire = 0x61BEDC9B,// buff_hash( "HolyFire" )
	SymphonyofWar = 0x64EB2265,// buff_hash( "SymphonyofWar" )
	Marksmage = 0x65A8CBEF,// buff_hash( "Marksmage" )
	ScopierWeapons = 0x662429D1,// buff_hash( "ScopierWeapons" )
	BluntForce = 0x6951004B,// buff_hash( "BluntForce" )
	MindtoMatter = 0x6AD13E9D,// buff_hash( "MindtoMatter" )
	Homeguard = 0x6CA0F337,// buff_hash( "Homeguard" )
	Earthwake = 0x6E25F1F7,// buff_hash( "Earthwake" )
	Quest_AngelofRetribution = 0x6F79D727,// buff_hash( "Quest_AngelofRetribution" )
	BuffBuddies = 0x71E56AB8,// buff_hash( "BuffBuddies" )
	NestingDoll = 0x73016C04,// buff_hash( "NestingDoll" )
	BreadAndJam = 0x75565D16,// buff_hash( "BreadAndJam" )
	Recursion = 0x76B60E67,// buff_hash( "Recursion" )
	TankItOrLeaveIt = 0x80B86F89,// buff_hash( "TankItOrLeaveIt" )
	FrozenFoundations = 0x819259C7,// buff_hash( "FrozenFoundations" )
	Vengeance = 0x886F1F8D,// buff_hash( "Vengeance" )
	WithHaste = 0x894E5EBC,// buff_hash( "WithHaste" )
	Erosion = 0x8C2F16FE,// buff_hash( "Erosion" )
	Perseverance = 0x8D3AE60E,// buff_hash( "Perseverance" )
	ChainLightning = 0x8E40C3DC,// buff_hash( "ChainLightning" )
	TrueshotProdigy = 0x93AB024B,// buff_hash( "TrueshotProdigy" )
	PhenomenalEvil = 0x94D656DE,// buff_hash( "PhenomenalEvil" )
	ContractKiller = 0x97C4EFA0,// buff_hash( "ContractKiller" )
	BacktoBasics = 0x984667B4,// buff_hash( "BacktoBasics" )
	CircleofDeath = 0x9A1D093E,// buff_hash( "CircleofDeath" )
	Castle = 0x9AC2A459,// buff_hash( "Castle" )
	JeweledGauntlet = 0x9CAAE31B,// buff_hash( "JeweledGauntlet" )
	SlapAround = 0x9DFB15EE,// buff_hash( "SlapAround" )
	RestlessRestoration = 0x9E1A180E,// buff_hash( "RestlessRestoration" )
	CriticalHealing = 0x9F40039E,// buff_hash( "CriticalHealing" )
	Flashy = 0x9F6FD4F0,// buff_hash( "Flashy" )
	MasterofDuality = 0x9F9005F8,// buff_hash( "MasterofDuality" )
	Quest_SteelYourHeart = 0xA173E08E,// buff_hash( "Quest_SteelYourHeart" )
	Impassable = 0xA1A3AF22,// buff_hash( "Impassable" )
	ScopiestWeapons = 0xA1D75DC2,// buff_hash( "ScopiestWeapons" )
	LightemUp = 0xA26FF4EC,// buff_hash( "LightemUp" )
	OceanSoul = 0xA3670B02,// buff_hash( "OceanSoul" )
	Deft = 0xA3E2E068,// buff_hash( "Deft" )
	LaserEyes = 0xA748902E,// buff_hash( "LaserEyes" )
	WisdomofAges = 0xA83CA207,// buff_hash( "WisdomofAges" )
	DemonsDance = 0xA8B08058,// buff_hash( "DemonsDance" )
	BloodBrother = 0xAB06A043,// buff_hash( "BloodBrother" )
	Minionmancer = 0xAB4CDD4D,// buff_hash( "Minionmancer" )
	Firebrand = 0xABA0CD52,// buff_hash( "Firebrand" )
	SpiritLink = 0xAC744FB8,// buff_hash( "SpiritLink" )
	MountainSoul = 0xAE76811D,// buff_hash( "MountainSoul" )
	Vulnerability = 0xAFE4CF71,// buff_hash( "Vulnerability" )
	RaidBoss = 0xB2EDEF40,// buff_hash( "RaidBoss" )
	MagicMissile = 0xB4545A74,// buff_hash( "MagicMissile" )
	WitchfulThinking = 0xB503AEA3,// buff_hash( "WitchfulThinking" )
	CantTouchThis = 0xB5D9645A,// buff_hash( "CantTouchThis" )
	ComboMaster = 0xBA23DC87,// buff_hash( "ComboMaster" )
	KeystoneConjurer = 0xBBE31DDB,// buff_hash( "KeystoneConjurer" )
	BreadAndButter = 0xBD47D568,// buff_hash( "BreadAndButter" )
	ThreadtheNeedle = 0xBE4AA497,// buff_hash( "ThreadtheNeedle" )
	SnowballFight = 0xBF2B1A73,// buff_hash( "SnowballFight" )
	Typhoon = 0xBF771C16,// buff_hash( "Typhoon" )
	MirrorImage = 0xC390B2C7,// buff_hash( "MirrorImage" )
	RabbleRousing = 0xC3A6E3C0,// buff_hash( "RabbleRousing" )
	SelfDestruct = 0xC451D495,// buff_hash( "SelfDestruct" )
	DefensiveManeuvers = 0xC488607E,// buff_hash( "DefensiveManeuvers" )
	SlowCooker = 0xCB705AEB,// buff_hash( "SlowCooker" )
	UltimateUnstoppable = 0xCDF2651B,// buff_hash( "UltimateUnstoppable" )
	ADAPt = 0xD18FEA7F,// buff_hash( "ADAPt" )
	TapDancer = 0xD1F84AA5,// buff_hash( "TapDancer" )
	Spellwake = 0xD3CBE301,// buff_hash( "Spellwake" )
	Flashbang = 0xD4DA8047,// buff_hash( "Flashbang" )
	ShadowRunner = 0xD5F12997,// buff_hash( "ShadowRunner" )
	CourageoftheColossus = 0xD68F7D08,// buff_hash( "CourageoftheColossus" )
	InfernalConduit = 0xD79FD9B0,// buff_hash( "InfernalConduit" )
	AcceleratingSorcery = 0xDA054EE4,// buff_hash( "AcceleratingSorcery" )
	Repulsor = 0xDABCBBC3,// buff_hash( "Repulsor" )
	ExtendoArm = 0xDE9A77E4,// buff_hash( "ExtendoArm" )
	ScopedWeapons = 0xE3E3DBBE,// buff_hash( "ScopedWeapons" )
	LightningStrikes = 0xE48980B4,// buff_hash( "LightningStrikes" )
	FallenAegis = 0xE67E996E,// buff_hash( "FallenAegis" )
	BladeWaltz = 0xE8A9A9F1,// buff_hash( "BladeWaltz" )
	FirstAidKit = 0xE9AFCCDF,// buff_hash( "FirstAidKit" )
	Dashing = 0xED80A0CB,// buff_hash( "Dashing" )
	FullyAutomated = 0xEDFA6D47,// buff_hash( "FullyAutomated" )
	HoldVeryStill = 0xF0544646,// buff_hash( "HoldVeryStill" )
	DieAnotherDay = 0xF0DBEF32,// buff_hash( "DieAnotherDay" )
	Goredrink = 0xF4EBEFD4,// buff_hash( "Goredrink" )
	Vanish = 0xF6A6FFEA,// buff_hash( "Vanish" )
	AllForYou = 0xFC06EEFA,// buff_hash( "AllForYou" )
	Goliath = 0xFCB87F9B,// buff_hash( "Goliath" )
	CenterOfTheUniverse = 0xFCCE03A7,// buff_hash( "CenterOfTheUniverse" )
	DiveBomber = 0xFD0ED9E4,// buff_hash( "DiveBomber" )
	ParasiticRelationship = 0xFE635A5B,// buff_hash( "ParasiticRelationship" )
	Restart = 0xFE9C11EC,// buff_hash( "Restart" )
	Tormentor = 0xFEFBCC4F,// buff_hash( "Tormentor" )
	SonicBoom = 0xFF509218,// buff_hash( "SonicBoom" )
};
```

####shop.buyItem(itemID, preferredSlotID)

####shop.sellItem(inventorySlotId)

####shop.undo()

####shop.swapItem(source, dest)




###memory
Valid types:<br>

 * char
 * unsigned char
 * short
 * unsigned short
 * int
 * unsigned int
 * long long
 * unsigned long long
 * float
 
####memory.new(type, n)
Parameters<br>
`string` type<br>
`number` n<br>
Return Value<br>
`mixed` c-type array<br>
###input
Enums:<br>

 * input.LOCK_MOVEMENT
 * input.LOCK_ABILITIES
 * input.LOCK_SUMMONERSPELLS
 * input.LOCK_SHOP
 * input.LOCK_CHAT
 * input.LOCK_MINIMAPMOVEMENT
 * input.LOCK_CAMERAMOVEMENT
 
####input.lock(...)
Parameters<br>
`number` input_type<br>
Return Value<br>
`void` <br>
####input.unlock(...)
Parameters<br>
`number` input_type<br>
Return Value<br>
`void` <br>
####input.islocked(...)
Parameters<br>
`number` input_type<br>
Return Value<br>
`boolean` <br>
####input.lock_slot(...)
Parameters<br>
`number` slot<br>
Return Value<br>
`void` <br>
####input.unlock_slot(...)
Parameters<br>
`number` slot<br>
Return Value<br>
`void` <br>
####input.islocked_slot(...)
Parameters<br>
`number` slot<br>
Return Value<br>
`boolean` <br>

###keyboard
####keyboard.isKeyDown(key_code)
Parameters<br>
`number` key_code<br>
Return Value<br>
`boolean` returns true if key_code is down<br>
``` lua
local function on_tick()
	if keyboard.isKeyDown(0x20) then --spacebar
		print('spacebar pressed')
	end
end

cb.add(cb.tick, on_tick)
```
####keyboard.getClipboardText()
Return Value<br>
`string` returns text that was copied to clipboard<br>
`string` returns error message on failure<br>
####keyboard.setClipboardText(text)
Parameters<br>
`string` text<br>
Return Value<br>
`void` copies text to clipboard<br>
####keyboard.keyCodeToString(key_code)
Parameters<br>
`number` key_code<br>
Return Value<br>
`string` returns corresponding character of key_code<br>
``` lua
print(keyboard.keyCodeToString(0x20))
```
####keyboard.stringToKeyCode(key)
Parameters<br>
`string` key<br>
Return Value<br>
`number` returns corresponding key_code of key<br>
``` lua
print(keyboard.stringToKeyCode('Space'))
```

###permashow
####permashow.enable(v1)
Parameters<br>
`boolean` enabled<br>
####permashow.set_pos(x, y)
Parameters<br>
`number` x<br>
`number` y<br>
####permashow.set_drag_enabled(option)
Parameters<br>
`number` option, 1 = enabled always, 2 = enabled when menu show<br>
####permashow.set_alpha(alpha)
Parameters<br>
`number` alpha<br>
####permashow.set_theme(theme)
Parameters<br>
`table` theme<br>

```lua
-- simple, set the alpha
permashow.set_alpha(100)

-- advanced usage, set custom theme (alpha will be ignored)
permashow.set_theme({
	itemHeight = 20,
	textSize = 14,
	textColor = 0xFFFFF799,
	textColorDisabled = 0xFFA8A8A8,

	shadowColor = 0x90000000,
	backgroundUpLeft = 0x90797145,
	backgroundUpRight = 0x904a3f23,
	backgroundBottomLeft = 0x90797145,
	backgroundBottomRight = 0x904a3f23,
	areaUpLeft = 0x90091e18,
	areaUpRight = 0x90091e18,
	areaBottomLeft = 0x9005120c,
	areaBottomRight = 0x9005120c,
	
	itemBorder1 = 0x33f4f499,
	itemBorder2 = 0x11f4f499,
	itemBorder3 = 0x33f4f499,
})
permashow.enable(true)
```

###network
####network.latency
Return Value<br>
`number` returns game network latency in seconds<br>

####network.download_file(url, dest)
Parameters<br>
`string` url<br>
`string` dest<br>
Return Value<br>
`boolean` returns true on success<br>
``` lua
local url = 'https://i.imgur.com/k6HB1gA.gif'
local dest = hanbot.luapath..'/ok.png'
local success = network.download_file(url, dest)
print(success)
```
####network.easy_download(cb, uri, path)
Parameters<br>
`function` cb<br>
`string` uri<br>
`string` dest<br>
Return Value<br>
`void` <br>
####network.easy_post(cb, uri, postfields)
Parameters<br>
`function` cb<br>
`string` uri<br>
`string` postfields<br>
Return Value<br>
`void` <br>
###module
####module.seek(mod)
Parameters<br>
`string` mod<br>
Return Value<br>
`module` returns module if it is loaded<br>
``` lua
local function on_tick()
	--module.seek will only return the module if its loaded
	local evade = module.seek('evade')
	if evade and evade.core.is_active() then return end
end

cb.add(cb.tick, on_tick)
```
####module.load(id, mod)
Parameters<br>
`string` id<br>
`string` mod<br>
Return Value<br>
`module` returns module, loads it if needed<br>
``` lua
local foo_bar = module.load('foo', 'bar')
```
####module.internal(mod)
Parameters<br>
`string` mod<br>
Return Value<br>
`module` returns module, loads it if needed<br>
``` lua
local orb = module.internal('orb')
local function on_tick()
	local evade = module.seek('evade')
	if evade and evade.core.is_active() then return end
end

cb.add(cb.tick, on_tick)
```
####module.lib(id)
Parameters<br>
`string` id<br>
Return Value<br>
`library` returns library, loads it if needed<br>
####module.path(id)
Parameters<br>
`string` id<br>
Return Value<br>
`string` returns module path<br>
####module.is_shard(id)
Parameters<br>
`string` id<br>
Return Value<br>
`boolean` returns true if shard id exists<br>
####module.is_libshard(id)
Parameters<br>
`string` id<br>
Return Value<br>
`boolean` returns true if libshard id exists<br>
####module.is_anyshard(id)
Parameters<br>
`string` id<br>
Return Value<br>
`boolean` returns true if shard id or libshard id exists<br>
####module.file_exists(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true file exists<br>
####module.directory_exists(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true file exists<br>
####module.create_directory(id, path)
Parameters<br>
`string` id<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.create_script_directory(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.create_lib_directory(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.create_shard_directory(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.open_file(id, path, mode)
Parameters<br>
`string` id<br>
`string` path<br>
`string` mod<br>
Return Value<br>
`file` returns file handle on success<br>
####module.open_script_file(path, mode)
Parameters<br>
`string` path<br>
`string` mod<br>
Return Value<br>
`file` returns file handle on success<br>
####module.open_lib_file(path, mode)
Parameters<br>
`string` path<br>
`string` mod<br>
Return Value<br>
`file` returns file handle on success<br>
####module.open_shard_file(path, mode)
Parameters<br>
`string` path<br>
`string` mod<br>
Return Value<br>
`file` returns file handle on success<br>
####module.delete_file(id, path)
Parameters<br>
`string` id<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.delete_script_file(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.delete_lib_file(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.delete_shard_file(path)
Parameters<br>
`string` path<br>
Return Value<br>
`boolean` returns true on success<br>
####module.rename_file(id, old, new)
Parameters<br>
`string` id<br>
`string` old<br>
`string` new<br>
Return Value<br>
`boolean` returns true on success<br>
####module.rename_script_file(old, new)
Parameters<br>
`string` old<br>
`string` new<br>
Return Value<br>
`boolean` returns true on success<br>
####module.rename_lib_file(old, new)
Parameters<br>
`string` old<br>
`string` new<br>
Return Value<br>
`boolean` returns true on success<br>
####module.rename_shard_file(old, new)
Parameters<br>
`string` old<br>
`string` new<br>
Return Value<br>
`boolean` returns true on success<br>
####module.generate_tree(id, hash, anyfile)
Parameters<br>
`string` id<br>
`string` hash<br>
`boolean` anyfile<br>
Return Value<br>
`table` returns file tree<br>
###menu
####menu(var, text)
Parameters<br>
`string` var<br>
`string` text<br>
Return Value<br>
`object` returns menu instance<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
```
####menu:header(var, text)
Parameters<br>
`string` var<br>
`string` text<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:header('example_header', 'Example Header')
```
####menu:boolean(var, text, value)
Parameters<br>
`string` var<br>
`string` text<br>
`boolean` value<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:boolean('example_boolean', 'Example Boolean')

local function on_tick()
	if myMenu.example_boolean:get() then
		print('example_boolean is true')
	end
end

cb.add(cb.tick, on_tick)
```
####menu:slider(var, text, value, min, max, step)
Parameters<br>
`string` var<br>
`string` text<br>
`number` value<br>
`number` min<br>
`number` max<br>
`number` step<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:slider('example_slider', 'Example Slider', 100, 0, 150, 5)

local function on_tick()
	print(myMenu.example_slider:get())
end

cb.add(cb.tick, on_tick)
```
####menu:keybind(var, text, key, toggle, defaultToggleValue)
Parameters<br>
`string` var<br>
`string` text<br>
`string` key<br>
`string` toggle<br>
`bool` defaultToggleValue<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
--this creates an on key down keybind for 'A'
myMenu:keybind('example_keybind_a', 'Example Keybind A', 'A', nil)
--this creates a toggle keybind for 'A'
myMenu:keybind('example_keybind_b', 'Example Keybind B', nil, 'A')
--this creates an on key down keybind for 'A' or toggle for 'B'
myMenu:keybind('example_keybind_c', 'Example Keybind C', 'A', 'B')
--this disable the permashow for Keybind C
myMenu.example_keybind_c:permashow(false)

local function on_tick()
	if myMenu.example_keybind_a:get() then
		print('example_keybind_a is active')
	end
end

cb.add(cb.tick, on_tick)
```
####menu:dropdown(var, text, value, options)
Parameters<br>
`string` var<br>
`string` text<br>
`number` value<br>
`table` options<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:dropdown('example_dropdown', 'Example Dropdown', 1, {'Option A', 'Option B', 'Option C',})

local function on_tick()
	print(myMenu.example_dropdown:get())
end

cb.add(cb.tick, on_tick)
```
####menu:button(var, text, buttonText, callback)
Parameters<br>
`string` var<br>
`string` text<br>
`string` buttonText<br>
`function` callback<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:button('example_button', 'Example Button', 'My Button', function() print('button was pressed') end)
```
####menu:color(var, text, red, green, blue, alpha)
Parameters<br>
`string` var<br>
`string` text<br>
`number` red<br>
`number` green<br>
`number` blue<br>
`number` alpha<br>
Return Value<br>
`void`<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')
myMenu:color('example_color', 'Example Color', 255, 0, 0, 255)

local function on_draw()
	graphics.draw_text_2D('foo', 14, game.cursorPos.x, game.cursorPos.y, myMenu.example_color:get())
end

cb.add(cb.draw, on_draw)
```
####menu:isopen()
Return Value<br>
`boolean` returns true if the menu is currently open<br>
``` lua
local myMenu = menu('example_menu', 'Example Menu')

local function on_tick()
	if myMenu:isopen() then
		print('menu is open')
	end
end

cb.add(cb.tick, on_tick)
```
####menu:set(property, value)
Parameters<br>
`string` property<br>
`mixed` value<br>
Return Value<br>
`void`<br>
``` lua
--[[
The following properties can be set on their respective instances:
	'tooltip'
	'callback'
	'value'
	'text'
	'visible'
	'buttonText'
	'red'
	'green'
	'blue'
	'alpha'
	'options'
	'toggleValue'
	'toggle'
	'key'
	'min'
	'max'
	'step',
	'icon',
]]

local myMenu = menu('example_menu', 'Example Menu')
myMenu:slider('example_slider', 'Example Slider', 100, 0, 150, 5)

myMenu.example_slider:set('tooltip', 'This text will appear when the mouse is hovering Example Slider')
myMenu.example_slider:set('callback', function(old, new)
	print(('example_slider changed from %u to %u'):format(old, new))
end)

local myIcon = graphics.sprite('XXX/menu_icon.png')
myMenu.example_slider:set('icon', myIcon)

```
###md5
####md5.file(path)
Parameters<br>
`string` path<br>
Return Values<br>
`string` returns md5 hash
####md5.sum(str)
Parameters<br>
`string` str<br>
Return Values<br>
`string` returns integer md5 hash
####md5.tohex(str, upper)
Parameters<br>
`string` str<br>
`boolean` upper<br>
Return Values<br>
`string` returns str in hex, in uppercase if upper is true

