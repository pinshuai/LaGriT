---
title: BUBBLE 
tags: ok
---

# BUBBLE

This command takes a topologically 2d mesh (a planar or non-planar
surface), extrudes it into three dimensions along either the normal to
the surface (default) or along a user defined vector, and then takes
the external surface of the volume created and returns that to the
user. This operation will result in a closed surface.

## FORMAT

<pre>
<b>bubble</b>/mesh1/mesh2/onstmin/offset/[norm**x1,y1,z1]
</pre>

* *mesh1* is the name of the resulting mesh.

* *mesh2* is the name of the initial mesh. This mesh must be either made up
of ris, quads, or hybrids.

* **`const`** is a keyword that indicates that the distance from each of the
points in the initial mesh along the extruding vector will be equal to
offset.Therefore, if you wanted the closed surface mesh to have the same
surface characteristics as the original mesh on both the initial and
newly formed surface or edge, you would use **`const`**.

* **`min`** is a keyword that indicates that the minimum distance along the
extruding vector to a reference plane that is perpendicular to the
extruding vector will be equal to offset. This means that if you want a
closed surface mesh with at least one flat side, you would use **`min`**.
This also means that if you use **`min`**, bubble computes the "bottom
point" on the initial mesh, or the point closest to the reference plane,
and then extrudes that point by min, all the other points will be
extruded by a larger distance. This avoids the problem of having the
initial surface intersect the reference plane that forms the other side
of the closed surface mesh.

* `offset` is the length of extrusion. It can either be an integer or a real.

The final argument is optional. It must either be the keyword **`norm`**,
or a three valued vector (in cartesian space) specifying a direction.
The default, if no argument is provided, is **`norm`**. If **`norm`** is
chosen, the element weighted average normal to the surface or curve is
computed, and the initial mesh is extruded in that direction. Otherwise,
if a vector value is specified, the vector is normalized, and its
direction used to extrude the initial mesh.

## NOTES

This code works on meshes containing quads, triangles, or hybrid
polygons.

It is very possible to create an invalid mesh object with this
command, especially if the initial mesh is a multivalued surface, or
if the extruding vector is in a direction parallel to the plane that
contains the initial surface is in. You have been warned.

There is an analog to this code that creates the volume enclosed by
the surface as opposed to the surface itself. It is called
[`extrude`](extrude.md).

This code is a wrapper for `extrude`. There are plans to integrate
`bubble`'s functionality with `extrude` and to eliminate
`bubble` from the commands recognized by LaGriT.

## EXAMPLES

<pre>
<b>bubble</b>/cmo_bigbox/cmo_quad/<b>const</b>/5.0/
</pre>

This would result in a surface surrounding an amalgamation of
parallelopipeds created from the initial quad sheet. First, since
**`const`** is used the quads will be extruded a constant amount from
each point in the quad sheet.

Second, since the extruding vector and **`norm`** are omitted,
the extrusion will occur on the average normal to the plane.
Therefore, this command will result in a mesh of tris
that form the surface of a group of parallelopipeds extruded 5.0 units
in an orthogonal direction.

<pre>
<b>bubble</b>/cmo_arbshape/cmo_tri/<b>min</b>/7.5/3,-2.5,-6
</pre>

This command would result in a mesh of tris that form a surface
enclosing a volume of prisms being created out of the initial tri
sheet. First, since **`min`** is used, the "bottom" of the surface would
be a plane.

Second, because the vector *3, -2.5, -6* is specified, the
extrusion will be in that direction (again the magnitude is not
important, the vector is normalized to a unit vector), not in the
direction of the average normal of the initial tri surface.
