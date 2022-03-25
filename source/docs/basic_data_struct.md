## Geometry
Support for all Geometry types defined in the OGC Simple Features for SQL specification, including:

> * Point and MultiPoint
> * LineString and MultiLineString
> * Polygon and MultiPolygon
> * heterogeneous GeometryCollection

## Point
Creates a Point Feature from a Position.
```
point := space.Point{116, 39}
```

## LineString
Creates a LineString Feature from an Array of Positions.
```
lineString := space.LineString{{-24, 63}, {-23, 60}, {-25, 65}, {-20, 69}}
```

## Polygon
Creates a Polygon Feature from an Array of LinearRings.
```
polygon := space.Polygon{{{-5, 52}, {-4, 56}, {-2, 51}, {-5, 52}}}
```
……