Parameters<br>
`hero.obj` player<br>
`number` index<br>
Return Value<br>
`void`<br>
####player:castSpell(type, slot, arg1, arg2, no_limit)
Parameters<br>
`hero.obj` player<br>
`string` type<br>
`number` slot<br>
`mixed` arg1<br>
`mixed` arg2<br>
`boolean` no_limit: ignore the limitation check, maybe kickout/banned, use careful<br>
Return Value<br>
`void`<br>
``` lua
--type 'pos', orianna q
player:castSpell('pos', 0, mousePos)
--type 'obj', teemo q
player:castSpell('obj', 0, game.selectedTarget)
--type 'self', teemo w
player:castSpell('self', 1)
--type 'line', rumble r
player:castSpell('line', 3, player.pos, mousePos)
--type 'release', varus q
player:castSpell('release', 0, player.pos, mousePos)
--type 'move', aurelion sol q
player:castSpell('move', 0, mousePos, nil, true)
--type 'switch', Hwei Q
player:castSpell('switch', 0)
```
####player:levelSpell(slot)
Parameters<br>
