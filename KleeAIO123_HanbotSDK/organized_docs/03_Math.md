#Math
###vec2
vec2(number, number)<br>
vec2(vec2)<br>
``` lua
local a = vec2(player.x, player.z)
local b = vec2(a)
a:print()
b:print()
```
####v1:dot(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns dot product<br>
``` lua
local a = player.pos2D:dot(mousePos2D)
print(a)
```
####v1:cross(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns cross product<br>
``` lua
local a = player.pos2D:cross(mousePos2D)
print(a)
```
####v1:len()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`number` returns length of v1<br>
``` lua
local a = mousePos2D - player.pos2D
local b = a:len()
print(b)
```
####v1:lenSqr()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`number` returns squared length of v1<br>
``` lua
local a = mousePos2D - player.pos2D
local b = a:lenSqr()
print(b)
```
####v1:norm()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`vec2` returns normalized v1<br>
``` lua
local a = mousePos2D - player.pos2D
local b = a:norm()
b:print()
```
####v1:extend(to, range)
Parameters<br>
`vec2` to<br>
`number` range<br>
Return Value<br>
`vec2` returns extended vec<br>
``` lua
local a = player.pos2D:extend(mousePos2D, 100)
a:print()
```
####v1:dist(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns distance between v1 and v2<br>
``` lua
local a = mousePos2D:dist(player.pos2D)
print(a)
```
####v1:distSqr(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns squared distance between v1 and v2<br>
``` lua
local a = mousePos2D:distSqr(player.pos2D)
print(a)
```
####v1:distLine(A, B)
Parameters<br>
`vec2` v1<br>
`vec2` A<br>
`vec2` B<br>
Return Value<br>
`number` returns distance between v1 and line: A to B<br>
####v1:inRange(v2, range)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`number` range<br>
Return Value<br>
`number` returns whether v2 in area from v1 to range<br>
####v1:isOnLineSegment(a, b)
Parameters<br>
`vec2` v1<br>
`vec2` a<br>
`vec2` b<br>
`number` range<br>
Return Value<br>
`number` returns whether v1 in line segment<br>
####v1:projectOnLine(a, b)
Parameters<br>
`vec2` v1<br>
`vec2` a<br>
`vec2` b<br>
`number` range<br>
Return Value<br>
`number` returns project result in line<br>
####v1:projectOnLineSegment(a, b)
Parameters<br>
`vec2` v1<br>
`vec2` a<br>
`vec2` b<br>
`number` range<br>
Return Value<br>
`number` returns project result in line segment<br>
####v1:angle(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns angle (radians) between v1 and v2<br>
####v1:angleDeg(v2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
Return Value<br>
`number` returns angle (degrees) between v1 and v2<br>
####v1:perp1()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`vec2` returns perpendicular (left) vec2 to v1<br>
``` lua
local a = mousePos2D-player.pos2D
local b = a:norm()
local c = b:perp1()
c:print()
```
####v1:perp2()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`vec2` returns perpendicular (right) vec2 to v1<br>
``` lua
local a = mousePos2D-player.pos2D
local b = a:norm()
local c = b:perp2()
c:print()
```
####v1:lerp(v2, s)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`number` s<br>
Return Value<br>
`vec2` returns interpolated vec2 between v1 and v2 by factor s<br>
``` lua
local a = player.pos2D:lerp(mousePos2D, 0.5)
a:print()
```
####v1:clone()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`vec2` returns cloned v1<br>
``` lua
local a = player.pos2D:clone()
a:print()
```
####v1:to3D(y)
Parameters<br>
`vec2` v1<br>
`number` y<br>
Return Value<br>
`vec3` returns vec3<br>
``` lua
local a = vec2(player.x, player.z)
local b = a:to3D(mousePos.y)
b:print()
```
####v1:toGame3D()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`vec3` returns vec3, y is set to world height for exact position<br>
####v1:rotate(s)
Parameters<br>
`vec2` v1<br>
`number` s<br>
Return Value<br>
`vec2` returns vec2 rotated by s radians<br>
``` lua
local a = (mousePos2D-player.pos2D)
local b = a:norm()
local c = b:rotate(0.785398)
c:print()
```
####v1:rotateDeg(angle)
Parameters<br>
`vec2` v1<br>
`number` angle<br>
Return Value<br>
`vec2` returns vec2 rotated by s degrees<br>
####v1:countAllies(range)
Parameters<br>
`vec2` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countEnemies(range)
Parameters<br>
`vec2` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countAllyLaneMinions(range)
Parameters<br>
`vec2` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countEnemyLaneMinions(range)
Parameters<br>
`vec2` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:isUnderEnemyTurret(range)
Parameters<br>
`vec2` v1<br>
`number` range, extra range, optional<br>
Return Value<br>
`boolean`<br>
####v1:isUnderAllyTurret(range)
Parameters<br>
`vec2` v1<br>
`number` range, extra range, optional<br>
Return Value<br>
`boolean`<br>
####v1:print()
Parameters<br>
`vec2` v1<br>
Return Value<br>
`void`
``` lua
local a = vec2(mousePos.x, mousePos.z)
a:print()
```
####vec2.array(n)
Parameters<br>
`number` n<br>
Return Value<br>
`vec2[?]` returns vec2 array of length n<br>
``` lua
local a = vec2.array(12)
a[0].x = 100
a[0].y = 200
a[0]:print()
```
###vec3
vec3(number, number, number)<br>
vec3(vec3)<br>
``` lua
local a = vec3(player.x, player.y, player.z)
local b = vec3(a)
a:print()
b:print()
```
####v1:dot(v2)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`number` returns dot product<br>
``` lua
local a = player.pos:dot(mousePos)
print(a)
```
####v1:cross(v2)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`number` returns cross product<br>
``` lua
local a = player.pos:cross(mousePos)
print(a)
```
####v1:len()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`number` returns length of v1<br>
``` lua
local a = mousePos - player.pos
local b = a:len()
print(b)
```
####v1:lenSqr()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`number` returns squared length of v1<br>
``` lua
local a = mousePos - player.pos
local b = a:lenSqr()
print(b)
```
####v1:norm()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec3` returns normalized v1<br>
``` lua
local a = mousePos - player.pos
local b = a:norm()
b:print()
```
####v1:extend(to, range)
Parameters<br>
`vec3` to<br>
`number` range<br>
Return Value<br>
`vec3` returns extended vec<br>
``` lua
local a = player.pos:extend(mousePos, 100)
a:print()
```
####v1:dist(v2)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`number` returns distance between v1 and v2<br>
``` lua
local a = mousePos:dist(player.pos)
print(a)
```
####v1:distSqr(v2)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`number` returns squared distance between v1 and v2<br>
``` lua
local a = mousePos:distSqr(player.pos)
print(a)
```
####v1:inRange(v2, range)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
`number` range<br>
Return Value<br>
`number` returns whether v2 in area from v1 to range<br>
####v1:angle(v2)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
Return Value<br>
`number` returns angle (deg) between v1 and v2<br>
####v1:perp1()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec3` returns perpendicular (left) vec3 to v1<br>
``` lua
local a = mousePos-player.pos
local b = a:norm()
local c = b:perp1()
c:print()
```
####v1:perp2()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec3` returns perpendicular (right) vec3 to v1<br>
``` lua
local a = mousePos-player.pos
local b = a:norm()
local c = b:perp2()
c:print()
```
####v1:lerp(v2, s)
Parameters<br>
`vec3` v1<br>
`vec3` v2<br>
`number` s<br>
Return Value<br>
`vec3` returns interpolated vec3 between v1 and v2 by factor s<br>
``` lua
local a = player.pos:lerp(mousePos, 0.5)
a:print()
```
####v1:clone()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec3` returns cloned v1<br>
``` lua
local a = player.pos:clone()
a:print()
```
####v1:to2D()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`vec2` returns vec2 from x and z properties<br>
``` lua
local a = vec3(player.x, player.y, player.z)
local b = a:to2D()
b:print()
```
####v1:rotate(s)
Parameters<br>
`vec3` v1<br>
`number` s<br>
Return Value<br>
`vec3` returns vec3 rotated by s radians<br>
``` lua
local a = (mousePos-player.pos)
local b = a:norm()
local c = b:rotate(0.785398)
c:print()
```
####v1:countAllies(range)
Parameters<br>
`vec3` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countEnemies(range)
Parameters<br>
`vec3` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countAllyLaneMinions(range)
Parameters<br>
`vec3` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:countEnemyLaneMinions(range)
Parameters<br>
`vec3` v1<br>
`number` range<br>
Return Value<br>
`number`<br>
####v1:isUnderEnemyTurret(range)
Parameters<br>
`vec3` v1<br>
`number` range, extra range, optional<br>
Return Value<br>
`boolean`<br>
####v1:isUnderAllyTurret(range)
Parameters<br>
`vec3` v1<br>
`number` range, extra range, optional<br>
Return Value<br>
`boolean`<br>
####v1:print()
Parameters<br>
`vec3` v1<br>
Return Value<br>
`void`
``` lua
local a = vec3(mousePos.x, mousePos.y, mousePos.z)
a:print()
```
####vec3.array(n)
Parameters<br>
`number` n<br>
Return Value<br>
`vec3[?]` returns vec3 array of length n<br>
``` lua
local a = vec3.array(12)
a[0].x = 100
a[0].y = 50
a[0].z = 200
a[0]:print()
```
###vec4
vec4(number, number, number)<br>
vec4(vec4)<br>
####v1:dot(v2)
Parameters<br>
`vec4` v1<br>
`vec4` v2<br>
Return Value<br>
`number` returns dot product<br>
####v1:cross(v2)
Parameters<br>
`vec4` v1<br>
`vec4` v2<br>
Return Value<br>
`number` returns cross product<br>
####v1:len()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`number` returns length of v1<br>
####v1:lenSqr()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`number` returns squared length of v1<br>
####v1:norm()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`vec4` returns normalized v1<br>
####v1:dist(v2)
Parameters<br>
`vec4` v1<br>
`vec4` v2<br>
Return Value<br>
`number` returns distance between v1 and v2<br>
####v1:distSqr(v2)
Parameters<br>
`vec4` v1<br>
`vec4` v2<br>
Return Value<br>
`number` returns squared distance between v1 and v2<br>
####v1:perp1()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`vec4` returns perpendicular (left) vec4 to v1<br>
####v1:perp2()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`vec4` returns perpendicular (right) vec4 to v1<br>
####v1:lerp(v2, s)
Parameters<br>
`vec4` v1<br>
`vec4` v2<br>
`number` s<br>
Return Value<br>
`vec4` returns interpolated vec4 between v1 and v2 by factor s<br>
####v1:clone()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`vec4` returns cloned v1<br>
####v1:to2D()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`vec2` returns vec2 from x and z properties<br>
####v1:rotate(s)
Parameters<br>
`vec4` v1<br>
`number` s<br>
Return Value<br>
`vec4` returns vec4 rotated by s radians<br>
####v1:print()
Parameters<br>
`vec4` v1<br>
Return Value<br>
`void`
####vec4.array(n)
Parameters<br>
`number` n<br>
Return Value<br>
`vec4[?]` returns vec4 array of length n<br>

###seg2
`vec2` seg2.startPos<br>
`vec2` seg2.endPos
####v1:len()
Parameters<br>
`seg2` v1<br>
Return Value<br>
`number` returns length of v1<br>
####v1:lenSqr()
Parameters<br>
`seg2` v1<br>
Return Value<br>
`number` returns squared length of v1<br>

###mathf
A library of commonly used 2D math functions.<br>
####mathf.PI
Return Value<br>
`number` returns pi<br>
``` lua
print(mathf.PI)
```
####mathf.cos(n)
Parameters<br>
`number` n<br>
Return Value<br>
`number` returns the cosine of n<br>
``` lua
local a = mathf.cos(mathf.PI)
print(a)
```
####mathf.sin(n)
Parameters<br>
`number` n<br>
Return Value<br>
`number` returns the sine of n<br>
``` lua
local a = mathf.sin(mathf.PI)
print(a)
```
####mathf.round(n, d)
Parameters<br>
`number` n<br>
`number` d<br>
Return Value<br>
`number` returns rounded n to precision d<br>
``` lua
local a = mathf.round(1.234567, 3)
print(a)
```
####mathf.sqr(n)
Parameters<br>
`number` n<br>
Return Value<br>
`number` returns squared value of n<br>
``` lua
local a = mathf.sqr(2)
print(a)
```
####mathf.clamp(min, max, n)
Parameters<br>
`number` min<br>
`number` max<br>
`number` n<br>
Return Value<br>
`number` returns clamped n between min and max<br>
``` lua
local a = mathf.clamp(0, 25, -1)
print(a)
```
####mathf.sect_line_line(v1, v3, v3, v4)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
`vec2` v4<br>
Return Value<br>
`vec2` returns intersection point of lines (v1, v2) and (v3, v4)<br>
``` lua
local v1 = vec2(0, 0)
local v2 = vec2(100,100)
local v3 = vec2(100, 0)
local v4 = vec2(0,100)
local a = mathf.sect_line_line(v1, v2, v3, v4)
a:print()
```
####mathf.dist_line_vector(v1, v2, v3)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
Return Value<br>
`number` returns distance between v1 and line (v2, v3)<br>
``` lua
local v1 = vec2(0, 0)
local v2 = vec2(100, 0)
local v3 = vec2(0,100)
local a = mathf.dist_line_vector(v1, v2, v3)
print(a)
```
####mathf.angle_between(v1, v2, v3)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
Return Value<br>
`number` returns the angle between v2 and v3 from origin v1 in radians<br>
``` lua
local v1 = vec2(0, 0)
local a = mathf.angle_between(v1, player.pos2D, mousePos2D)
print(a)
```
####mathf.mec(pts, n)
Parameters<br>
`vec2[]` pts<br>
`number` n<br>
Return Value<br>
`vec2` returns the center of the minimum enclosing circle<br>
`number` returns the radius of the minimum enclosing circle<br>
``` lua
local pts = vec2.array(2)
pts[0].x, pts[0].y = 0, 0
pts[1].x, pts[1].y = mousePos.x, mousePos.z
pts[2].x, pts[2].y = player.x, player.z
local c, n = mathf.mec(pts, 2)
print(c.x, c.y, n)
```
####mathf.project(v1, v2, v3, s1, s2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
`number` s1<br>
`number` s2<br>
Return Value<br>
`vec2` returns the collision point<br>
`number` returns the time until collision occurs<br>
``` lua
--calculates collision position and time of a projectile from mousePos along the players path
local src = mousePos2D
local pos_s = player.path.serverPos2D
local pos_e = player.path.point2D[player.path.index]
local s1 = 2000
local s2 = player.moveSpeed

local res, res_t = mathf.project(src, pos_s, pos_e, s1, s2)
if res then
	print(res.x, res.y, res_t)
end
```
####mathf.dist_seg_seg(v1, v2, v3, v4)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
`vec2` v4<br>
Return Value<br>
`number` returns the distance between line segments (v1, v2) and (v3, v4)<br>
``` lua
local v1 = vec2(0,0)
local v2 = vec2(1000,1000)
local v3 = mousePos2D
local v4 = player.pos2D
local res = mathf.dist_seg_seg(v1, v2, v3, v4)
print(res)
```
####mathf.closest_vec_line(v1, v2, v3)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
Return Value<br>
`vec2` returns a vec2 along the line (v2, v3) closest to v1<br>
``` lua
local v1 = player.pos2D
local v2 = vec2(0,0)
local v3 = mousePos2D
local res = mathf.closest_vec_line(v1, v2, v3)
res:print()
```
####mathf.closest_vec_line_seg(v1, v2, v3)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
Return Value<br>
`vec2` returns a vec2 along the line segment (v2, v3) closest to v1<br>
``` lua
local v1 = player.pos2D
local v2 = vec2(0,0)
local v3 = mousePos2D
local res = mathf.closest_vec_line_seg(v1, v2, v3)
if res then
	res:print()
end
```
####mathf.col_vec_rect(v1, v2, v3, w1, w2)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
`number` w1<br>
`number` w2<br>
Return Value<br>
`boolean` returns true if v1 with bounding radius of w1 collides with line (v2, v3) of width w2<br>
``` lua
local v1 = player.pos2D
local v2 = vec2(0, 0)
local v3 = mousePos2D
local w1 = player.boundingRadius
local w2 = 100
local res = mathf.col_vec_rect(v1, v2, v3, w1, w2)
print(res)
```
####mathf.sect_circle_circle(v1, r1, v2, r2)
Parameters<br>
`vec2` v1<br>
`number` r1<br>
`vec2` v2<br>
`number` r2<br>
Return Value<br>
`vec2` returns first intersection of circles at v1 with radius of r1 and v2 with radius of r2<br>
`vec2` returns second intersection of circles at v1 with radius of r1 and v2 with radius of r2<br>
``` lua
local v1 = mousePos2D
local r1 = 500
local v2 = player.pos2D
local r2 = player.attackRange
local res1, res2 = mathf.sect_circle_circle(v1, r1, v2, r2)
if res1 then
	res1:print()
	res2:print()
end
```
####mathf.sect_line_circle(v1, v2, v3, r)
Parameters<br>
`vec2` v1<br>
`vec2` v2<br>
`vec2` v3<br>
`number` r<br>
Return Value<br>
`vec2` returns first intersection of line (v1, v2) and circle v3 with radius of r<br>
`vec2` returns second intersection of line (v1, v2) and circle v3 with radius of r<br>
``` lua
local v1 = vec2(0, 0)
local v2 = mousePos2D
local v3 = player.pos2D
local r = player.attackRange
local res1, res2 = mathf.sect_line_circle(v1, v2, v3, r)
if res1 then
	res1:print()
end
if res2 then
	res2:print()
end
```
####mathf.mat2()
Return Value<br>
`double[2][2]` returns a 2x2 transformation matrix<br>
####mathf.mat3()
Return Value<br>
`double[3][3]` returns a 3x3 transformation matrix<br>
####mathf.mat4()
Return Value<br>
`double[4][4]` returns a 4x4 transformation matrix<br>

###clipper
Unlike the other math libraries, clipper must first be loaded.<br>
Further documentation can be found [here](http://www.angusj.com/delphi/clipper/documentation/Docs/_Body.htm).
``` lua
local clip = module.internal('clipper')
local polygon = clip.polygon
local polygons = clip.polygons
local clipper = clip.clipper
local clipper_enum = clip.enum
```
Enums:

 * clipper_enum.PolyFillType.EvenOdd
 * clipper_enum.PolyFillType.NonZero
 * clipper_enum.PolyFillType.Positive
 * clipper_enum.PolyFillType.Negative
 * clipper_enum.JoinType.Square
 * clipper_enum.JoinType.Round
 * clipper_enum.JoinType.Miter
 * clipper_enum.ClipType.Intersection
 * clipper_enum.ClipType.Union
 * clipper_enum.ClipType.Difference
 * clipper_enum.ClipType.Xor
 * clipper_enum.PolyType.Subject
 * clipper_enum.PolyType.Clip

####polygon:Add(v1)
Parameters<br>
`vec2` v1<br>
Return Value<br>
`void`<br>
``` lua
local p = polygon()
local v = vec2(200, 200)
p:Add(v)
```
####polygon:ChildCount()
Return Value<br>
`number` returns number of vertices<br>
``` lua
local p = polygon(vec2(200, 200), vec2(200, 100), vec2(100, 200))

print(p:ChildCount())
```
####polygon:Childs(i)
Parameters<br>
`number` i<br>
Return Value<br>
`vec2` returns vec2 at vertex i<br>
``` lua
local p = polygon(vec2(200, 200), vec2(200, 100), vec2(100, 200))

local v = p:Childs(1)
v:print()
```
####polygon:Area()
Return Value<br>
`number` returns the area of polygon<br>
``` lua
local p = polygon(vec2(200, 200), vec2(200, 100), vec2(100, 200))

print(p:Area())
```
####polygon:Clean(dist)
Parameters<br>
`number` dist<br>
Return Value<br>
`void`<br>
``` lua
local p = polygon(vec2(200, 200), vec2(200, 100), vec2(200, 101), vec2(100, 200))

print(p:ChildCount())
p:Clean(5)
print(p:ChildCount())
```
####polygon:Simplify(PolyFillType)
Parameters<br>
`number` PolyFillType<br>
Return Value<br>
`polygons` returns polygon set<br>
``` lua
local p1 = polygon(vec2(5,62), vec2(164,62), vec2(36,157), vec2(85, 4), vec2(134, 158))
local p = p1:Simplify(clipper_enum.PolyFillType.NonZero)
local p2 = p:Childs(0)

cb.add(cb.draw, function()
	p2:Draw2D(5, 0xFF00FFFF)
	p1:Draw2D(2, 0xFFFF00FF)
end)
```
####polygon:Orientation()
Return Value<br>
`number` returns 1 if polygon has clockwise orientation<br>
####polygon:Reverse()
Return Value<br>
`void` reverses polygons orientation<br>
####polygon:Contains(v1)
Parameters<br>
`vec2\vec3` v1<br>
Return Value<br>
`number` returns 1 if v1 is inside of polygon, 0 if outside, -1 if v1 is on polygon edge<br>
``` lua
local p1 = polygon(vec2(200,200), vec2(200,300), vec2(300,300), vec2(300, 200))
cb.add(cb.draw, function()
	p1:Draw2D(2, p1:Contains(game.cursorPos)==1 and 0xFF00FF00 or 0xFFFF0000)
end)
```
####polygon:Draw2D(width, color)
Parameters<br>
`number` width<br>
`number` color<br>
Return Value<br>
`void`<br>
####polygon:Draw3D(y, width, color)
Parameters<br>
`number` y<br>
`number` width<br>
`number` color<br>
Return Value<br>
`void`<br>
####polygon:OnScreen2D()
Return Value<br>
`boolean` returns true if polygon intersects the screen<br>
####polygon:OnScreen3D(y)
Parameters<br>
`number` y<br>
Return Value<br>
`boolean` returns true if polygon intersects the screen<br>
####polygons:Add(polygon)
Parameters<br>
`polygon` polygon<br>
Return Value<br>
`void`<br>
####polygons:ChildCount()
Return Value<br>
`number` returns number of polygons contained polygon set<br>
####polygons:Childs(i)
Parameters<br>
`number` i<br>
Return Value<br>
`polygon` returns polygon at index i<br>
####polygons:Reverse()
Return Value<br>
`void` reverses the orientation of all containing polygons<br>
####polygons:Clean(dist)
Parameters<br>
`number` dist<br>
Return Value<br>
`void` cleans all contained polygons<br>
####polygons:Simplify(PolyFillType)
Parameters<br>
`number` PolyFillType<br>
Return Value<br>
`polygons` returns polygon set<br>
####polygons:Offset(delta, JoinType, limit)
Parameters<br>
`number` delta<br>
`number` JoinType<br>
`number` limit<br>
Return Value<br>
`polygons` returns polygon set<br>
####clipper:AddPath(polygon, PolyType, closed)
Parameters<br>
`polygon` polygon<br>
`number` PolyType<br>
`boolean` closed<br>
Return Value<br>
`void`<br>
####clipper:AddPaths(polygons, PolyType, closed)
Parameters<br>
`polygons` polygons<br>
`number` PolyType<br>
`boolean` closed<br>
Return Value<br>
`void`<br>
####clipper:Clear()
Return Value<br>
`void`<br>
####clipper:Execute(ClipType, PolyFillType, PolyFillType)
Parameters<br>
`number` ClipType<br>
`number` PolyFillType<br>
`number` PolyFillType<br>
Return Value<br>
`polygons` returns polygon set<br>

```lua
-- Example to calc DariusQ Outer Ring

local clip = module.internal('clipper')
local polygon = clip.polygon
local polygons = clip.polygons
local clipper = clip.clipper
local clipper_enum = clip.enum

local function create_ring(center, outer_radius, inner_radius)
    local outer_ring = polygon()
    local inner_ring = polygon()
    for i = 1, 64 do
        local angle = (i - 1) * (2 * math.pi / 64)
        local x_outer = center.pos.x + outer_radius * math.cos(angle)
        local y_outer = center.pos.z + outer_radius * math.sin(angle)
        local x_inner = center.pos.x + inner_radius * math.cos(angle)
        local y_inner = center.pos.z + inner_radius * math.sin(angle)
        outer_ring:Add(vec2(x_outer, y_outer))
        inner_ring:Add(vec2(x_inner, y_inner))
    end

    local clpr = clipper()
    clpr:AddPath(outer_ring, clipper_enum.PolyType.Subject, true)
    clpr:AddPath(inner_ring, clipper_enum.PolyType.Clip, true)
    local ring_area = clpr:Execute(clipper_enum.ClipType.Difference, clipper_enum.PolyFillType.NonZero, clipper_enum.PolyFillType.EvenOdd)
    return ring_area
end

-- Darius Outer ring Q, Find hit areas
local function on_draw()
    local centers = {}
    for i=0, objManager.enemies_n-1 do
        local obj = objManager.enemies[i]
        if obj and obj:isValidTarget(850) then
            table.insert(centers, obj)
        end
    end

    if #centers >= 2 then
        local clpr = clipper()
        local first_ring = create_ring(centers[1], 460, 250)
        local second_ring = create_ring(centers[2], 460, 250)

        clpr:AddPaths(first_ring, clipper_enum.PolyType.Subject, true)
        clpr:AddPaths(second_ring, clipper_enum.PolyType.Clip, true)

        local solution = clpr:Execute(clipper_enum.ClipType.Intersection, clipper_enum.PolyFillType.NonZero, clipper_enum.PolyFillType.EvenOdd)

        for i = 0, solution:ChildCount() - 1 do
            local poly = solution:Childs(i)
            poly:Draw3D(player.y, 2, 0xFF00FF00)
        end
    end
end

cb.add(cb.draw, on_draw)
```

###clipper2
Clipper2 is a high-performance polygon clipping and offsetting library that works with double precision coordinates.<br>
Further documentation can be found [https://www.angusj.com/clipper2/Docs/Overview.htm](https://www.angusj.com/clipper2/Docs/Overview.htm).

``` lua
local clipper2 = require("clipper2")
local PointD = clipper2.PointD
local PathD = clipper2.PathD
local PathsD = clipper2.PathsD
local BooleanOpD = clipper2.BooleanOpD
local Enum = clipper2.Enum
```

**Enums:**

**ClipType:**

- Enum.ClipType.None
- Enum.ClipType.Intersection
- Enum.ClipType.Union
- Enum.ClipType.Difference
- Enum.ClipType.Xor

**FillRule:**

- Enum.FillRule.EvenOdd
- Enum.FillRule.NonZero
- Enum.FillRule.Positive
- Enum.FillRule.Negative

**JoinType:**

- Enum.JoinType.Square
- Enum.JoinType.Bevel
- Enum.JoinType.Round
- Enum.JoinType.Miter

**EndType:**

- Enum.EndType.Polygon
- Enum.EndType.Joined
- Enum.EndType.Butt
- Enum.EndType.Square
- Enum.EndType.Round

####PointD(x, y)
Create a new double precision point.<br>
Parameters<br>
`number` x coordinate<br>
`number` y coordinate<br>
Return Value<br>
`PointD` returns a new point object<br>
``` lua
local point = PointD(100.5, 200.7)
```

####PathD()
Create a new double precision path (polygon).<br>
Parameters<br>
`...` optional points to initialize the path<br>
Return Value<br>
`PathD` returns a new path object<br>
``` lua
-- Create empty path
local path = PathD()

-- Create path with initial points
local p1 = PointD(0, 0)
local p2 = PointD(100, 0) 
local p3 = PointD(50, 100)
local path = PathD(p1, p2, p3)
```

####PathD:Add(x, y)
Add a point to the path.<br>
Parameters<br>
`number` x coordinate<br>
`number` y coordinate<br>
Return Value<br>
`void`<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(50, 100)
```

####PathD:ChildCount()
Get the number of points in the path.<br>
Return Value<br>
`number` returns number of points<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
print(path:ChildCount()) -- prints 2
```

####PathD:Childs(index)
Get a point at the specified index.<br>
Parameters<br>
`number` index (0-based)<br>
Return Value<br>
`PointD` returns point at index<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
local point = path:Childs(0)
print(point.x, point.y) -- prints 0, 0
```

####PathD:Clear()
Remove all points from the path.<br>
Return Value<br>
`void`<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Clear()
print(path:ChildCount()) -- prints 0
```

####PathD:Area()
Calculate the area of the polygon.<br>
Return Value<br>
`number` returns area (positive for clockwise, negative for counter-clockwise)<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(100, 100)
path:Add(0, 100)
print(path:Area()) -- prints 10000
```

####PathD:Orientation()
Get the orientation of the polygon.<br>
Return Value<br>
`boolean` returns true if clockwise, false if counter-clockwise<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(100, 100)
path:Add(0, 100)
print(path:Orientation()) -- prints true (clockwise)
```

####PathD:Reverse()
Reverse the order of points in the path.<br>
Return Value<br>
`void`<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(100, 100)
path:Reverse()
```

####PathD:Simplify(epsilon, isClosedPath)
Simplify the path by removing unnecessary points.<br>
Parameters<br>
`number` epsilon - simplification tolerance<br>
`boolean` isClosedPath - whether the path is closed (default: true)<br>
Return Value<br>
`PathD` returns simplified path<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(50, 1)
path:Add(100, 0)
local simplified = path:Simplify(2.0, false)
```

####PathD:Contains(point)
Check if a point is inside the polygon.<br>
Parameters<br>
`PointD` point to test<br>
Return Value<br>
`number` returns 1 if inside, 0 if outside<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(100, 100)
path:Add(0, 100)

local point = PointD(50, 50)
print(path:Contains(point)) -- prints 1 (inside)
```

####PathD:OnScreen2D()
Check if the path is visible on screen in 2D.<br>
Return Value<br>
`boolean` returns true if on screen<br>

####PathD:OnScreen3D(y)
Check if the path is visible on screen in 3D.<br>
Parameters<br>
`number` y coordinate (default: 0)<br>
Return Value<br>
`boolean` returns true if on screen<br>

####PathD:Draw2D(width, color)
Draw the path in 2D.<br>
Parameters<br>
`number` width - line width (default: 0)<br>
`number` color - color in ARGB format (default: 0xffffffff)<br>
Return Value<br>
`void`<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(50, 100)
path:Draw2D(2, 0xFF00FF00) -- green lines, 2 pixels wide
```

####PathD:Draw3D(y, width, color)
Draw the path in 3D.<br>
Parameters<br>
`number` y coordinate<br>
`number` width - line width (default: 0)<br>
`number` color - color in ARGB format (default: 0xffffffff)<br>
Return Value<br>
`void`<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(50, 100)
path:Draw3D(player.y, 2, 0xFF00FF00)
```

####PathD:Intersection(p0, p1) or PathD:Intersection(x0, y0, x1, y1)
Test if the path intersects with a line segment.<br>
Parameters<br>
`PointD` p0, p1 - line segment endpoints<br>
or<br>
`number` x0, y0, x1, y1 - line segment coordinates<br>
Return Value<br>
`boolean` returns true if intersection exists<br>
``` lua
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(50, 100)

local p0 = PointD(25, -10)
local p1 = PointD(25, 110)
print(path:Intersection(p0, p1)) -- prints true
```

####PathD:IntersectionPoint(p0, p1) or PathD:IntersectionPoint(x0, y0, x1, y1)
Get intersection points between the path and a line segment.<br>
Parameters<br>
`PointD` p0, p1 - line segment endpoints<br>
or<br>
`number` x0, y0, x1, y1 - line segment coordinates<br>
Return Value<br>
`PathD` returns path containing intersection points<br>

####PathsD()
Create a new collection of paths.<br>
Parameters<br>
`...` optional PathD objects to initialize the collection<br>
Return Value<br>
`PathsD` returns a new paths collection<br>
``` lua
-- Create empty collection
local paths = PathsD()

-- Create with initial paths
local path1 = PathD()
local path2 = PathD()
local paths = PathsD(path1, path2)
```

####PathsD:Add(path)
Add a path to the collection.<br>
Parameters<br>
`PathD` path to add<br>
Return Value<br>
`void`<br>
``` lua
local paths = PathsD()
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(50, 100)
paths:Add(path)
```

####PathsD:ChildCount()
Get the number of paths in the collection.<br>
Return Value<br>
`number` returns number of paths<br>

####PathsD:Childs(index)
Get a path at the specified index.<br>
Parameters<br>
`number` index (0-based)<br>
Return Value<br>
`PathD` returns path at index<br>

####PathsD:Clear()
Remove all paths from the collection.<br>
Return Value<br>
`void`<br>

####PathsD:Simplify(epsilon, isClosedPath)
Simplify all paths in the collection.<br>
Parameters<br>
`number` epsilon - simplification tolerance<br>
`boolean` isClosedPath - whether paths are closed (default: true)<br>
Return Value<br>
`PathsD` returns simplified paths collection<br>

####PathsD:Reverse()
Reverse the order of points in all paths.<br>
Return Value<br>
`void`<br>

####PathsD:Offset(delta, joinType, endType)
Create offset paths from the collection.<br>
Parameters<br>
`number` delta - offset distance (positive for expansion, negative for shrinking)<br>
`number` joinType - join type from Enum.JoinType<br>
`number` endType - end type from Enum.EndType (default: 0)<br>
Return Value<br>
`PathsD` returns offset paths<br>
``` lua
local paths = PathsD()
local path = PathD()
path:Add(0, 0)
path:Add(100, 0)
path:Add(100, 100)
path:Add(0, 100)
paths:Add(path)

local offset_paths = paths:Offset(10, Enum.JoinType.Round, Enum.EndType.Polygon)
```

####PathsD:Draw2D(width, color)
Draw all paths in the collection in 2D.<br>
Parameters<br>
`number` width - line width (default: 0)<br>
`number` color - color in ARGB format (default: 0xffffffff)<br>
Return Value<br>
`void`<br>

####PathsD:Draw3D(y, width, color)
Draw all paths in the collection in 3D.<br>
Parameters<br>
`number` y coordinate<br>
`number` width - line width (default: 0)<br>
`number` color - color in ARGB format (default: 0xffffffff)<br>
Return Value<br>
`void`<br>

####BooleanOpD(clipType, fillRule, subjects, clips, solution, precision, reverse_solution)
Perform boolean operations on path collections.<br>
Parameters<br>
`number` clipType - operation type from Enum.ClipType<br>
`number` fillRule - fill rule from Enum.FillRule<br>
`PathsD` subjects - subject paths<br>
`PathsD` clips - clip paths<br>
`PathsD` solution - result paths (output)<br>
`number` precision - calculation precision<br>
`boolean` reverse_solution - whether to reverse result orientation<br>
Return Value<br>
`number` returns operation result code<br>
``` lua
local subjects = PathsD()
local clips = PathsD()
local solution = PathsD()

-- Create subject rectangle
local subject = PathD()
subject:Add(0, 0)
subject:Add(100, 0)
subject:Add(100, 100)
subject:Add(0, 100)
subjects:Add(subject)

-- Create clip circle (approximated)
local clip = PathD()
for i = 0, 31 do
    local angle = i * 2 * math.pi / 32
    local x = 50 + 30 * math.cos(angle)
    local y = 50 + 30 * math.sin(angle)
    clip:Add(x, y)
end
clips:Add(clip)

-- Perform intersection
local result = BooleanOpD(
    Enum.ClipType.Intersection,
    Enum.FillRule.NonZero,
    subjects,
    clips,
    solution,
    2,
    false
)

-- Draw result
cb.add(cb.draw, function()
    for i = 0, solution:ChildCount() - 1 do
        local path = solution:Childs(i)
        path:Draw2D(2, 0xFF00FF00)
    end
end)
```

####Eigen_PolynomialSolver(a, b, c, d, e)
Solve polynomial equations using Eigen library.
Parameters<br>
`number` a, b, c, d, e - polynomial coefficients<br>
Return Value<br>
`PathD` returns path containing solutions<br>

####Eigen_PolynomialSolver_realRoots(a, b, c, d, e)
Solve polynomial equations and return only real roots.
Parameters<br>
`number` a, b, c, d, e - polynomial coefficients<br>
Return Value<br>
`PathD` returns path containing real solutions<br>

**Example: Complex Boolean Operations**
``` lua
local clipper2 = require("clipper2")

-- Create multiple overlapping circles
local function create_circle(center_x, center_y, radius, segments)
    local path = clipper2.PathD()
    for i = 0, segments - 1 do
        local angle = i * 2 * math.pi / segments
        local x = center_x + radius * math.cos(angle)
        local y = center_y + radius * math.sin(angle)
        path:Add(x, y)
    end
    return path
end

local function on_draw()
    local subjects = clipper2.PathsD()
    local clips = clipper2.PathsD()
    local solution = clipper2.PathsD()
    
    -- Create overlapping circles
    local circle1 = create_circle(100, 100, 50, 32)
    local circle2 = create_circle(150, 100, 50, 32)
    local circle3 = create_circle(125, 150, 50, 32)
    
    subjects:Add(circle1)
    clips:Add(circle2)
    clips:Add(circle3)
    
    -- Perform union operation
    local result = clipper2.BooleanOpD(
        clipper2.Enum.ClipType.Union,
        clipper2.Enum.FillRule.NonZero,
        subjects,
        clips,
        solution,
        2,
        false
    )
    
    if result == 1 then
        -- Draw the unified shape
        for i = 0, solution:ChildCount() - 1 do
            local path = solution:Childs(i)
            path:Draw2D(3, 0xFF00FFFF)
        end
        
        -- Create offset version
        local offset_solution = solution:Offset(10, clipper2.Enum.JoinType.Round)
        for i = 0, offset_solution:ChildCount() - 1 do
            local path = offset_solution:Childs(i)
            path:Draw2D(1, 0xFFFF0000)
        end
    end
end

cb.add(cb.draw, on_draw)
```




