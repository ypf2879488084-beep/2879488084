#Lua
###Libraries
* [math](https://www.lua.org/manual/5.1/manual.html#5.6)
* [string](https://www.lua.org/manual/5.1/manual.html#5.4)
* [table](https://www.lua.org/manual/5.1/manual.html#5.5)
* [os](https://www.lua.org/manual/5.1/manual.html#5.8)
* [bit](http://bitop.luajit.org/api.html)

The os library has been restricted to the following functions: clock, time, date

###Functions
* [assert](https://www.lua.org/manual/5.1/manual.html#pdf-assert)
* [print](https://www.lua.org/manual/5.1/manual.html#pdf-print)
* [tostring](https://www.lua.org/manual/5.1/manual.html#pdf-tostring)
* [tonumber](https://www.lua.org/manual/5.1/manual.html#pdf-tonumber)
* [pairs](https://www.lua.org/manual/5.1/manual.html#pdf-pairs)
* [ipairs](https://www.lua.org/manual/5.1/manual.html#pdf-ipairs)
* [unpack](https://www.lua.org/manual/5.1/manual.html#pdf-unpack)
* [type](https://www.lua.org/manual/5.1/manual.html#pdf-type)
* [setmetatable](https://www.lua.org/manual/5.1/manual.html#pdf-setmetatable)
* [loadfile](https://www.lua.org/manual/5.1/manual.html#pdf-loadfile)
* [loadstring](https://www.lua.org/manual/5.1/manual.html#pdf-loadstring)
* delayaction(fn, delay, params)

```lua
delayaction(
	function(a1, a2, a3)
		print(a1, a2, a3)
	end, 
	0.5, 
	{ 1, 2, 3 }
)
```

