---
layout: single
title:  "Guidance Algorithm: Left or Right Side of the Line"
date:  2020-12-01
tags: algorithms
excerpt: For a line on an ellipsoid and a point not on the line, on which side of the line does the point exist?
---

I was working on a very interesting (and frustrating) algorithm recently at work that really messed with my head. After I had it solved and behind me, I decided to put it into prose and post it here -- just in case my future self needs a reminder of how it works. Hope you find it useful too!

**Problem Statement**

Given an arbitrary line on the surface of an ellipsoid with known start and end points (implying directionality); and given an arbitrary point that is not on the line (known within some reasonably small tolerance that is << the line length); determine which side (e.g. LEFT or RIGHT) of the line the point lies on.

Quick drawing:

![](/assets/2020/12/2020-12-1-ecef-depiction.png)

**Background**

This exact problem occurs routinely in automated path-following guidance algorithms that build their paths on the earth surface. The vehicle will rarely be exactly "on the path", so the obvious question to answer before determining a control response is: on which side of path is the vehicle?

**Solution**

In a flat-earth Euclidean world, this problem is easily solved using [cross-vectors](https://en.wikipedia.org/wiki/Cross_product). To me, the challenge occurred (mentally) once I defined the line as being a geodesic on an ellipsoid.

Turns out it's not that hard. You still use a cross-product. Vector-calc win, peeps!

Here we go. (Use the diagram above as reference.)

Solve for the course, $course_\text{at start point}$ of the line at the start point, $P_\text{start}$. Let this be defined in the [NED Frame](https://en.wikipedia.org/wiki/Local_tangent_plane_coordinates#Local_north,_east,_down_(NED)_coordinates).

Solve for a point $P_\text{perpendicular}$ that lies on the line and that represents a perpendicular projection from point $P_\text{off-line}$ to the line.

Let there be a vector $\vec{C}$ that is in the [ECEF Frame](https://en.wikipedia.org/wiki/ECEF) and points to the point $P_\text{off-line}$.

Let there be a vector $\vec{D}$ that is in the ECEF Frame and points to the point $P_\text{perpendicular}$.

Take the cross-product of the two vectors to determine a new vector $V$ that is orthogonal to $P_\text{perpendicular}$ and $P_\text{off-line}$.

$$\vec{V} = \vec{C} \times \vec{D}$$

The components of $\vec{V}$ contain the information for our solution. We can examine the signs of the terms in $\vec{V}$ and determine on which side of our line $P_\text{off-line}$ exists.

If we constrain our solution space to being for lines on the continent of North America, the algorithm looks like this:

    if $course_\text{at start point}$ is approximately 90 degrees:
        $V_x is negative, ON_LEFT_SIDE$
        $V_x is positive, ON_RIGHT_SIDE$

    if $course_\text{at start point}$ is approximately 270 degrees:
        $V_x is negative, ON_RIGHT_SIDE$
        $V_x is positive, ON_LEFT_SIDE$

    if $course_\text{at start point}$ is positive:
        $V_z is negative, ON_LEFT_SIDE$
        $V_z is positive, ON_RIGHT_SIDE$

    if $course_\text{at start point}$ is negative:
        $V_z is negative, ON_RIGHT_SIDE$
        $V_z is positive, ON_LEFT_SIDE$

Of course, I constrained my solution to a particular region of the globe. But, if you're thinking about the geometry here, you'll find a way to expand this into a more general solution.

Do you have a better way to solve this? [Let me know by opening a GitHub issue!](https://github.com/buffetboy2001/buffetboy2001.github.io/issues)

When I get the chance, I'll post an implementation of this in a Jupyter Notebook. :thumbsup:
