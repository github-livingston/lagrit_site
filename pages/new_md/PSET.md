---
GENERATOR: 'Mozilla/4. [en] (X11; U; IRIX 6.5 IP32) [Netscape]'
Generator: Microsoft Word 98
title: PSET
---

 

 **PSET**

  Give a name to a selected set of points.

  **seq** forms a pset of the nodes in ifirst, ilast, istride;

  the special sets: 1,0,0 refers to all nodes and 0,0,0 refers to the
  last set of nodes created.

  **union, inter** and **not** are logical operations on previously
  defined psets.  The definition of the unary operator **not** is
  extended such that **not**/p1/p2 means p1 and (not(p2)).

  **list** lists nodes in a pset or names of all psets

  **delete** deletes a previously defined pset

  **attribute ** forms a pset from all points in ** **
  ifirst,ilast,istride which have the specified value for a node based
  attribute. This option was previously named **zq.**

  If the optional comparator field is given; that operation is used to
  compare the attribute value to the requested value.

  **geom/xyz**/ forms a pset from all points inside the box whose
  corners are xl,yl,zl and xu,yu,zu relative to the geometry center at
  xc,yc,zc.

  **geom/rtz**/ forms a pset of nodes within the cylinder or
  cylindrical shell given by radius r1 to r2, angle t1 to t2 and
  height z1 to z2.

  **geom/rtp**/ forms a pset of nodes within the sphere, sperical
  shell or sperical section given by r1 to r2, and angles t1 to t2 and
  p1 to p2.  [See chapter II, A. Conventions](conventions.md) for an
  explanation of angles theta and phi.

  **surface** identifies nodes on the specified surface.  Keyword
  surface names have the following meaning:
 
   -**all**- will identify nodes on any surface.

   -**interface**- will identify nodes on any interface surface.

   -**boundary**- will idendify nodes on exterior surfaces.

**eltset** form a pset of nodes in the element set listed.

**constraints** forms a pset of nodes having the specified number of
constraints.  The node's **icr** value is used as an index to the
**icontab** attribute which gives the number of constraints.  [See
chapter III, A](meshobject.md) for an explanation of the **icontab**
entries.

**FORMAT:**

**pset**/pset name

**seq**/ifirst,ilast,istride

**unioninternotdelete**/pset1[/pset2/.../psetn]

**list**

**delete**

**attribute**/attribute /ifirst,ilast,istride/value/

  [**le** **gt** **gt** **ne** **eq**]

**zq**/attribute /ifirst,ilast,istride/value/[**le** **gt** **gt**
**ne** **eq**]

**region**/region name/ifirst,ilast,istride

**mregion**/mregion name/ifirst,ilast,istride

will return all nodes that are in the specified mregion - the definition
of the mregion is evaluated to determine membership.  Hence the result
may vary from what would be returned if the 'imt1' value of the nodes
had been queried using the **attribute** option

**geom** **/xyz**/ifirst,ilast,istride/xl,yl,zl/xu,yu,zu/xcen,ycen,zcen

**geom** **/rtz**/ifirst,ilast,istride/r1,t1,z1/r2,t2,z2/xcen,ycen,zcen

**geom** **/rtp**/ifirst,ilast,istride/r1,t1,p1/r2/t2/p2/xcen,ycen,zcen

**surface**/surface\_name/[ifirst,ilast,istride]

**surface** will select nodes that are on the specified surface.  If
**-interface-** is specified for the surface name, all interface  nodes 
will be returned.  If **-boundary-** is specified for the surface name,
all nodes on external bounding surfaces will be returned. If **-all-**
is specified all nodes on any surface are returned.

**eltset**/element\_set\_name

**eltset** will return all nodes that are vertices of the elements in
the specified element set

**constraints**/number\_of\_constraints/ifirst,ilast,istride

 

**EXAMPLES:**

**pset**/apset**/seq**/1,0,0/

 associate the pset name apsetwith all points.

**pset**/apset**/seq**/0,0,0/

 associate the pset name apsetwith the last set of nodes created.

**pset**/apset**/union**/pset1,pset2,pset

 associate the pset name apset with the set of nodes which belong to at
least one of pset1, pset2, pset3.

**pset**/apset**/inter**/pset1,pset2,pset3

   associate the pset name apset with the set of nodes which belong to
pset1, and pset2, and pset3.

**pset**/apset**/not**/pset1,pset2,pset3

   associate the pset name apset with the set of nodes which belong to
pset1, and do not belong to pset2, and do not belong to pset3

**pset**/apset**/not**/pset1

   associate the pset name apset with the set of nodes which do not
belong to pset1

**pset**/**/list**/

   list the names of all psets

**pset**/apset**/attribute** **/itp**/1,0,0/10**/ge**

   associate the name apset with the points whose type field(**itp1**)
has value greater than or equal to 10 (these would be boundary nodes).

**pset**/mypset**/list**

   list the node numbers of the members of mypset

**pset**/mypset**/geom** **/xyz**/1,0,0/1.,1.,-5./10.,20.,10./

   associate the name mypset with all nodes that fall with the box with
corners at (1,1,-5) and (10,20,10)

**pset**/mypset**/geom/rtz/pset,get,**oldpset/0.,0.,0./10.,360.,10.  
associate the name mypset with the nodes that are members of the pset
oldpset and which fall inside the cylinder of radius 10 and height 10
and whose axis is the z-axis.

**pset**/spset**/surface**/s1/1,0,0

  associate the name spset with the set of nodes that lie on the surface
s1.

**pset**/spseta**/surface**/s2**/pset,get,spset**

  associate the name spseta with the set of nodes that lie on the
surface s2 and which are members of the pset spset  This command and the
previous command would identify the nodes that are on the intersection
of surfaces s1 and s2 and give the name spseta to these nodes.

**pset**/mypset**/constraints**/3

 associate the name mypset with the set of nodes that have 3 constraints
( normally the set of nodes that lie on 3  constrained surfaces --
surfaces of type **reflect** or **intrcons**)
[Click here for demos](../docs/demos/pset/md/main_pset.md)
