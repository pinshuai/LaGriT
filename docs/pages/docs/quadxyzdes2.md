Description

qquadxyz/5 25 7/ 0. 0. 0. /1. 0. 0. /1. 2. 0. /0. 2. 0. /&

0. 0. 10. /1. 0. 10. /1. 2. 10. /0. 2. 10. /
Define an arbitrary, logical hexahedron of points in the xy plane.

 

Argument | Description
------------| --------------------------------------------------
5 25 7 |     create 5 points between the 1st and 2nd point. 

            create 25 points between the 1st and 4th point.

            create 7 points between the 1st and 5th point.

0
. 0. 0. |  first corner of first quad

1. 0. 0. |  second corner of first quad

1
. 2. 0. |  third corner of first quad

0
. 2. 0. |  fourth corner of first quad

0
. 0. 10. | first corner of second quad

1
. 0. 10. | second corner of second quad

1
. 2. 10. | third corner of second quad

0
. 2. 10. | fourth corner of second quad

Input file:

    *input.hex
    * create a hexaheral grid
    cmo create abc///hex
    quadxyz/5 25 7/ 0. 0. 0. /1. 0. 0. /1. 2. 0. /0. 2. 0. /&
    0. 0. 10. /1. 0. 10. /1. 2. 10. /0. 2. 10. /
    *cmo/printatt//-xyz-
    setpts
    creatpts/brick/xyz/5 25 7/1,0,0/connect/
    settets
    dump/gmv/gmv.myhex
    dump/avs/avs.myhex/abc/
    finish
