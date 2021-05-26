# Geometry
支持OGC中所有的空间数据类型，如下：

> * Point and MultiPoint
> * LineString and MultiLineString
> * Polygon and MultiPolygon
> * heterogeneous GeometryCollection

## Point
表示空间位置中的点
```go
point := geoos.Point{116,39}
```

## LineString
线是由一个或多个路径定义的形状，其中路径是指一系列相连线段。
```go
lineString:=geoos.LineString{{-24, 63},{-23, 60},{-25, 65},{-20, 69}}
```go

## Polygon
面是指由一系列相连的 x,y 坐标对定义的闭合形状。
```
polygon := Polygon{{{-5, 52},{-4, 56},{-2, 51},{-5, 52}}}
```
......