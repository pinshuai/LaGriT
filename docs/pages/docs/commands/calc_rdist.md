---
title: CALC_RDIST 
tags: ok
---

# CALC_RDIST

This command is a macro command that calculates the radial distance
from a specified point to a set of points. That set of points can be
defined using the standard LaGriT syntax of psets and range. If the
specification for a set of points is omitted, the whole grid is
used. The command operates on the current mesh object.
This operation will (often) result in two attributes being added to
the current mesh object. The first, a real named rdist, contains the
radial distance from the point of interest. The second, an integer
named ictrpt, contains an index that specifies the center point that
was used for this calculation.

## FORMAT

<pre>
<b>calc_rdist</b>/x0,y0,z0/ [radius_index] / [<b>pset,get,</b> pset_name, ifirst,ilast,istride]
</pre>

* **x0,y0,z0** are the coordinates of the center point used in the
calculation.

* `radius_index` is an optional integer. It serves as an index for a
specific center point.  Its value is placed in the attribute

ictrpt throughout the range affected by the command. If it is not
specified, no changes are made to the attribute ictrpt. The
non-value for this attribute is 0 (i.e., if there is no radius
index, the value of ictrpt will be 0).

The last argument that `calc_rdist` takes specifies the range
over which the command will be executed. If it is omitted, the whole
grid is assumed.

## NOTES

This command is a macro command. It does not add any new
functionality.

## EXAMPLES

<pre>
<b>calc_rdist</b>/0,0,0
</pre>
 
This command would calculate the distance from the origin to all
points in the mesh, and place the values in rdist. It would not
modify ictrpt in any way.
 
<pre>
<b>calc_rdist</b>/1,0.25,1/10/pset,get,big_sphere
</pre>
 
This command would calculate the distance from the point 1,0.25,1
to all the points within the pset `big_sphere`. It would place
those distances into rdist within that pset, and would replace the
value of `ictrpt` with 10 within that pset as well.
