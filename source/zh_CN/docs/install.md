## 安装使用

安装 geoos
```sh
$ go get github.com/spatial-go/geoos
```

## 快速入门
怎样使用 `GeoOS`:
示例: 用`GeoOS`计算`area`
```
package main

import (
	"bytes"
	"fmt"
	"log"

	"github.com/spatial-go/geoos/geoencoding"
	"github.com/spatial-go/geoos/planar"
	"github.com/spatial-go/geoos/space"
)

func main() {
	// First, choose the default algorithm.
	strategy := planar.NormalStrategy()
	// Secondly, manufacturing test data and convert it to geometry
	const polygon = `POLYGON((-1 -1, 1 -1, 1 1, -1 1, -1 -1))`
	// geometry, _ := wkt.UnmarshalString(polygon)

	buf := new(bytes.Buffer)
	buf.Write([]byte(polygon))
	geometry, _ := geoencoding.Read(buf, geoencoding.WKT)

	// Last， call the Area () method and get result.
	area, e := strategy.Area(geometry)
	if e != nil {
		fmt.Printf(e.Error())
	}
	fmt.Printf("%f", area)
	// get result 4.0

	rawJSON := []byte(`
  { "type": "FeatureCollection",
    "features": [
      { "type": "Feature",
        "geometry": {"type": "Point", "coordinates": [102.0, 0.5]},
        "properties": {"prop0": "value0"}
      }
    ]
  }`)

	buf1 := new(bytes.Buffer)
	buf1.Write([]byte(rawJSON))
	fc, _ := geoencoding.ReadGeoJSON(buf1, geoencoding.GeoJSON)

	// Geometry will be unmarshalled into the correct geo.Geometry type.
	point := fc.Features[0].Geometry.Coordinates.(space.Point)
	log.Println(point)
}

```