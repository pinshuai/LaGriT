---
GENERATOR: 'Mozilla/4.79C-SGI [en] (X11; U; IRIX64 6.5 IP30) [Netscape]'
title: 'cmo/addatt'
---

cmo/addatt
----------

 The general version of the **cmo/addatt** command is used to add and initialize a new mesh
 object attribute. Note for the general form, parameters will resort to default settings if not
 included on the command line. 
 See the **[modatt](cmo_modatt.md)** command for details on these  attribute parameters.

 
 **GENERAL FORMAT:**

  **cmo/addatt** / mo\_name / att\_name / [ type / rank / length /
  interpolate / persistence / ioflag / value ]

 
 The keyword syntax uses keywords to create and/or fill a valid attribute
 with values as defined by the keyword being used.
 The keyword is the fourth token on the command line and the syntax for each keyword 
 is unique as defined below. If the named attribute already exists, values will be
 overwritten with values as indicated by the keyword.
 This syntax can also derive a vector attribute from three attributes or derive three 
 scalar attributes from a vector attribute.


 **KEYWORD FORMAT:**

  **cmo/addatt** / mo\_name / **area\_normal** / normal\_type /
  att\_v\_name

  **cmo/addatt** / mo\_name / **unit\_area\_normal** / normal\_type /
  att\_v\_name

  **cmo/addatt** / mo\_name / **volume** / att\_name

  **cmo/addatt** / mo\_name / **vector** / att\_v\_snk / att\_1src,
  att\_2src, att\_3src

  **cmo/addatt** / mo\_name / **scalar** / att\_1snk, att\_2snk,
  att\_3snk / att\_v\_src

  **area\_normal**: creates vector attribute att\_v\_name and fills
  with the x,y,z components of the area normal for each face. The new
  attribute is [nelements](meshobject.md#nelements)in length, type
  is [VDOUBLE](meshobject.md#type), and rank is
  [vector](meshobject.md#vector). normal\_type choices include
  **xyz, rtz**, and **rtp**. The area\_normal is a vector
  perpendicular to the triangle face with length equal to the area of
  the triangle. Currently implemented for **xyz** on triangles only.
 
  **unit\_area\_normal**: creates vector attribute att\_v\_name and
  fills with the x,y,z direction components of the area normal for
  each face. The new attribute is nelements in length, type is
  VDOUBLE, and rank is vector. normal\_type choices include **xyz,
  rtz**, and **rtp**. The unit\_area\_normal is a vector perpendicular
  to the triangle face with length equal to one. Currently implemented
  for **xyz** on triangles only.
 
  **volume** or **area**: creates an attribute nelements in length and
  type VDOUBLE. For **volume** keyword the att\_name attribute is
  filled with **volume**(if 3D), **area**(if 2D) or **length**(if
  lines). Currently implemented for triangle areas.
 
  **vector**: creates att\_v\_snk of rank vector from three existing
  attributes att\_1src, att\_2src, and att\_3src
 
  **scalar**: creates three attributes att\_1snk, att\_2snk, and
  att\_3snk from an existing attribute att\_v\_src of rank vector.

 

 **EXAMPLES:**

  **cmo** **/addatt**/cmo1/boron1**/VDOUBLE** **/scalar** **/nnodes** **/asinh** **/permanent**
  Create node attribute named boron1 with interpolate method of asinh.
  **cmo/addatt**/-cmo-/boron2**/VDOUBLE/scalar/nnodes/asinh/permanent/gl**/2.0
  Create node attribute named boron2 and fill with value 2.0, write to
  gmv and lagrit dumps.
  **cmo/addatt**/cmo1/boron3**/VDOUBLE/scalar/nnodes/user/temporary**
  Create temporary node attribute named boron3.
  **cmo/addatt/-default-**/boron3
  Create attribute named boron3 with default mesh object settings.
  **cmo/addatt**/ cmotri / **area\_normal** / **xyz** / anorm
  Create and fill element vector named anorm with the x,y,z components
  for area normals of each triangle.
  **cmo/addatt**/ cmotri / **unit\_area\_normal** / **xyz** / n\_face
  Create and fill element vector named n\_face with the x,y,z
  components for unit area normals of each triangle.
  **cmo/addatt**/cmo1/ **scalar** / xnorm, ynorm, znorm / anorm
  Create attributes xnorm, ynorm, znorm from the three components of
  the vector attribute anorm.
  **cmo/addatt**/cmo1/ **vector** / vnorm /xnorm, ynorm, znorm
  Create vector attribute vnorm from the three attributes xnorm,
  ynorm, znorm.
  **cmo/addatt**/ cmotri / **area** / darea
  Create and fill attribute named darea with area of each triangle.
  
  
This example will fill an attribute with a cmo scalar value.
First a scalar value is created from the max value in zic, then all zic are set to this value.
Note error may occur due to difference in attribute length but can be ignored.

```
cmo/ addatt/ mo /maxnode/ zic_new/ zic
cmo/ copyatt/ mo mo / zic zic_new
cmo/ printatt /mo/ zic_new
cmo/ printatt/ mo/ zic

# Result complains but values are written

cmo/ addatt/ mo /maxnode/ zic_new/ zic                                              
ADDATT/maxnode: creating new attribute: zic_new                                 
 
cmo/ copyatt/ mo mo / zic zic_new                                                   
Error from:   incompatible att length types for   cmo_copyatt                   
 Special Copy...
         3 copied from mo element zic_new to -> mo node vertices zic            
 
cmo/ printatt /mo/ zic_new                                                         
Attribute: zic_new                                                              
         1  2.90000E+03                                                         
 
cmo/ printatt/ mo/ zic                                                             
Attribute: zic                                                                  
         1  2.90000E+03                                                         
         2  2.90000E+03                                                         
         3  2.90000E+03        
```         
         
