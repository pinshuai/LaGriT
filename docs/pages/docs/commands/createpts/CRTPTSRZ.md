---
title: CREATEPTS xyz rtz rtp line
---

 
# CREATEPTS/ xyz rtz rtp line #

  This command adds points to a mesh object. It can distribute points evenly or according to a ratio zoning method as indicated by the choices **xyz**, **rtz**, **rtp**, or **line**. These points can be connected into a tet mesh object. If you want a connected hex mesh object, use the **createpts/brick** commands instead.
  
## FORMAT ##

<pre> 
cmo/create/ mo_name / / / tet

<b>createpts</b> / <b>xyz</b> or <b>rtz</b> or <b>rtp</b> / ni,nj,nk / xmin,ymin,zmin / xmax,ymax,zmax / iiz,ijz,ikz / [ iirat,ijrat,ikrat /xrz,yrz,zrz ]

<b>createpts</b> / <b>line</b> / npoints / / / xmin,ymin,zmin / xmax,ymax,zmax / iiz,ijz,ikz /
 </pre>
 

**`xyz`** Cartesian coordinates.

**`rtz`** Cylindrical coordinates with center at (0,0,0). Use a **trans** command to move the center to a new location. The minimum and maximum coordinates are the triplets: radius from the cylinder's axis, angle in the xy-plane measured from the x-axis, and height along the z-axis. 
  Note that the **rtz** always results in a (partial) cylinder of points
  centered around the z axis. Use the **rotateln** command to orient
  the cylinder. For example, to center the cylinder around the y axis,
  specify the x axis as the line of rotation in the **rotateln** command.

**`rtp`** Spherical coordinates with center at (0,0,0). Use a **trans** command to move the center to a new location. The minimum and maximum coordinates are the triplets:   
  radius from the center of the sphere axis, angle in the zy-plane measured from the positive z-axis, and the angle in the xy-plane measured from the positive x-axis ([see II.a.11](../../conventions.md)). 

**`line`** this option implies xyz and will distribute npoint nodes from (xmin,ymin,zmin) to (xmax,ymax,zmaz)
  
  
*`ni,nj,nk`* are the number of points to be created in each direction.

*`xmin,ymin,zmin`* are the minimums for coordinates.

*`xmax,ymax,zmax`* are the maximums for coordinates.

*`iiz,ijz,ikz`* 0 or 1 switches 
  
* if 0 then mins and maxs are used as cell centers

* if 1 then mins and maxs are used as cell vertices
    

*`iirat,ijrat,ikrat`* ratio zoning switches 0=off (default), 1=on

*`xrz,yrz,zrz`* ratio zoning value - distance is multiplied by this
  value for each subsequent point.


# EXAMPLES #

```
createpts/xyz/ 5,3,10 /0.,2.,0./5.,6.,2./1,1,1/
```
This results in a set of 150 points, five across from x=0. to x=5.,
3 deep from y=2. to y=6. and 10 high from z=0. to z=2.
```
cmo/create/ motet / / / tet
createpts/rtz/ 4,6,11 /0.,0.,0./3.,360.,10./1,0,1/
cmo/setatt/ motet/ imt/ 1
filter/1,0,0; rmpoint/compress;
connect
```
  This results in 264 points arranged around the z- axis.   
  There are 3 rings of points at distances r=1., r=2. and r=3. from the z-axis.  
  There are 11 sets of these three rings of points and heights z=0.,
  z=1., z=2.,...,z=10.   
  In each ring there are 6 points where each pair of points is separated by 60°   
  Note that ijz=0 requests that points
  be placed at cell centers, hence the first point will be at 30° not
  at 0°.  
  Corresponding to r=0, there will be 6 identical points at 11
  intervals along the z-axis at heights z=0., z=1., z=2.,...z=10.
The **filter** command tags duplicate points and the **rmpoint/compress** removes the tagged points and updates the mesh object. The **connect** command will create a connected tetrahedral mesh object.
  

```
define XP1 1.
define YP1 1.
define XP2 100.
define YP2 150.
define N_POINTS 100

cmo/create/mo_line 
createpts/line/ N_POINTS / / /XP1 YP1  0. /  XP2 YP2 0. /1 1 1/
```
Create a line of 100 unconnected points from point 1,1,0 to 100,150,0.


