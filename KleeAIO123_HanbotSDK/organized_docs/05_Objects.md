#Objects
###base.obj
Properties:<br>

 * `boolean` base.valid
 * `number` base.type
 * `number` base.index
> The index of object
 * `number` base.index32
> The object_id of object
 * `number` base.team
 * `string` base.name
 * `number` base.networkID
 * `number` base.networkID32
> The network_id of object
 * `number` base.x
 * `number` base.y
 * `number` base.z
 * `vec3` base.pos
 * `vec2` base.pos2D
 * `boolean` base.isOnScreen
 * `number` base.selectionHeight
 * `number` base.selectionRadius
 * `vec3` base.minBoundingBox
 * `vec3` base.maxBoundingBox

###hero.obj

Properties:<br>

 * `string` hero.name
 * `string` hero.charName
 * `string` hero.recallName
 * `texture.obj` hero.iconCircle
 * `texture.obj` hero.iconSquare
 * `boolean` hero.isOnScreen
 * `boolean` hero.inShopRange
 * `boolean` hero.isDead
 * `boolean` hero.isAlive
 * `boolean` hero.isVisible
 * `boolean` hero.isRecalling
 * `boolean` hero.isTargetable
 * `boolean` hero.parEnabled
 * `boolean` hero.sarEnabled
 * `vec3` hero.pos
 * `vec3` hero.direction
 * `vec2` hero.pos2D
 * `vec2` hero.direction2D
 * `vec2` hero.barPos
 * `path.obj` hero.path
 * `spell.obj` hero.activeSpell
 * `table` hero.buff

```lua
-- use BUFF_XXX for buff type
if hero.buff[BUFF_BLIND] then
	print('player blind')
end

-- Use the name(in lowercase) to get the the specified name
if hero.buff['kaisaeevolved'] then
	print('has buff KaisaEEvolved')
end
```

 * `runemanager.obj` hero.rune
 * `number` hero.type
 * `number` hero.index
 * `number` hero.networkID
 * `number` hero.networkID32
 * `number` hero.team
 * `number` hero.x
 * `number` hero.y
 * `number` hero.z
 * `number` hero.selectionHeight
 * `number` hero.selectionRadius
 * `number` hero.boundingRadius
 * `number` hero.overrideCollisionRadius
 * `number` hero.pathfindingCollisionRadius
 * `vec3` hero.minBoundingBox
 * `vec3` hero.maxBoundingBox
 * `number` hero.deathTime
 * `number` hero.health
 * `number` hero.maxHealth
 * `number` hero.maxHealthPenalty
 * `number` hero.allShield
 * `number` hero.physicalShield
 * `number` hero.magicalShield
 * `number` hero.champSpecificHealth
 * `number` hero.stopShieldFade
 * `number` hero.isTargetableToTeamFlags
 * `number` hero.mana
 * `number` hero.maxMana
 * `number` hero.baseAttackDamage
 * `number` hero.baseAd
> alias of `baseAttackDamage`
 * `number` hero.bonusAd
 * `number` hero.totalAd
> The TotalAttackDamage
 * `number` hero.totalAp
> The TotalAbilityPower
 * `number` hero.armor
 * `number` hero.spellBlock
 * `number` hero.attackSpeedMod
 * `number` hero.flatPhysicalDamageMod
 * `number` hero.percentPhysicalDamageMod
 * `number` hero.flatMagicDamageMod
 * `number` hero.percentMagicDamageMod
 * `number` hero.healthRegenRate
 * `number` hero.bonusArmor
 * `number` hero.bonusSpellBlock
 * `number` hero.flatBubbleRadiusMod
 * `number` hero.percentBubbleRadiusMod
 * `number` hero.moveSpeed
 * `number` hero.moveSpeedBaseIncrease
 * `number` hero.scaleSkinCoef
 * `number` hero.gold
 * `number` hero.goldTotal
 * `number` hero.minimumGold
 * `number` hero.evolvePoints
 * `number` hero.evolveFlag
 * `number` hero.inputLocks
 * `number` hero.skillUpLevelDeltaReplicate
 * `number` hero.manaCost0
 * `number` hero.manaCost1
 * `number` hero.manaCost2
 * `number` hero.manaCost3
 * `number` hero.baseAbilityDamage
 * `number` hero.dodge
 * `number` hero.crit
 * `number` hero.parRegenRate
 * `number` hero.attackRange
 * `number` hero.flatMagicReduction
 * `number` hero.percentMagicReduction
 * `number` hero.flatCastRangeMod
 * `number` hero.percentCooldownMod
 * `number` hero.passiveCooldownEndTime
 * `number` hero.passiveCooldownTotalTime
 * `number` hero.flatArmorPenetration
 * `number` hero.percentArmorPenetration
 * `number` hero.flatMagicPenetration
 * `number` hero.percentMagicPenetration
 * `number` hero.percentLifeStealMod
 * `number` hero.percentSpellVampMod
 * `number` hero.percentOmnivamp
 * `number` hero.percentPhysicalVamp
 * `number` hero.percentBonusArmorPenetration
 * `number` hero.percentCritBonusArmorPenetration
 * `number` hero.percentCritTotalArmorPenetration
 * `number` hero.percentBonusMagicPenetration
 * `number` hero.physicalLethality
 * `number` hero.magicLethality
 * `number` hero.baseHealthRegenRate
 * `number` hero.primaryARBaseRegenRateRep
 * `number` hero.secondaryARRegenRateRep
 * `number` hero.secondaryARBaseRegenRateRep
 * `number` hero.percentCooldownCapMod
 * `number` hero.percentEXPBonus
 * `number` hero.flatBaseAttackDamageMod
 * `number` hero.percentBaseAttackDamageMod
 * `number` hero.baseAttackDamageSansPercentScale
 * `number` hero.exp
 * `number` hero.par
 * `number` hero.maxPar
 * `number` hero.sar
 * `number` hero.maxSar
 * `number` hero.pathfindingRadiusMod
 * `number` hero.levelRef
 * `number` hero.numNeutralMinionsKilled
 * `number` hero.primaryArRegenRateRep
 * `number` hero.physicalDamagePercentageModifier
 * `number` hero.magicalDamagePercentageModifier
 * `number` hero.baseHealth
 * `number` hero.baseMana
 * `number` hero.baseManaPerLevel
 * `number` hero.combatType
 * `number` hero.critDamageMultiplier
 * `number` hero.abilityHasteMod
 * `number` hero.baseMoveSpeed
 * `number` hero.baseAttackRange
 * `bool` hero.isZombie
 * `bool` hero.isMelee
 * `bool` hero.isRanged
 * `bool` hero.isBot
 * `bool` hero.isMe
 
 
__The following functions are limited to player only:__<br>
####player:move(v1)
Parameters<br>
`hero.obj` player<br>
`vec3` v1<br>
Return Value<br>
`void`<br>
####player:attackmove(v1)
Parameters<br>
`hero.obj` player<br>
`vec3` v1<br>
Return Value<br>
`void`<br>
####player:altmove(v1)
Parameters<br>
`hero.obj` player<br>
`vec3` v1<br>
Return Value<br>
`void`<br>
####player:attack(obj)
Parameters<br>
`hero.obj` player<br>
`obj` obj<br>
Return Value<br>
`void`<br>
####player:altattack(obj)
Parameters<br>
`hero.obj` player<br>
`obj` obj<br>
Return Value<br>
`void`<br>
####player:stop()
Parameters<br>
`hero.obj` player<br>
Return Value<br>
`void`<br>
####player:select(n)
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
`hero.obj` player<br>
`number` slot<br>
Return Value<br>
`void`<br>
####player:interact(obj)
Parameters<br>
`hero.obj` player<br>
`obj` obj<br>
Return Value<br>
`void`<br>
####player:buyItem(itemID)
Parameters<br>
`hero.obj` player<br>
`number` itemID<br>
Return Value<br>
`void`<br>
<br>
__The following functions are available for all hero.obj__<br>
####hero:spellSlot(slot)
Parameters<br>
`hero.obj` hero<br>
`number` slot<br>
Return Value<br>
`spell_slot.obj`<br>
####hero:findSpellSlot(spellName)
Parameters<br>
`hero.obj` hero<br>
`string` spell name<br>
Return Value<br>
`spell_slot.obj`<br>
####hero:inventorySlot(slot)
Parameters<br>
`hero.obj` hero<br>
`number` slot<br>
Return Value<br>
`inventory_slot.obj`<br>
####hero:basicAttack(index)
Parameters<br>
`hero.obj` hero<br>
`number` index, -1 to get the default AA spell<br>
Return Value<br>
`spell.obj`<br>
####hero:itemID(slot)
Parameters<br>
`hero.obj` hero<br>
`number` slot<br>
Return Value<br>
`number` returns item ID for item slot i<br>

####hero:isPlayingAnimation(animationNameHash)
Parameters<br>
`hero.obj` hero<br>
`number` animationNameHash<br>
Return Value<br>
`boolean`<br>

####hero:attackDelay()
Parameters<br>
`hero.obj` hero<br>
Return Value<br>
`number`<br>

####hero:attackCastDelay(slot)
Parameters<br>
`hero.obj` hero<br>
`number` spellSlot<br>
Return Value<br>
`number`<br>

####hero:getPassablePos(to)
Parameters<br>
`hero.obj` hero<br>
`vec3` to pos<br>
Return Value<br>
`vec3` The NearstPassable position (the cell center, and include hero collsion state)<br>

####hero:baseHealthForLevel(level)
Parameters<br>
`number` level<br>
Return Value<br>
`number` returns base health for level i<br>

####hero:abilityResourceBase(slot)
Parameters<br>
`number` slot, usually the slot is 0 for mana<br>
Return Value<br>
`number` returns ability resource value (with level factor calculated)<br>

####hero:abilityResourceForLevel(slot, level)
Parameters<br>
`number` slot, usually the slot is 0 for mana<br>
`number` level<br>
Return Value<br>
`number` returns ability resource value for level<br>

####hero:statForLevel(type, level)
Parameters<br>
`number` type<br>
`number` level<br>
Return Value<br>
`number` returns stat of type for level i<br>

####hero:getStat(name)
Parameters<br>
`string` name<br>
Return Value<br>
`number` returns stat value<br>

The available stats (Some of them are deprecated by riot and always zero):

 * EXP	
 * GOLD_SPENT	
 * GOLD_EARNED	
 * MINIONS_KILLED	
 * NEUTRAL_MINIONS_KILLED	
 * NEUTRAL_MINIONS_KILLED_YOUR_JUNGLE	
 * NEUTRAL_MINIONS_KILLED_ENEMY_JUNGLE	
 * PLAYER_SCORE_0	
 * PLAYER_SCORE_1	
 * PLAYER_SCORE_2	
 * PLAYER_SCORE_3	
 * PLAYER_SCORE_4	
 * PLAYER_SCORE_5	
 * PLAYER_SCORE_6	
 * PLAYER_SCORE_7	
 * PLAYER_SCORE_8	
 * PLAYER_SCORE_9	
 * PLAYER_SCORE_10	
 * PLAYER_SCORE_11	
 * VICTORY_POINT_TOTAL	
 * TOTAL_DAMAGE_DEALT	
 * PHYSICAL_DAMAGE_DEALT_PLAYER	
 * MAGIC_DAMAGE_DEALT_PLAYER	
 * TRUE_DAMAGE_DEALT_PLAYER	
 * TOTAL_DAMAGE_DEALT_TO_CHAMPIONS	
 * PHYSICAL_DAMAGE_DEALT_TO_CHAMPIONS	
 * MAGIC_DAMAGE_DEALT_TO_CHAMPIONS	
 * TRUE_DAMAGE_DEALT_TO_CHAMPIONS	
 * TOTAL_DAMAGE_TAKEN	
 * PHYSICAL_DAMAGE_TAKEN	
 * MAGIC_DAMAGE_TAKEN	
 * TRUE_DAMAGE_TAKEN	
 * TOTAL_DAMAGE_SELF_MITIGATED	
 * TOTAL_DAMAGE_SHIELDED_ON_TEAMMATES	
 * TOTAL_DAMAGE_DEALT_TO_BUILDINGS	
 * TOTAL_DAMAGE_DEALT_TO_TURRETS	
 * TOTAL_DAMAGE_DEALT_TO_OBJECTIVES	
 * LARGEST_ATTACK_DAMAGE	
 * LARGEST_ABILITY_DAMAGE	
 * LARGEST_CRITICAL_STRIKE	
 * TOTAL_TIME_CROWD_CONTROL_DEALT	
 * TOTAL_TIME_CROWD_CONTROL_DEALT_TO_CHAMPIONS	
 * TOTAL_HEAL_ON_TEAMMATES	
 * TIME_PLAYED	
 * LONGEST_TIME_SPENT_LIVING	
 * TOTAL_TIME_SPENT_DEAD	
 * TIME_OF_FROM_LAST_DISCONNECT	
 * TIME_SPENT_DISCONNECTED	
 * TIME_CCING_OTHERS	
 * TEAM	
 * LEVEL	
 * CHAMPIONS_KILLED	
 * NUM_DEATHS	
 * ASSISTS	
 * LARGEST_KILLING_SPREE	
 * KILLING_SPREES	
 * LARGEST_MULTI_KILL	
 * BOUNTY_LEVEL	
 * DOUBLE_KILLS	
 * TRIPLE_KILLS	
 * QUADRA_KILLS	
 * PENTA_KILLS	
 * UNREAL_KILLS	
 * BARRACKS_KILLED	
 * BARRACKS_TAKEDOWNS	
 * TURRETS_KILLED	
 * TURRET_TAKEDOWNS	
 * HQ_KILLED	
 * HQ_TAKEDOWNS	
 * OBJECTIVES_STOLEN	
 * OBJECTIVES_STOLEN_ASSISTS	
 * FRIENDLY_DAMPEN_LOST	
 * FRIENDLY_TURRET_LOST	
 * FRIENDLY_HQ_LOST	
 * BARON_KILLS	
 * DRAGON_KILLS	
 * RIFT_HERALD_KILLS
 * HORDE_KILLS
 * ATAKHAN_KILLS
 * NODE_CAPTURE	
 * NODE_CAPTURE_ASSIST	
 * NODE_NEUTRALIZE	
 * NODE_NEUTRALIZE_ASSIST	
 * TEAM_OBJECTIVE	
 * ITEMS_PURCHASED	
 * CONSUMABLES_PURCHASED	
 * ITEM0	
 * ITEM1	
 * ITEM2	
 * ITEM3	
 * ITEM4	
 * ITEM5	
 * ITEM6	
 * PERK_PRIMARY_STYLE	
 * PERK_SUB_STYLE	
 * STAT_PERK_0	
 * STAT_PERK_1	
 * STAT_PERK_2	
 * SIGHT_WARDS_BOUGHT_IN_GAME	
 * VISION_WARDS_BOUGHT_IN_GAME	
 * WARD_PLACED	
 * WARD_KILLED	
 * WARD_PLACED_DETECTOR	
 * VISION_SCORE	
 * SPELL1_CAST	
 * SPELL2_CAST	
 * SPELL3_CAST	
 * SPELL4_CAST	
 * SUMMON_SPELL1_CAST	
 * SUMMON_SPELL2_CAST	
 * KEYSTONE_ID	
 * TOTAL_HEAL	
 * TOTAL_UNITS_HEALED	
 * WAS_AFK	
 * WAS_AFK_AFTER_FAILED_SURRENDER	
 * WAS_EARLY_SURRENDER_ACCOMPLICE	
 * TEAM_EARLY_SURRENDERED	
 * GAME_ENDED_IN_EARLY_SURRENDER	
 * GAME_ENDED_IN_SURRENDER	
 * WAS_SURRENDER_DUE_TO_AFK	
 * WAS_LEAVER	
 * PLAYERS_I_MUTED	
 
####hero:isValidTarget(range)
Parameters<br>
`hero.obj` hero<br>
`number` range, optional <br>
Return Value<br>
`bool` Returns whether this is valid target to self or not<br>
 
####hero:findBuff(hash)
Equal to `player.buff["some_name"] and player.buff["some_name"] or nil` <br>
Parameters<br>
`hero.obj` hero<br>
`int` fnv hash of buff name<br>
Return Value<br>
`buff.obj` <br>
 
####hero:getBuffStacks(hash)
Equal to `player.buff["some_name"] and player.buff["some_name"].stacks or 0` <br>
Parameters<br>
`hero.obj` hero<br>
`int` fnv hash of buff name<br>
Return Value<br>
`int` <br>
 
####hero:getBuffCount(hash)
Equal to `player.buff["some_name"] and player.buff["some_name"].stacks2 or 0` <br>
Parameters<br>
`hero.obj` hero<br>
`int` fnv hash of buff name<br>
Return Value<br>
`int` <br>

```lua
local ezrealpassivestacks = game.fnvhash("ezrealpassivestacks")
cb.add(cb.tick, function()
	local stacks = player:getBuffStacks(ezrealpassivestacks)
	if stacks > 0 then
		-- do somethings
	end
end)
```

####hero:getTeamBuffCount(team, buffType)
Parameters<br>
`hero.obj` hero<br>
`int` team<br>
`int` buffType<br>
Return Value<br>
`int` <br>

The available buffType:
 * DragonFireStacks = 0x1,
 * DragonAirStacks = 0x2,
 * DragonWaterStacks = 0x3,
 * DragonEarthStacks = 0x4,
 * DragonElderStacks = 0x5,

```lua
print(player:getTeamBuffCount(TEAM_ALLY, 0))
print(player:getTeamBuffCount(TEAM_ENEMY, 0))
```

###minion.obj
Properties:<br>

 * `string` minion.name
 * `string` minion.charName
 * `boolean` minion.isOnScreen
 * `boolean` minion.isDead
 * `boolean` minion.isAlive
 * `boolean` minion.isVisible
 * `boolean` minion.isTargetable
 * `vec3` minion.pos
 * `vec3` minion.direction
 * `vec2` minion.pos2D
 * `vec2` minion.direction2D
 * `vec2` minion.barPos
 * `path.obj` minion.path
 * `hero.obj` minion.owner
 * `spell.obj` minion.activeSpell
 * `table` minion.buff
 * `number` minion.networkID
 * `number` minion.networkID32
 * `number` minion.team
 * `number` minion.x
 * `number` minion.y
 * `number` minion.z
 * `number` minion.selectionHeight
 * `number` minion.selectionRadius
 * `number` minion.boundingRadius
 * `number` minion.overrideCollisionRadius
 * `number` minion.pathfindingCollisionRadius
 * `vec3` minion.minBoundingBox
 * `vec3` minion.maxBoundingBox
 * `number` minion.deathTime
 * `number` minion.health
 * `number` minion.maxHealth
 * `number` minion.mana
 * `number` minion.maxMana
 * `number` minion.maxHealthPenalty
 * `number` minion.physicalShield
 * `number` minion.magicalShield
 * `number` minion.allShield
 * `number` minion.stopShieldFade
 * `number` minion.isTargetableToTeamFlags
 * `number` minion.actionState
 * `number` minion.baseAttackDamage
 * `number` minion.baseAd
> alias of `baseAttackDamage`
 * `number` minion.bonusAd
 * `number` minion.totalAd
> The TotalAttackDamage
 * `number` minion.totalAp
> The TotalAbilityPower
 * `number` minion.armor
 * `number` minion.spellBlock
 * `number` minion.attackSpeedMod
 * `number` minion.flatPhysicalDamageMod
 * `number` minion.percentPhysicalDamageMod
 * `number` minion.flatMagicDamageMod
 * `number` minion.percentMagicDamageMod
 * `number` minion.healthRegenRate
 * `number` minion.bonusArmor
 * `number` minion.bonusSpellBlock
 * `number` minion.moveSpeed
 * `number` minion.moveSpeedBaseIncrease
 * `number` minion.baseAbilityDamage
 * `number` minion.attackRange
 * `number` minion.flatMagicReduction
 * `number` minion.percentMagicReduction
 * `number` minion.flatArmorPenetration
 * `number` minion.percentArmorPenetration
 * `number` minion.flatMagicPenetration
 * `number` minion.percentMagicPenetration
 * `number` minion.physicalLethality
 * `number` minion.magicLethality
 * `number` minion.flatBaseAttackDamageMod
 * `number` minion.percentBaseAttackDamageMod
 * `number` minion.baseAttackDamageSansPercentScale
 * `number` minion.exp
 * `number` minion.par
 * `number` minion.maxPar
 * `number` minion.parEnabled
 * `number` minion.percentDamageToBarracksMinionMod
 * `number` minion.flatDamageReductionFromBarracksMinionMod
 * `bool` minion.isMelee
 * `bool` minion.isRanged
 * `bool` minion.isClone
 * `bool` minion.isLaneMinion
 * `bool` minion.isEliteMinion
 * `bool` minion.isEpicMinion
 * `bool` minion.isJungleMonster
 * `bool` minion.isLaneMinion
 * `bool` minion.isSiegeMinion
 * `bool` minion.isSuperMinion
 * `bool` minion.isCasterdMinion
 * `bool` minion.isMeleeMinion
 * `bool` minion.isBarrel
 * `bool` minion.isPet
 * `bool` minion.isCollidablePet
 * `bool` minion.isTrap
 * `bool` minion.isWard
 * `bool` minion.isWardNoBlue
 * `bool` minion.isPlant
 * `bool` minion.isMonster
 * `bool` minion.isLargeMonster
 * `bool` minion.isBaron
 * `bool` minion.isDragon
 * `bool` minion.isEpicMonster
 * `bool` minion.isSmiteMonster
 
####m:basicAttack(index)
Parameters<br>
`minion.obj` m<br>
`number` index, -1 to get the default AA spell<br>
Return Value<br>
`spell.obj` returns the minions basic attack<br>

####m:isPlayingAnimation(animationNameHash)
Parameters<br>
`minion.obj` m<br>
`number` animationNameHash<br>
Return Value<br>
`boolean`<br>

####m:attackDelay()
Parameters<br>
`minion.obj` m<br>
Return Value<br>
`number`<br>

####m:attackCastDelay(slot)
Parameters<br>
`minion.obj` m<br>
`number` spellSlot<br>
Return Value<br>
`number`<br>

####m:isValidTarget(range)
Parameters<br>
`m.obj` m<br>
`number` range, optional <br>
Return Value<br>
`bool` Returns whether this is valid target to self or not<br>

###turret.obj
Properties:<br>

 * `string` turret.name
 * `string` turret.charName
 * `boolean` turret.isOnScreen
 * `boolean` turret.isDead
 * `boolean` turret.isAlive
 * `boolean` turret.isVisible
 * `boolean` turret.isTargetable
 * `vec3` turret.pos
 * `vec3` turret.direction
 * `vec2` turret.pos2D
 * `vec2` turret.barPos
 * `vec2` turret.direction2D
 * `path.obj` turret.path
 * `spell.obj` turret.activeSpell
 * `table` turret.buff
 * `number` turret.networkID
 * `number` turret.networkID32
 * `number` turret.team
 * `number` turret.x
 * `number` turret.y
 * `number` turret.z
 * `number` turret.selectionHeight
 * `number` turret.selectionRadius
 * `number` turret.boundingRadius
 * `number` turret.overrideCollisionRadius
 * `number` turret.pathfindingCollisionRadius
 * `vec3` turret.minBoundingBox
 * `vec3` turret.maxBoundingBox
 * `number` turret.deathTime
 * `number` turret.health
 * `number` turret.maxHealth
 * `number` turret.mana
 * `number` turret.maxMana
 * `number` turret.allShield
 * `number` turret.isTargetableToTeamFlags
 * `number` turret.baseAttackDamage
 * `number` turret.baseAd
> alias of `baseAttackDamage`
 * `number` turret.bonusAd
 * `number` turret.totalAd
> The TotalAttackDamage
 * `number` turret.totalAp
> The TotalAbilityPower
 * `number` turret.armor
 * `number` turret.spellBlock
 * `number` turret.attackSpeedMod
 * `number` turret.flatPhysicalDamageMod
 * `number` turret.percentPhysicalDamageMod
 * `number` turret.flatMagicDamageMod
 * `number` turret.percentMagicDamageMod
 * `number` turret.healthRegenRate
 * `number` turret.bonusArmor
 * `number` turret.bonusSpellBlock
 * `number` turret.baseAbilityDamage
 * `number` turret.parRegenRate
 * `number` turret.attackRange
 * `number` turret.flatMagicReduction
 * `number` turret.percentMagicReduction
 * `number` turret.flatArmorPenetration
 * `number` turret.percentArmorPenetration
 * `number` turret.flatMagicPenetration
 * `number` turret.percentMagicPenetration
 * `number` turret.percentBonusArmorPenetration
 * `number` turret.percentBonusMagicPenetration
 * `number` turret.physicalLethality
 * `number` turret.magicLethality
 * `number` turret.baseHealthRegenRate
 * `number` turret.secondaryARBaseRegenRateRep
 * `number` turret.flatBaseAttackDamageMod
 * `number` turret.percentBaseAttackDamageMod
 * `number` turret.baseAttackDamageSansPercentScale
 * `number` turret.exp
 * `number` turret.par
 * `number` turret.maxPar
 * `number` turret.parEnabled
 * `number` turret.physicalDamagePercentageModifier
 * `number` turret.magicalDamagePercentageModifier
 * `bool` turret.isMelee
 * `bool` turret.isRanged
 * `number` turret.tier
> Base=1, Inner=2, Outer=3, NexusRight=4, NexusLeft=5
 * `number` turret.lane
> Bottom=0, Mid=1, Top=2
 
####t:basicAttack(i)
Parameters<br>
`turret.obj` t<br>
`number` i<br>
Return Value<br>
`spell.obj` returns the turrets basic attack<br>

####t:isPlayingAnimation(animationNameHash)
Parameters<br>
`turret.obj` t<br>
`number` animationNameHash<br>
Return Value<br>
`boolean`<br>

####t:attackDelay()
Parameters<br>
`turret.obj` t<br>
Return Value<br>
`number`<br>

####t:attackCastDelay(slot)
Parameters<br>
`turret.obj` t<br>
`number` spellSlot<br>
Return Value<br>
`number`<br>

####t:isValidTarget(range)
Parameters<br>
`turret.obj` t<br>
`number` range, optional <br>
Return Value<br>
`bool` Returns whether this is valid target to self or not<br>

###inhib.obj
Properties:<br>

 * `number` inhib.type
 * `number` inhib.index
 * `number` inhib.team
 * `number` inhib.networkID
 * `number` inhib.networkID32
 * `string` inhib.name
 * `number` inhib.x
 * `number` inhib.y
 * `number` inhib.z
 * `vec3` inhib.pos
 * `vec2` inhib.pos2D
 * `boolean` inhib.isOnScreen
 * `number` inhib.selectionHeight
 * `number` inhib.selectionRadius
 * `number` inhib.boundingRadius
 * `number` inhib.overrideCollisionRadius
 * `number` inhib.pathfindingCollisionRadius
 * `vec3` inhib.minBoundingBox
 * `vec3` inhib.maxBoundingBox
 * `boolean` inhib.isDead
 * `boolean` inhib.isAlive
 * `boolean` inhib.isVisible
 * `number` inhib.deathTime
 * `number` inhib.health
 * `number` inhib.maxHealth
 * `number` inhib.allShield
 * `boolean` inhib.isTargetable
 * `number` inhib.isTargetableToTeamFlags

####inhib:isValidTarget(range)
Parameters<br>
`inhib.obj` inhib<br>
`number` range, optional <br>
Return Value<br>
`bool` Returns whether this is valid target to self or not<br>

###nexus.obj
Properties:<br>

 * `string` nexus.name
 * `boolean` nexus.isOnScreen
 * `boolean` nexus.isDead
 * `boolean` nexus.isAlive
 * `boolean` nexus.isVisible
 * `boolean` nexus.isTargetable
 * `vec3` nexus.pos
 * `vec2` nexus.pos2D
 * `number` nexus.team
 * `number` nexus.type
 * `number` nexus.x
 * `number` nexus.y
 * `number` nexus.z
 * `number` nexus.health
 * `number` nexus.maxHealth
 * `number` nexus.allShield
 * `number` nexus.isTargetableToTeamFlags
 
####nexus:isValidTarget(range)
Parameters<br>
`nexus.obj` nexus<br>
`number` range, optional <br>
Return Value<br>
`bool` Returns whether this is valid target to self or not<br>

###missile.obj
Properties:<br>

 * `number` missile.type
 * `number` missile.index
 * `number` missile.index32
 * `number` missile.team
 * `string` missile.name
 * `number` missile.networkID
 * `number` missile.networkID32
 * `boolean` missile.isOnScreen
 * `number` missile.selectionHeight
 * `number` missile.selectionRadius
 * `vec3` missile.minBoundingBox
 * `vec3` missile.maxBoundingBox
 * `number` missile.x
 * `number` missile.y
 * `number` missile.z
 * `vec3` missile.pos
 * `vec2` missile.pos2D
> The `x`/`y`/`z`/`pos`/`pos2D` now means `minBoundingBox` of `GameObject`
 * `spell.obj` missile.spell
 * `base.obj` missile.caster
 * `base.obj` missile.target
 * `number` missile.width
 * `number` missile.velocity
 * `missile_info.obj` missile.missile_info
> The `MissileMovement` of `Missile`, And follow properties is getting from this as a alias: 
 * `vec3` missile.startPos
 * `vec2` missile.startPos2D
 * `vec3` missile.endPos
 * `vec2` missile.endPos2D
 * `number` missile.speed


###particle.obj
Properties:<br>

 * `number` particle.type
 * `number` particle.index
 * `number` particle.index32
 * `number` particle.team
 * `string` particle.name
 * `number` particle.networkID
 * `number` particle.networkID32
 * `number` particle.x
 * `number` particle.y
 * `number` particle.z
 * `number` particle.effectKey
> The hash of effect resource name, only valid for effects from spell (invalid for missile/sound/etc)
 * `vec3` particle.pos
 * `vec2` particle.pos2D
 * `vec3` particle.initPos
> The initial position when effect created, only valid for effects from spell
 * `vec3` particle.initTargetPos
> The initial target position when effect created, only valid for effects from spell
 * `vec3` particle.initOrientation
> The initial orientation when effect created, only valid for effects from spell
 * `vec3` particle.direction
> The effect drection when rendering.
 * `boolean` particle.isOnScreen
 * `number` particle.selectionHeight
 * `number` particle.selectionRadius
 * `vec3` particle.minBoundingBox
 * `vec3` particle.maxBoundingBox
 * `obj` particle.caster
> The initial caster/emitter when effect created, only valid for effects from spell, could be nil
 * `obj` particle.target
> The initial target when effect created, only valid for effects from spell, could be nil
 * `obj` particle.attachmentObject
 * `obj` particle.targetAttachmentObject


###spell.obj
> known as `SpellCastInfo`

Properties:<br>

 * `number` spell.identifier
> The `missileNetworkID` of `SpellCastInfo`
 * `number` spell.slot
 * `boolean` spell.isBasicAttack
 * `obj` spell.owner
 * `boolean` spell.hasTarget
 * `obj` spell.target
 * `vec3` spell.startPos
 * `vec2` spell.startPos2D
> `LaunchPosition`
 * `vec3` spell.endPos
 * `vec2` spell.endPos2D
> `TargetPosition`
 * `vec3` spell.endPosLine
 * `vec2` spell.endPosLine2D
> `TargetEndPosition`
 * `boolean` spell.useChargeChanneling
 * `boolean` spell.channelingFinished
 * `boolean` spell.spellCasted
 * `number` spell.windUpTime
> `DesignerCastTime` + `ExtraTimeForCast`
 * `number` spell.animationTime
> `DesignerTotalTime`
 * `number` spell.clientWindUpTime
> `CharacterAttackCastDelay`
 * `number` spell.startTime
> `TimeTillPlayAnimation`
 * `number` spell.castEndTime
> `TimeCast`
 * `number` spell.endTime
> `TimeSpellEnd`
 * `spell_info.obj` spell.spell_info
> The `SpellData` of current `SpellCastInfo`
 * `string` spell.name
> equal to `spell.spell_info.name`
 * `string` spell.hash
> equal to `spell.spell_info.hash`
 * `spell_static.obj` spell.static
> equal to `spell.spell_info.static`

###spell_slot.obj
> known as `SpellDataInst`

Properties:<br>

 * `number` spell_slot.slot
 * `boolean` spell_slot.isBasicSpellSlot
 * `boolean` spell_slot.isSummonerSpellSlot
 * `string` spell_slot.name
 * `number` spell_slot.hash
 * `texture.obj` spell_slot.icon
 * `number` spell_slot.targetingType
 * `number` spell_slot.level
 * `number` spell_slot.cooldown
 * `number` spell_slot.totalCooldown
 * `number` spell_slot.iconUsed
> For champion like Bel'Veth, the index of spell icon (Q Spell)
 * `number` spell_slot.startTimeForCurrentCast
 * `number` spell_slot.displayRange
 * `number` spell_slot.currentNumericalDisplay
 * `number` spell_slot.stacks
> `CurrentAmmo`
 * `number` spell_slot.stacksCooldown
> `TimeForNextAmmoRecharge`
 * `number` spell_slot.state
 * `number` spell_slot.toggleState
 * `boolean` spell_slot.isCharging
 * `boolean` spell_slot.isNotEmpty
> Whether current `spell_slot` has a active `spell_info` 
 * `spell_info.obj` spell_slot.spell_info
 * `spell_static.obj` spell_slot.static
 

####spell_slot:getTooltip(type)
Parameters<br>
`spell_slot.obj`<br>
`int` tooltip type: 0<br>
Return Value<br>
`string`<br>

####spell_slot:getTooltipVar(index)
Return the numerical variable when mouseover the skill icons<br>
Parameters<br>
`spell_slot.obj`<br>
`int` tooltip var index: [0,15]<br>
Return Value<br>
`number`<br>

####spell_slot:getEffectAmount(index, level)
Return the fixed class value of the target skill<br>
Parameters<br>
`spell_slot.obj`<br>
`int` index: [1,11]<br>
`int` level: [0,6]<br>
Return Value<br>
`number`<br>

####spell_slot:calculate(spellNameHash, calculationHash)
Parameters<br>
`spell_slot.obj` current spell<br>
`unsigned int` spell name hash, could be 0 if using default spell name<br>
`unsigned int` calculation type hash<br>
Return Value<br>
`void`<br>

```
-- Jhin Example: 
-- https://raw.communitydragon.org/13.15/game/data/characters/jhin/jhin.bin.json
-- JhinW: ["Characters/Jhin/Spells/JhinRAbility/JhinW"].mSpell.mSpellCalculations
-- JhinR: ["Characters/Jhin/Spells/JhinRAbility/JhinR"].mSpell.mSpellCalculations

local calcHashW = game.fnvhash('TotalDamage')
local rawDamageW = player:spellSlot(0):calculate(0, calcHashW)

local calcHashR = game.fnvhash('DamageCalc')
local rawDamageR = player:spellSlot(3):calculate(0, calcHashR)


-- AatroxQ Example:
-- The `spellSlot(0).name` could be "AatroxQ"/"AatroxQ2"/"AatroxQ3"
-- We need use "AatroxQ" to calculate the damage.

local QDamage = game.fnvhash('QDamage')
local AatroxQ = game.spellhash('AatroxQ')
local rawDamageQ1 = player:spellSlot(0):calculate(AatroxQ, QDamage)
local rawDamageQ2 = player:spellSlot(0):calculate(AatroxQ, QDamage) * 1.25
local rawDamageQ3 = player:spellSlot(0):calculate(AatroxQ, QDamage) * 1.25 * 1.25

```

####spell_slot:getDamage(target, spellHash, stage)
Parameters<br>
`spell_slot.obj` current spell<br>
`int` spell name hash, could be 0 if using default spell name<br>
`int` stage, 0 for default, 1/2/3 for custom usage<br>
Return Value<br>
`void`<br>

```lua
-- AatroxQ
local spellHash_AatroxQ = game.spellhash('AatroxQ')
local spellHash_AatroxQ2 = game.spellhash('AatroxQ2')
local spell = player:spellSlot(_Q)
print(spell:getDamage(target, spellHash_AatroxQ, 0)) -- Q damage
print(spell:getDamage(target, spellHash_AatroxQ, 1)) -- Q edge damage
print(spell:getDamage(target, spellHash_AatroxQ2, 0)) -- Q2 damage (need pass AatroxQ2 as arg1)

-- AkaliP
local spellHash_AkaliP = game.spellhash('AkaliP')
local spell = player:spellSlot(63) -- 63 = Passive
print(spell:getDamage(target, spellHash_AkaliP, 3)) -- Akali passive damage for stage 3

-- AurelionSolR
local spellHash_AurelionSolR = game.spellhash('AurelionSolR')
local spell = player:spellSlot(_R)
print(spell:getDamage(target, spellHash_AurelionSolR, 0)) -- AurelionSol R damage
print(spell:getDamage(target, spellHash_AurelionSolR, 1)) -- AurelionSol R2 damage
```


###spell_info.obj
> known as `SpellData`

Properties:<br>

 * `string` spell_info.name
 * `number` spell_info.hash
> the fnvhash of name
 * `spell_static.obj` spell_info.static

###spell_static.obj
> known as `SpellDataResource`

Properties:<br>

 * `string` spell_static.alternateName
 * `string` spell_static.imgIconName
 * `number` spell_static.castType
> `Flags`
 * `boolean` spell_static.useMinimapTargeting
 * `number` spell_static.missileSpeed
 * `number` spell_static.lineWidth
 * `number` spell_static.castFrame

###inventory_slot.obj
Properties:<br>

 * `number` inventory_slot.stacks
 * `number` inventory_slot.purchaseTime
 * `boolean` inventory_slot.hasItem
 * `item_data.obj` inventory_slot.item
 * `texture.obj` inventory_slot.icon
 * `number` inventory_slot.spellStacks
 * `number` inventory_slot.id
 * `number` inventory_slot.maxStacks
 * `number` inventory_slot.cost
 * `string` inventory_slot.name
 * `string` inventory_slot.iconName
 * `texture.obj` inventory_slot.icon

####inventory_slot:getTooltip(type)
Parameters<br>
`inventory_slot.obj` current inventory<br>
`int` tooltip type: 0<br>
Return Value<br>
`string`<br>

####inventory_slot:calculate(calculationHash)
Parameters<br>
`inventory_slot.obj` current inventory<br>
`unsigned int` calculation type hash<br>
Return Value<br>
`void`<br>

###item_data.obj
Properties:<br>

 * `number` item_data.id
 * `number` item_data.maxStacks
 * `number` item_data.cost
 * `string` item_data.name
 * `string` item_data.iconName
 * `texture.obj` item_data.icon

###path.obj
Properties:<br>

 * `obj` path.owner
 * `boolean` path.isActive
 * `boolean` path.isMoving
> Sometimes player is moving but `path.isActive` will be `false` (eg: no path for short move).
 * `boolean` path.isDashing
 * `number` path.dashSpeed
 * `boolean` path.unstoppable
 * `vec3` path.endPos
 * `vec2` path.endPos2D
 * `vec3` path.serverPos
 * `vec2` path.serverPos2D
 * `vec3` path.serverVelocity
 * `vec2` path.serverVelocity2D
 * `vec3` path.startPoint
 * `vec3` path.endPoint
 * `vec3[]` path.point
> `WaypointList` array
 * `vec2[]` path.point2D
> `WaypointList` array
 * `number` path.index
> The index of next point
 * `number` path.count
> The count of `point`/`point2D`
 * `number` path.update
> `UpdateNumber`

```lua
cb.add(cb.path, function (obj)
  if obj.ptr == player.ptr then
    print("--------newpath")
    print("isActive: " .. tostring(obj.path.isActive))
    print("index: " .. obj.path.index)
    print("count: " .. obj.path.count)

    local pos = obj.path.serverPos
    print("serverPos: " .. pos.x .. "," .. pos.y .. "," .. pos.z)
    print("isDashing: " .. tostring(obj.path.isDashing))

    if obj.path.isDashing then
      print("dashSpeed: " .. obj.path.dashSpeed)
    end
  end
end)

cb.add(cb.draw, function()
	if player.path.active then
		graphics.draw_line_strip(player.path.point, 2, 0xFFFFFFFF, player.path.count+1)
	end
end)
```

 
####p:calcPos(v1)
Parameters<br>
`path.obj` p<br>
`vec3` v1<br>
Return Value<br>
`vec3[]` returns vec3 array containing path points<br>
`number` returns array length<br>
``` lua
cb.add(cb.draw, function()
  local p, n = player.path:calcPos(mousePos)
  for i = 0, n - 1 do
    graphics.draw_circle(p[i], 15, 2, 0xffffffff, 3)
  end
end)
```

####p:isDirectPath(v1, v2)
Parameters<br>
`path.obj` p<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`boolean` returns result<br>
`number[]` return lastReachedPos<br>
``` lua
local isDirect,lastReachedPos = player.path:isDirectPath(player.pos, mousePos)
if isDirect then
	print('lastReachedPos.x', lastReachedPos[0])
	print('lastReachedPos.y', lastReachedPos[1])
end
```


###buff.obj
Warning: <br>
`buff.obj` are temporary objects, their memory may change or become invalid at any time, please do not save `buff.obj` anywhere<br>

Properties:<br>

 * `number` buff.type
 * `string` buff.name
 * `number` buff.hash
> The fnvhash of buff.name
 * `boolean` buff.valid
 * `obj` buff.owner
 * `obj` buff.source
 * `number` buff.startTime
 * `number` buff.endTime
 * `number` buff.stacks
> Number of buff layers
 * `number` buff.stacks2
> The buff `Counter`
 * `number` buff.count
> same to stacks2

####buff:hasSource(src)
Parameters<br>
`buff.obj`<br>
`base.obj` game object: hero.obj/minion.obj/turret.obj<br>
Return Value<br>
`bool`<br>

####buff:getTooltipVar(index)
Return the numerical variable when mouseover the skill icons<br>
Parameters<br>
`buff.obj`<br>
`int` tooltip var index: [0,15]<br>
Return Value<br>
`number`<br>

###runemanager.obj
Properties:<br>

 * `number` runemanager.size

####runemanager:get(index)
Parameters<br>
`runemanager.obj` camp<br>
`number` index: the index to get<br>
Return Value<br>
`rune.obj` returns the rune of current index<br>



###rune.obj
Properties:<br>

 * `number` rune.id
 * `string` rune.name
 * `texture.obj` rune.icon

####rune:getTooltipVar(index)
Return the numerical variable when mouseover the icons<br>
Parameters<br>
`rune.obj`<br>
`int` tooltip var index: [0,15]<br>
Return Value<br>
`number`<br>
 
###camp.obj
Properties:<br>

 * `number` camp.type
 * `number` camp.index
 * `number` camp.index32
 * `number` camp.team
 * `string` camp.name
 * `number` camp.networkID
 * `number` camp.networkID32
 * `number` camp.x
 * `number` camp.y
 * `number` camp.z
 * `vec3` camp.pos
 * `vec2` camp.pos2D
 * `boolean` camp.isOnScreen
 * `number` camp.selectionHeight
 * `number` camp.selectionRadius
 * `vec3` camp.minBoundingBox
 * `vec3` camp.maxBoundingBox
 * `boolean` camp.active
 * `number` camp.spawnTime
 * `number` camp.count

####camp:getMinion(index)
Parameters<br>
`camp.obj` camp<br>
`number` index: the index to get<br>
Return Value<br>
`minion.obj` returns the minion of current index<br>
``` lua
for i=0,camp.count-1 do
	local minion = camp:getMinion(i)
	if minion then
		print(minion.name, minion.pos.x, minion.pos.z)
	end
end

```

###texture.obj
Properties:<br>
 * `number` texture.width
 * `number` texture.height
 * `string` texture.name

###shadereffect.obj
####effect:show()
Parameters<br>
`shadereffect.obj` effect<br>
Return Value<br>
`void`
####effect:hide()
Parameters<br>
`shadereffect.obj` effect<br>
Return Value<br>
`void`
####effect:attach(obj)
Parameters<br>
`shadereffect.obj` effect<br>
`base.obj` game object: hero.obj/minion.obj/turret.obj<br>
Return Value<br>
`void`
####effect:update_circle(pos, radius, width, color)
Update the circle info of current shadereffect.<br>
Parameters<br>
`shadereffect.obj` effect<br>
`vec3` effect center pos<br>
`number` radius<br>
`number` width<br>
`number` color, argb (rgb is ignored when effect type is CIRCLE_RAINBOW)<br>
Return Value<br>
`void`


###skillshot.obj (Evade3)

Properties:<br>

 * `obj` skillshot.Caster
 * `string` skillshot.SpellName
 * `spelldata.obj` skillshot.SpellData
 * `number` skillshot.DetectionType
 * `cast_info_saved.obj` skillshot.SpellCastInfoData
 * `number` skillshot.InitTick
 * `number` skillshot.StartTick
 * `number` skillshot.EndTick
> Ticks are based on game.time
 * `number` skillshot.TargetHandle
> The ObjID
 * `boolean` skillshot.IsGlobal
 * `boolean` skillshot.IsFoW
 * `boolean` skillshot.IsRenderEnabled
 * `boolean` skillshot.IsVisible
 * `vec2` skillshot.StartPosition
 * `vec2` skillshot.OriginalStartPosition
 * `vec2` skillshot.DirectionVector
 * `vec2` skillshot.NormalVector
 * `vec2` skillshot.EndPosition
 * `vec2` skillshot.OriginalEndPosition
 * `vec2` skillshot.CastPosition
 * `number` skillshot.StartObjectHandle
 * `number` skillshot.EndObjectHandle
> The ObjID
 * `boolean` skillshot.IsIgnoredFromInside

Member Functions:<br>

 * skillshot:IsValid()
 * skillshot:Invalidate()
 * skillshot:IsActive()
 * skillshot:Activate()
 * skillshot:Deactivate(isForced, isFamilyCall)
 * skillshot:IsEnabledInMenu()
 * skillshot:IsFoWEnabledInMenu()
 * skillshot:GetDangerLevelFromMenu()
 * skillshot:GetDangerLevel()
 * skillshot:CalculateTicks()
 * skillshot:IsIgnored()
 * skillshot:IsIgnoredTemporarily()
 * skillshot:IgnoreTemporarily(ignore)
 * skillshot:Contains(pos/obj)
 * skillshot:ContainsPlayer()
 * skillshot:GetHitTime(pos/obj)
 * skillshot:GetHitRemainingTime(pos/obj)


###spelldata.obj (Evade3)

Properties:<br>

 * `string` spelldata.Name
 * `number` spelldata.NameHash
 * `table` spelldata.SpellNames
 * `table` spelldata.MissileNames
 * `number` spelldata.Slot
 * `number` spelldata.CastDuration
 * `number` spelldata.StayDuration
 * `number` spelldata.Speed
 * `number` spelldata.Range
 * `number` spelldata.HitArea
 * `number` spelldata.ExtraHitArea
 * `boolean` spelldata.IsDynamicHitArea
 * `boolean` spelldata.IsGlobal
 * `boolean` spelldata.IsFixedRange
 * `boolean` spelldata.IsAreaIgnoringHitBox
 * `boolean` spelldata.IsRangeIgnoringHitBox
 * `boolean` spelldata.IsCrowdControl

###cast_info_saved.obj (Evade3)

Properties:<br>

 * `string` cast_info_saved.Name
 * `number` cast_info_saved.Level
 * `boolean` cast_info_saved.HasTarget
 * `number` cast_info_saved.SenderHandle
 * `number` cast_info_saved.TargetHandle
 * `number` cast_info_saved.CastSpeed
 * `number` cast_info_saved.Slot
 * `number` cast_info_saved.MissileHash
 * `number` cast_info_saved.MissileNetworkId
 * `vec2` cast_info_saved.StartPos
 * `vec2` cast_info_saved.EndPos
 * `vec2` cast_info_saved.EndPos2
 * `number` cast_info_saved.WindUpTime
 * `number` cast_info_saved.AnimationTime
 * `number` cast_info_saved.StartTime
 * `number` cast_info_saved.CastEndTime
 * `number` cast_info_saved.EndTime
 * `number` cast_info_saved.Cooldown
 * `boolean` cast_info_saved.IsBasicAttack
 * `boolean` cast_info_saved.IsSpecialAttack
 * `boolean` cast_info_saved.IsInstantCast
 * `boolean` cast_info_saved.IsAutoAttack
 * `boolean` cast_info_saved.IsChanneling
 * `boolean` cast_info_saved.IsBasicAttackSlot
 * `boolean` cast_info_saved.IsCharging
 * `boolean` cast_info_saved.SpellWasCast
 * `boolean` cast_info_saved.IsStopped
 * `boolean` cast_info_saved.ChargeEndScheduled

