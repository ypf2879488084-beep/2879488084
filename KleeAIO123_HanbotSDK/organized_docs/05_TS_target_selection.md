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
