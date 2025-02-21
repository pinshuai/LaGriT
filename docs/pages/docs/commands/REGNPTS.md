---
title: REGNPTS
tags: ok
--- 

**REGNPTS**

  Generates points in a region previously defined by the region
  command. The points are generated by shooting rays through a user
  specified set of points from an origin point, line, or plane and
  finding the intersection of each ray with the surfaces that define
  the region. The point distribution is determined by the data in
  ptdist. If ptdist is integer, then that many points are evenly
  distributed along the ray in the region. If ptdist is real, then
  points are distributed at that distance along the ray, up to a
  maximum of maxpenetr points along the ray (in addition to any
  interface points that may be created). note: If the ray encounters a
  region more than once, multiple sets of points are layed down.
  Points are distributed on the regionís material interfaces and
  external boundaries if the region definition includes the interfaces
  or boundaries -- usually **ge** or **le** means that the region
  includes the interface or boundary.

  Only surface intersection points are created if ptdist is
  **inside**, **in**, **out**, **outside**, or**both.** In this case,
  surface points are created regardless of region ownership of the
  interface or boundary surface -- if a ray encounters a region more
  than once, the appropriate surface intersection point(s) is
  generated for each encounter.

  If another region intrudes upon the regnpts region so that the
  regpts region is divided into more than one piece, points that fall
  inside the intruding region are not distributed.

  The variables irratio and rrz determine ratio zoning when ptdist is
  an integer. Ratio zoning is on when irratio is 1; the point
  distribution is adjusted so that the ratio between successive pairs
  of points is rrz. When irratio is 3, ratio zoning is calculated on
  the longest ray; then this length distribution is applied to all
  rays.

  See the description of the command **surface** for a discussion of
  point distributions with respect to sheet surfaces.

 **FORMAT:**

 **regnpts**/region name/ptdist/ifirst,ilast,istride/geom/

 ray origin/irratio,rrz,maxpenetr

 **regnpts**/region name/ptdist**/pset**,**get**,setname/geom/ray
 origin /irratio,rrz/maxpenetr

 Where ifirst,ilast,istride or **pset**,**get**,setname define the set
 of points to shoot rays through.

 **SPECIFICALLY FOR ALLOWABLE GEOMETRIC TYPES:**

 **regnpts**/region name/ptdist/ifirst,ilast,istride**/xyz**

 /x1,y1,z1/x2,y2,z2/x3,y3,z3/irratio,rrz/maxpenetr

 Where points 1, 2, 3 define the plane to shoot rays from that are
 normal to the plane.

 **regnpts**/region name/ptdist/ifirst,ilast,istride/
 **rtz**/x1,y1,z1/x2,y2,z2/irratio,rrz/

 Where points 1, 2, define the line from which to shoot perpendicular
 rays

 **regnpts**/region name/ptdist/ifirst,ilast,istride/

 **rtp**/xcen,ycen,zcen/irratio,rrz,maxpenetr

 Where xcen,ycen,zcen define a point from which to shoot rays .

 **regnpts**/region
 name/ptdist/ifirst,ilast,istride**/points**/iffirst,iflast,ifstride/irratio,rrz/
 maxpenetr

 Where the 2 point sets have the same length and rays are constructed
 between pairs of elements, one from each point set.

 [Click here for demos](../demos/main_regnpts.md)
