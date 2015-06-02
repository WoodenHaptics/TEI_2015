

  Please note the following for laser-cutting the parts.

  - All sheets are 6 mm, preferably birch plywood
  - The source drawing(s) in .SLDDRW for each body is found in respective part's folder
  - These files are exported to .dxf files in the lasercut_drawing/dxf/ folder
  - If you alter the parts of a body, the .DWG will be updated when you load them, but
    not necessarily any exported files. So make sure to do the export (save as...) as well.
  
  - You can use the dxf directly if:
    * Your laser-cutter can handle up to A2 sheets (594 x 420 mm)
    * You make sure the laser-cutter cuts in the middle of the lines, or change
      the thickness to be as thin as is required to do so (for VLS-4.60 you set it to ~0.001 mm)
    * The BLACK AREAS should be ENGRAVED to 1.5-2.5 mm, instead of cut. Be careful to 
      set the edges of those areas to be cut through OR not cut through depending on location.
  
  - Otherwise, we reccommend:
    * Using Adobe Illustrator; "place" the .DXF file(s) on a sheet suitable for your cutter.
    * You may have to place with scaling 1:1000 or 1000:1, make sure it NEVER scales to "fit"
    * Always measure an object to see it is exactly as expected
    * Change lines to be as thin as necessary (0.001 mm/pt in our case)
    * Change line colors to be what you code as "cut through" (RGB: 255,0,0 in our case)
    * Change black areas to be coded as "engraving" (see above, in our case fill with RGB: 0,0,0)


  /Jonas Forsslund Jan 5th 2015
