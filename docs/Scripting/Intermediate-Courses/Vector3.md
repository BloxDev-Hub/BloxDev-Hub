---
title: Vector3
template: docs.html
comments: true
hide:
  - navigation
---
# Introduction To Vector
Before learning `Vector3` you need to know what is a "Vector". Vector is a physical quantity that has a magnitude and a direction. A vector is graphically represented by an arrow drawn parallel to the direction of the vector, The length of the arrow represents the magnitude of the vector.

## 2D Vector
In 2 dimensions, where you have two coordinates/axis `X-Axis` and `Y-Axis`. They are perpendicular to each other.

<img src=https://github.com/Rodevs-Helpers/Helpers-Documents/blob/editing/images/2d.png?raw=true width="500" height="500"/>

A vector is drawn from the origin `(0,0)` to the `(10,10)` coordinate point of the plane. These coordinate points represent the magnitude of the vector on the X and Y axis and are written as `(X, Y)`. 

![2dVector](https://imgur.com/A8nM0in.png)

## 3D Vector
In three-dimensional space, There are three axes `X-Axis`, `Y-Axis`, and `Z-Axis`. A 3D vector is the same as 2D but with an extra dimension. The rest of our topic will be based on a three-dimensional vector.

![3dvector](https://imgur.com/rvo4Pbz.png)

Similar to a 2D vector, coordinates of a vector in 3 dimensions are written as `(10,10,10)`. These coordinate points represent the magnitude of the vector on the X, Y, and Z axis and are written as `(X, Y, Z)`.
??? correct "Confused about how we calculated the magnitude?"

	![magnitude](https://imgur.com/keRiBq7.png)
	
    The length of the vector on each axis is represented by three lines. Each of them is parallel to one of the lines of the axis. The line parallel to the x-axis represents its magnitude on the x-axis, the same for the y and z-axis.

## Vector in Roblox
In Roblox, a **Vector3** is a vector in the three-dimensional space. It is created by `Vector3.new(x,y,z)`. Roblox engine uses `Vector3` in multiple cases, such as positioning base parts, size of base parts, setting directions of linear velocities, etc. In every case the origin of the vector is different. We will talk about them later. For now, we will go through some common properties of Vector3.

## Magnitude of a Vector.
For your easiness, Roblox allows you to get the magnitude of a vector by just `Vector3.Magnitude`. As mentioned earlier, magnitude is the length of the vector. If `v` is a vector and its coordinates are (10,13,10) then its magnitude is given by

```
|V| = √(x^2 + y^2 + z^2)
|V| = √(10^2 + 13^2 + 10^2)
|V| =  √(100 + 169 + 100)
|V| = √(369)
|V| = 19.209
```

Now, in the studio, add the following code in a script and run.

=== "Code"
	```lua
	local vector = Vector3.new(10,13,10)
	print(vector.Magnitude)
	```
=== "Output"
	```
	 19.209
	```

It is the length of a vector given in studs.

## Unit Vector
A **unit vector** is a vector with a magnitude `1`. It can be obtained by dividing a vector by its magnitude.  If **u** is a vector of magnitude (10,13,10) then its unit vector **û** can be obtained by

```
û = u / |u|
```

We will first calculate the magnitude and divide it by every component of the vector.

```
|u| = √(x^2 + y^2 + z^2)
|u| = √(10^2 + 13^2 + 10^2)
|u| = √(100 + 169 + 100)
|u| = √(369)
|u| = 19.209
```

Let x2, y2, and z2 be the x,y, and z components of  **û**.
Dividing x,y, and z components of **u** by |u|

```
x2 = x / |u| = 10 / 19.209 = 0.5205
y2 = y / |u| = 13 / 19.209 = 0.6767
z2 = z / |u| = 10 / 19.209 = 0.5205
```

We have obtained by x,y, and z components of the unit vector (**û**).  Now the coordinates of **û** is (0.5205,0.6767,0.5205). If it is a unit vector then its magnitude must be 1. Let's prove that

```
|û| = √(x^2 + y^2 + z^2)
|û| = √(0.5205^2 + 0.6767^2 + 0.5205^2)
|û| = √(0.2709 + 0.4579 + 0.2709)
|û| = √(1) -- nearly 1
|û| = 1
```

In the studio, you can easily get the unit vector of a vector by `Vector3.Unit`.

=== "Code" 
	```
	local vector = Vector3.new(10,13,10)
	print(vector.Unit)
	```
=== "Output"
	```
	0.5205791592597961, 0.6767529249191284, 0.5205791592597961
	```
    
If you look carefully, you can see it is the same as we calculated. Unit vectors are mainly used for specifying directions. The Direction of a vector and its unit vector always remain the same. 

??? question "Did you just waste my time when you could get it that easily?"
	No, I could explain you more easily by just saying use `.Unit` and `.Magnitude` but it will never clear your concepts of magnitude and unit. The purpose of deriving was to explain what exactly it is.

## Normal Vector
A vector perpendicular to a surface is called a normal vector.

![waveplane](https://imgur.com/FOXKF5K.png)

![sphereplane](https://imgur.com/8RM3WSJ.png)

In Roblox, you can find a normal vector in [RaycastResult.Normal](https://developer.roblox.com/en-us/api-reference/datatype/RaycastResult). This vector is normal to the intersected face. There are many other use cases that you will find when computing vector maths

### Closing!
I hope it helped in developing a better understanding of vectors and Vector3. Feel free to report this article if there is any mistake. There is a few stuff left regarding vectors and we will discuss them later. For now, bai!