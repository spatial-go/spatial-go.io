## Geometry
支持OGC中所有的空间数据类型，如下：

> * Point and MultiPoint
> * LineString and MultiLineString
> * Polygon and MultiPolygon
> * heterogeneous GeometryCollection

## Point
点对象经常与光标配合使用。点要素将返回单个点对象而不是点对象数组。而其他要素类型（面、折线和多点）都将返回一个点对象数组，并且当这些要素具有多个部分时，则返回包含多个点对象数组的数组。
```
point := geoos.Point{116,39}
```

## LineString
折线对象是由一个或多个路径定义的形状，其中路径是指一系列相连线段。
```
lineString:=geoos.LineString{{-24, 63},{-23, 60},{-25, 65},{-20, 69}}
```

## Polygon
面对象是指由一系列相连的 x,y 坐标对定义的闭合形状。
```
polygon := Polygon{{{-5, 52},{-4, 56},{-2, 51},{-5, 52}}}
```