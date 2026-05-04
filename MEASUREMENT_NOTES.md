# HexVase Reference Measurements

## Extracted from vase001.3mf

**Source File:** `../Commercial License/HexVase/vase001.3mf`  
**Import Method:** Mesh.insert() - 75,248 faces, 37,680 points  
**Date Measured:** 2026-05-01

## Critical Dimensions for VarSet

### Overall Geometry
- **Overall Height:** 150.00 mm (target: ~120mm - NEEDS ADJUSTMENT)
- **Approximate Diameter:** 108.00 mm (target: 80-85mm - NEEDS ADJUSTMENT) 
- **X Width:** 108.00 mm
- **Y Width:** 107.97 mm
- **Wall Thickness (estimated):** 2.5 mm (target maintained)

### Bounding Box Coordinates
- **X:** 136.38 to 244.38 mm
- **Y:** 131.35 to 239.32 mm  
- **Z:** 0.00 to 150.00 mm

### Lip Geometry Analysis
- **Estimated Lip Height:** ~15.00 mm (10% of total height)
- **Current Issue:** Sharp overhangs detected - requires 50° chamfer improvement
- **Top Region:** Z > 135.00 mm

## VarSet Parameter Recommendations

Based on measurements and target specifications:

### Primary Dimensions
```
VaseHeight = 120.0 mm          # Reduce from current 150mm
VaseBottomDiameter = 80.0 mm   # Reduce from current 108mm  
VaseTopDiameter = 85.0 mm      # Reduce from current ~108mm
VaseWallThickness = 2.5 mm     # Maintain current estimate
```

### Lip Chamfer (NEW - for FDM printability)
```
LipChamferAngle = 50.0 deg     # FDM-friendly angle
LipChamferHeight = 12.0 mm     # Proportional to overall height reduction
```

### Honeycomb Pattern (to be determined)
```
HexCellSize = TBD mm           # Need to analyze mesh pattern
HexWallThickness = TBD mm      # Need to analyze pattern structure
HexDepth = TBD mm              # Need to analyze relief depth
```

## Notes

1. **Scale Adjustment Required:** Current vase is ~25% larger than target specifications
2. **Lip Improvement:** Original has sharp overhangs causing print failures - needs 50° chamfer
3. **Honeycomb Pattern:** Detailed pattern analysis requires further mesh inspection
4. **Parametric Approach:** All dimensions must be controlled via VarSet for tuning flexibility

## Next Steps

1. Create Params.FCStd with VarSet containing above parameters
2. Develop parametric sketch for vase profile with chamfered lip
3. Implement honeycomb pattern generation (sketch or array)
4. Test print verification workflow