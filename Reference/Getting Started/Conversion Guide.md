---
aliases: 
tags: 
---

# Conversion Guide

I abhor XIC for editing, particularly because I'm so used to a wealth of tools and routines within AutoCAD to make my life so much easier. So, I've developed a routine to create layouts in AutoCAD, export them to an intermediary DXF, and finally to the GDSII format needed for XIC. To ensure compliance with Star Cryo's tech file, there are a few details to pay particular attention to:

1. Export from AutoCAD to DXF
	 1. Perform a `Purge`, removing any AutoCAD objects, including:
		  - Groups
		  - Arrays
		  - Temporary Blocks
	 2. Name blocks with only `$`, `_`, and alphanumerics. Follow [[cell hierarchy naming guide]].
	 3. Name layers as `L%D@` with designation `%` and #dakine `@` (typically 0)
	 4. (Not tested) Probably needs to be unitless, as units will ultimately be in microns
2. Export from DXF to GDS in KLayoutEditor
	 1. Hide/delete layer `0` (and non-printing layer `Defpoints`, if left in the AutoCAD file)
	 2. Clean up any cells from other paperspace tabs
    	 1. Change Levels (under Cell sidebar) to 
	 3. Save as GDS, including only visible layers
3. Open GDS in XIC
	 1. Verify the Cell Tree looks correct, and all cells are correct
	 2. Verify geometry, which can be easier now that geometries are filled
		  1. *Check this! Thick polylines should now be traces, and other polygons should be filled.*
		  2. (Not tested) Likely, open polylines w/ 0 global width should have given an error by now.
