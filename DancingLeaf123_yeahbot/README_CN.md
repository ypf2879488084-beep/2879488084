# yeahbot Hanbot Open Source ??

??: https://github.com/DancingLeaf123/yeahbot/tree/main/Hanbot%20Open%20Source

## ????????

- Generic prediction wrapper: `Hanbot Open Source/lvxlol/lvxbot/expert.lua`
- Ezreal simple champion script: `Hanbot Open Source/lvxlol/ezreal/main.lua`
- Ezreal Q implementation: `Hanbot Open Source/lvxlol/ezreal/q.lua`
- Lucian spell modules: `Hanbot Open Source/lvxlol/lucian/main.lua`
- Syndra Q prediction: `Hanbot Open Source/beasty syndra/Syndra/q.lua`
- Syndra Q-E combo: `Hanbot Open Source/beasty syndra/Syndra/q_e.lua`
- Syndra E on target: `Hanbot Open Source/beasty syndra/Syndra/e_on_tar.lua`
- Riven prediction modules: `Hanbot Open Source/gagong riven/pred/main.lua`
- Menu example: `Hanbot Open Source/menu example/menu.lua`
- Spell timing tip: `Hanbot Open Source/coding tips/spell timing.lua`

## ?? Lua ??

- `Hanbot Open Source/beasty syndra/draw/chat.lua`
- `Hanbot Open Source/beasty syndra/draw/circle.lua`
- `Hanbot Open Source/beasty syndra/draw/color.lua`
- `Hanbot Open Source/beasty syndra/draw/info.lua`
- `Hanbot Open Source/beasty syndra/draw/stacks.lua`
- `Hanbot Open Source/beasty syndra/draw/text.lua`
- `Hanbot Open Source/beasty syndra/draw/timer.lua`
- `Hanbot Open Source/beasty syndra/header.lua`
- `Hanbot Open Source/beasty syndra/main.lua`
- `Hanbot Open Source/beasty syndra/Syndra/auto_e.lua`
- `Hanbot Open Source/beasty syndra/Syndra/core.lua`
- `Hanbot Open Source/beasty syndra/Syndra/dmg.lua`
- `Hanbot Open Source/beasty syndra/Syndra/e_on_q.lua`
- `Hanbot Open Source/beasty syndra/Syndra/e_on_tar.lua`
- `Hanbot Open Source/beasty syndra/Syndra/main.lua`
- `Hanbot Open Source/beasty syndra/Syndra/menu.lua`
- `Hanbot Open Source/beasty syndra/Syndra/q.lua`
- `Hanbot Open Source/beasty syndra/Syndra/q_e.lua`
- `Hanbot Open Source/beasty syndra/Syndra/r.lua`
- `Hanbot Open Source/beasty syndra/Syndra/spells.lua`
- `Hanbot Open Source/beasty syndra/Syndra/sphere_manager.lua`
- `Hanbot Open Source/beasty syndra/Syndra/w.lua`
- `Hanbot Open Source/beasty syndra/Syndra/w_cast.lua`
- `Hanbot Open Source/coding tips/spell timing.lua`
- `Hanbot Open Source/gagong riven/core/ai.lua`
- `Hanbot Open Source/gagong riven/core/draw.lua`
- `Hanbot Open Source/gagong riven/core/main.lua`
- `Hanbot Open Source/gagong riven/header.lua`
- `Hanbot Open Source/gagong riven/item/crescent_wrapper.lua`
- `Hanbot Open Source/gagong riven/main.lua`
- `Hanbot Open Source/gagong riven/menu.lua`
- `Hanbot Open Source/gagong riven/pred/aa.lua`
- `Hanbot Open Source/gagong riven/pred/e.lua`
- `Hanbot Open Source/gagong riven/pred/e_flash_q.lua`
- `Hanbot Open Source/gagong riven/pred/e_flash_w.lua`
- `Hanbot Open Source/gagong riven/pred/e_q.lua`
- `Hanbot Open Source/gagong riven/pred/e_w.lua`
- `Hanbot Open Source/gagong riven/pred/flash_q.lua`
- `Hanbot Open Source/gagong riven/pred/flash_w.lua`
- `Hanbot Open Source/gagong riven/pred/main.lua`
- `Hanbot Open Source/gagong riven/pred/push.lua`
- `Hanbot Open Source/gagong riven/pred/q.lua`
- `Hanbot Open Source/gagong riven/pred/r1.lua`
- `Hanbot Open Source/gagong riven/pred/r2.lua`
- `Hanbot Open Source/gagong riven/pred/r2_dmg.lua`
- `Hanbot Open Source/gagong riven/pred/w.lua`
- `Hanbot Open Source/gagong riven/spell/e.lua`
- `Hanbot Open Source/gagong riven/spell/flash.lua`
- `Hanbot Open Source/gagong riven/spell/main.lua`
- `Hanbot Open Source/gagong riven/spell/q.lua`
- `Hanbot Open Source/gagong riven/spell/r1.lua`
- `Hanbot Open Source/gagong riven/spell/r2.lua`
- `Hanbot Open Source/gagong riven/spell/w.lua`
- `Hanbot Open Source/hello world/header.lua`
- `Hanbot Open Source/hello world/main.lua`
- `Hanbot Open Source/lvxlol/debug.lua`
- `Hanbot Open Source/lvxlol/ezreal/main.lua`
- `Hanbot Open Source/lvxlol/ezreal/menu.lua`
- `Hanbot Open Source/lvxlol/ezreal/q.lua`
- `Hanbot Open Source/lvxlol/ezreal/w.lua`
- `Hanbot Open Source/lvxlol/header.lua`
- `Hanbot Open Source/lvxlol/lucian/e.lua`
- `Hanbot Open Source/lvxlol/lucian/main.lua`
- `Hanbot Open Source/lvxlol/lucian/menu.lua`
- `Hanbot Open Source/lvxlol/lucian/q.lua`
- `Hanbot Open Source/lvxlol/lucian/w.lua`
- `Hanbot Open Source/lvxlol/lvxbot/combo_tracker.lua`
- `Hanbot Open Source/lvxlol/lvxbot/expert.lua`
- `Hanbot Open Source/lvxlol/lvxbot/main.lua`
- `Hanbot Open Source/lvxlol/main.lua`
- `Hanbot Open Source/menu example/header.lua`
- `Hanbot Open Source/menu example/main.lua`
- `Hanbot Open Source/menu example/menu.lua`

## ? LS SDK ???

????? Hanbot ???

```lua
local pred = module.internal('pred')
local orb = module.internal('orb')
local TS = module.internal('TS')
player:castSpell('pos', slot, pos)
player:castSpell('obj', slot, target)
```

?? BlueAi ? LS ???

```lua
Q:Cast(target, HitChance.High)
Q:Cast(position)
E:CastOnUnit(target)
TargetSelector.GetTarget(...)
Orbwalker.CanUseSpell()
```

????????????? Hanbot ? pred/TS/orb/castSpell ?? LS ? SDKSpell/TargetSelector/Orbwalker?
