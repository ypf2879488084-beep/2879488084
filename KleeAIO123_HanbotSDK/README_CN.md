# Hanbot SDK Local Organized Copy

Source repository:
https://github.com/KleeAIO123/HanbotSDK

## ????

??? Hanbot/HanbotND Lua SDK ?????????

```lua
local pred = module.internal('pred')
local ts = module.internal('TS')
local orb = module.internal('orb')
player:castSpell('pos', 0, pos)
player:castSpell('obj', 0, target)
```

??? BlueAi/LS ????????

```lua
Champions.Q = SDKSpell.Create(...)
Q:Cast(target, HitChance.High)
Q:Cast(position)
E:CastOnUnit(target)
TargetSelector.GetTarget(...)
Orbwalker.CanUseSpell()
```

?? Hanbot SDK ?????????target_filter?trace_filter?pred_input?collision?castSpell ???
????? Hanbot ????? LS ????????? LS ? SDKSpell / TargetSelector / Orbwalker ???

## Recommended Reading

1. organized_docs/01_castSpell_api.md
2. organized_docs/02_pred_linear.md
3. organized_docs/03_pred_collision.md
4. organized_docs/05_TS_target_selection.md
5. organized_docs/00_full_content.md

## Original Web Page

Open docs.html to view the original webpage documentation.
