# HexVase Parametric Reconstruction Design

**Date:** 2026-04-29  
**Project:** Honeycomb Pattern Vase Recreation  
**Objective:** Recreate parametric vase with improved 50° lip chamfer for better printability

## Background

Original vase had sharp overhang lip causing print quality issues. Need parametric reconstruction from existing 3MF file with:
- Improved lip geometry (50° chamfer for FDM printability)  
- Full parametric control via VarSet
- Reusable template for design variations

## Architecture

**File Structure:**
- `Params.FCStd` - VarSet document with all parameters
- `HexVase.FCStd` - Main model with XLink to Params  
- All dimensions bound via `<<Params>>#VarSet.VarName`

**VarSet Parameters:**
```
# Base Geometry
VaseHeight: 120mm (from 3MF measurement)
BottomDiameter: 80mm  
TopDiameter: 85mm (slight taper)
WallThickness: 2.5mm

# Printable Lip Design  
LipChamferDepth: 3mm
LipChamferAngle: 50° (prevents overhang issues)

# Honeycomb Pattern
HexSize: 8mm (inscribed diameter)
HexDepth: 1.5mm (emboss relief)  
HexSpacingX: 9mm (center-to-center)
HexSpacingY: 7.8mm (offset rows)
PatternStartHeight: 10mm (from base)
PatternEndHeight: 100mm (below lip)
```

## Modeling Workflow (Traditional PartDesign)

**Phase 1: Base Vase**
1. Import reference 3MF → extract dimensions
2. Create/populate VarSet parameters  
3. Base cylindrical sketch (BottomDiameter) on XY_Plane
4. Pad with taper to TopDiameter at VaseHeight
5. Shell operation using WallThickness  
6. Chamfer lip using LipChamferDepth/Angle parameters

**Phase 2: Honeycomb Pattern**
1. Master hexagon sketch on YZ_Plane
2. Position using PatternStartHeight constraint
3. Pad hexagon (HexDepth parameter)
4. Array pattern with HexSpacing parameters
5. Constrain pattern bounds (StartHeight to EndHeight)

**Phase 3: Design Variations** 
- Modify VarSet for different designs
- Pattern variations: HexSize, spacing, depth
- Form variations: height/diameter ratios  
- All changes propagate parametrically

## Constraints

- 50° overhang maximum for FDM printing
- All features attached to datum planes (not faces)
- One parameter per clearance concept
- Idempotent macro-based workflow
- Compatible with CAD_STANDARDS.md requirements

## Success Criteria

- Parametric model rebuilds reliably with parameter changes
- Lip prints cleanly at 50° overhang
- Template enables rapid design variations
- Follows established FreeCAD workflow patterns