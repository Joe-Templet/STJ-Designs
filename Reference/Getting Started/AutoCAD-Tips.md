---
aliases: 
tags: 
---
# Design Tips and Tricks

## Polyline Width to Exclusion

While wide polylines convert nicely from DWG to GDS as filled regions defined by a central spine (which is much easier to locate than individual vertices of the traces), AutoCAD does not respect the space taken up by linewidth as a geometry. So, tricks have to be played to say fill the region excluded by this thickness.

To do this, convert polylines to planar surfaces using `CONVTOSURFACE`. This can then be exploded into a Region object which surrounds the polyline. Regions are AutoCAD specific, so use `BOUNDARY` to create polylines which respect the boundaries of region objects, and be sure to delete the regions before trying to export to other tools.

In this fashion, filling with gold becomes a three step process:
1. Convert thick polylines to surfaces
	1. Explode
2. Fill region where gold should be with `BOUNDARY` polyline
3. Offset boundary polylines by 10.
4. Done!

