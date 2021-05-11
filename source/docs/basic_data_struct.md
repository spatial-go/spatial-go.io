## Point
Creates a Point Feature from a Position.
```
point := geoos.Point{116.386442,39.911337}
```

## LineString
Creates a LineString Feature from an Array of Positions.
```
lineString:=geoos.LineString{{116.386442,39.911337},{116.688566,39.531076},{117.18295,39.097582}}
```

## Polygon
Creates a Polygon Feature from an Array of LinearRings.
```
polygon := Polygon{{{116.386442,39.911337},{116.688566,39.531076},{117.18295,39.097582},{116.386442,39.911337}}}
```